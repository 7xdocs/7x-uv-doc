# Storage

## 存储目录

uv 使用以下高级目录进行存储。

对于每个位置，uv 会按给定顺序检查环境变量是否存在，并使用找到的第一个路径。

存储目录的路径是平台相关的。在 Linux 和 macOS 上，uv 遵循 [XDG](https://specifications.freedesktop.org/basedir-spec/latest/) 规范；在 Windows 上，遵循 [已知文件夹](https://learn.microsoft.com/en-us/windows/win32/shell/known-folders) 方案。

### 临时目录

临时目录用于存储临时数据。

=== "Unix"

    1. `$TMPDIR`
    1. `/tmp`

=== "Windows"

    1. `%TMP%`
    1. `%TEMP%`
    1. `%USERPROFILE%`

### 缓存目录

缓存目录用于存储可丢弃但长期存在会有用的数据。

=== "Unix"

    1. `$XDG_CACHE_HOME/uv`
    1. `$HOME/.cache/uv`

=== "Windows"

    1. `%LOCALAPPDATA%\uv\cache`
    1. `uv\cache` within [`FOLDERID_LocalAppData`](https://learn.microsoft.com/en-us/windows/win32/shell/knownfolderid#FOLDERID_LocalAppData)

### 持久化数据目录

持久化数据目录用于存储不可丢弃的数据。

=== "Unix"

    1. `$XDG_DATA_HOME/uv`
    1. `$HOME/.local/share/uv`
    1. `$CWD/.uv`

=== "Windows"

    1. `%APPDATA%\uv\data`
    1. `.\.uv`

### 配置目录

配置目录用于存储对 uv 设置的更改。

用户级配置

=== "Unix"

    1. `$XDG_CONFIG_HOME/uv`
    1. `$HOME/.config/uv`

=== "Windows"

    1. `%APPDATA%\uv`
    1. `uv` within [`FOLDERID_RoamingAppData`](https://learn.microsoft.com/en-us/windows/win32/shell/knownfolderid#FOLDERID_RoamingAppData)

系统级配置

=== "Unix"

    1. `$XDG_CONFIG_DIRS/uv`
    1. `/etc/uv`

=== "Windows"

    1. `%PROGRAMDATA%\uv`
    1. `uv` within [`FOLDERID_AppDataProgramData`](https://learn.microsoft.com/en-us/windows/win32/shell/knownfolderid#FOLDERID_AppDataProgramData)

### 可执行文件目录

可执行文件目录用于存储用户可以运行的文件，即应位于 `PATH` 环境变量中的目录。

=== "Unix"

    1. `$XDG_BIN_HOME`
    1. `$XDG_DATA_HOME/../bin`
    1. `$HOME/.local/bin`

=== "Windows"

    1. `%XDG_BIN_HOME%`
    1. `%XDG_DATA_HOME%\..\bin`
    1. `%USERPROFILE%\.local\bin`

## 数据类型

### 依赖缓存

uv 使用本地缓存来避免重复下载和重新构建依赖。

默认情况下，缓存存储在[缓存目录](#缓存目录)中，但可以通过命令行参数、环境变量或设置来覆盖，如[缓存文档](../concepts/cache.md#cache-directory)中所述。当缓存被禁用时，缓存将存储在[临时目录](#临时目录)中。

使用 `uv cache dir` 显示当前缓存目录路径。

!!! important

    为了获得最佳性能，缓存目录需要与虚拟环境位于同一文件系统上。

### Python 版本

uv 可以安装托管的 [Python 版本](../concepts/python-versions.md)，例如使用 `uv python install`。

默认情况下，由 uv 托管的 Python 版本存储在[持久化数据目录](#持久化数据目录)的 `python/` 子目录中，例如 `~/.local/share/uv/python`。

使用 `uv python dir` 显示 Python 安装目录。

使用 `UV_PYTHON_INSTALL_DIR` 环境变量来覆盖安装目录。

!!! note

    更改 Python 的安装位置不会自动反映在现有的虚拟环境中；它们将继续引用旧位置，需要手动更新（例如，通过重新创建它们）。

### Python 可执行文件

uv 为 [Python 版本](#python-版本)安装可执行文件，例如 `python3.13`。

默认情况下，Python 可执行文件存储在[可执行文件目录](#可执行文件目录)中。

使用 `uv python dir --bin` 显示 Python 可执行文件目录。

使用 `UV_PYTHON_BIN_DIR` 环境变量来覆盖 Python 可执行文件目录。

### 工具

uv 可以使用 `uv tool install` 将 Python 包安装为[命令行工具](../concepts/tools.md)。

默认情况下，工具安装在[持久化数据目录](#持久化数据目录)的 `tools/` 子目录中，例如 `~/.local/share/uv/tools`。

使用 `uv tool dir` 显示工具安装目录。

使用 `UV_TOOL_DIR` 环境变量来配置安装目录。

### 工具可执行文件

uv 为已安装的[工具](#工具)安装可执行文件，例如 `ruff`。

默认情况下，工具可执行文件存储在[可执行文件目录](#可执行文件目录)中。

使用 `uv tool dir --bin` 显示工具可执行文件目录。

使用 `UV_TOOL_BIN_DIR` 环境变量来配置工具可执行文件目录。

### uv 可执行文件

当使用 uv 的[独立安装程序](./installer.md)安装 uv 时，`uv` 和 `uvx` 可执行文件会被安装到[可执行文件目录](#可执行文件目录)中。

使用 `UV_INSTALL_DIR` 环境变量来配置 uv 的安装目录。

### 配置文件

uv 的行为可以通过 TOML 文件进行配置。

配置文件在[配置目录](#配置目录)中被发现。

更多详细信息，请参阅[配置文件文档](../concepts/configuration-files.md)。

### 项目虚拟环境

在处理[项目](../concepts/projects/index.md)时，uv 会为每个项目创建一个专用的虚拟环境。

默认情况下，项目虚拟环境创建在项目或工作区根目录下的 `.venv` 中，即 `pyproject.toml` 旁边。

使用 `UV_PROJECT_ENVIRONMENT` 环境变量来覆盖此位置。更多详细信息，请参阅[项目环境文档](../concepts/projects/config.md#project-environment-path)。

### 脚本虚拟环境

当运行[带有内联元数据的脚本](../guides/scripts.md)时，uv 会在[缓存目录](#缓存目录)中为每个脚本创建一个专用的虚拟环境。