# Python 版本

一个 Python 版本由一个 Python 解释器（即 `python` 可执行文件）、标准库和其他支持文件组成。

## 托管和系统 Python 安装

由于系统上通常已存在 Python 安装，uv 支持[发现](#发现-python-版本) Python 版本。然而，uv 也支持自行[安装 Python 版本](#安装-python-版本)。为了区分这两种类型的 Python 安装，uv 将其自身安装的 Python 版本称为*托管* Python 安装，而所有其他 Python 安装称为*系统* Python 安装。

!!! note

    uv 不区分由操作系统安装的 Python 版本与由其他工具安装和管理的 Python 版本。例如，如果某个 Python 安装是由 `pyenv` 管理的，在 uv 中它仍被视为*系统* Python 版本。

## 请求版本

在大多数 uv 命令中，可以使用 `--python` 标志请求特定的 Python 版本。例如，在创建虚拟环境时：

```console
$ uv venv --python 3.11.6
```

uv 将确保 Python 3.11.6 可用——必要时会下载并安装它——然后使用它创建虚拟环境。

支持以下 Python 版本请求格式：

- `<version>`（例如：`3`, `3.12`, `3.12.3`）
- `<version-specifier>`（例如：`>=3.12,<3.13`）
- `<version><short-variant>`（例如：`3.13t`, `3.12.0d`）
- `<version>+<variant>`（例如：`3.13+freethreaded`, `3.12.0+debug`）
- `<implementation>`（例如：`cpython` 或 `cp`）
- `<implementation>@<version>`（例如：`cpython@3.12`）
- `<implementation><version>`（例如：`cpython3.12` 或 `cp312`）
- `<implementation><version-specifier>`（例如：`cpython>=3.12,<3.13`）
- `<implementation>-<version>-<os>-<arch>-<libc>`（例如：`cpython-3.12.3-macos-aarch64-none`）

此外，可以通过以下方式请求特定的系统 Python 解释器：

- `<executable-path>`（例如：`/opt/homebrew/bin/python3`）
- `<executable-name>`（例如：`mypython3`）
- `<install-dir>`（例如：`/some/environment/`）

默认情况下，如果在系统上找不到 Python 版本，uv 将自动下载它们。此行为可以通过 [`python-downloads` 选项](#禁用自动-python-下载)来禁用。

### Python 版本文件

`.python-version` 文件可用于创建默认的 Python 版本请求。uv 在工作目录及其每个父目录中搜索 `.python-version` 文件。如果未找到，uv 将检查用户级配置目录。可以使用上述任何请求格式，但为了与其他工具互操作，建议使用版本号。

可以使用 [`uv python pin`](../reference/cli.md/#uv-python-pin) 命令在当前目录创建 `.python-version` 文件。

可以使用 [`uv python pin --global`](../reference/cli.md/#uv-python-pin) 命令在用户配置目录中创建全局 `.python-version` 文件。

可以使用 `--no-config` 禁用对 `.python-version` 文件的发现。

uv 不会跨越项目或工作区边界（用户配置目录除外）搜索 `.python-version` 文件。

## 安装 Python 版本

uv 捆绑了一份可下载的 CPython 和 PyPy 发行版列表，适用于 macOS、Linux 和 Windows。

!!! tip

    默认情况下，Python 版本会在需要时自动下载，而无需使用 `uv python install`。

要安装特定版本的 Python 版本：

```console
$ uv python install 3.12.3
```

要安装最新的补丁版本：

```console
$ uv python install 3.12
```

要安装满足约束条件的版本：

```console
$ uv python install '>=3.8,<3.10'
```

要安装多个版本：

```console
$ uv python install 3.9 3.10 3.11
```

要安装特定的实现：

```console
$ uv python install pypy
```

所有 [Python 版本请求](#请求版本) 格式都受支持，除了那些用于请求本地解释器的格式（如文件路径）。

默认情况下，`uv python install` 将验证是否安装了托管的 Python 版本，或者安装最新版本。如果存在 `.python-version` 文件，uv 将安装该文件中列出的 Python 版本。需要多个 Python 版本的项目可以定义一个 `.python-versions` 文件。如果存在，uv 将安装该文件中列出的所有 Python 版本。

!!! important

    可用的 Python 版本在每个 uv 发布版本中是固定的。要安装新的 Python 版本，您可能需要升级 uv。

有关已安装 Python 版本存储位置的详细信息，请参阅[存储文档](../reference/storage.md#python-versions)。

### 安装 Python 可执行文件

uv 默认将 Python 可执行文件安装到您的 `PATH` 中，例如，在 Unix 上，`uv python install 3.12` 将把一个 Python 可执行文件安装到 `~/.local/bin`，例如 `python3.12`。有关目标目录的更多详细信息，请参阅[存储文档](../reference/storage.md#python-executables)。

!!! tip

    如果 `~/.local/bin` 不在您的 `PATH` 中，您可以使用 `uv tool update-shell` 添加它。

要安装 `python` 和 `python3` 可执行文件，请包含实验性的 `--default` 选项：

```console
$ uv python install 3.12 --default
```

在安装 Python 可执行文件时，uv 仅当现有可执行文件由 uv 管理时才会覆盖它——例如，如果 `~/.local/bin/python3.12` 已存在，没有 `--force` 标志，uv 将不会覆盖它。

uv 会更新其管理的可执行文件。但是，默认情况下，它会优先选择每个 Python 次要版本的最新补丁版本。例如：

```console
$ uv python install 3.12.7  # 添加 `python3.12` 到 `~/.local/bin`
$ uv python install 3.12.6  # 不更新 `python3.12`
$ uv python install 3.12.8  # 将 `python3.12` 更新为指向 3.12.8
```

## 升级 Python 版本

!!! important

    对升级 Python 版本的支持处于*预览*阶段。这意味着该行为是实验性的，可能会发生变化。

    升级仅支持 uv 托管的 Python 版本。

    目前不支持升级 PyPy 和 GraalPy。

uv 允许透明地将 Python 版本升级到最新的补丁版本，例如，从 3.13.4 升级到 3.13.5。uv 不允许透明地跨次要 Python 版本升级，例如从 3.12 升级到 3.13，因为更改次要版本可能会影响依赖项解析。

可以使用 `python upgrade` 命令将 uv 托管的 Python 版本升级到最新的受支持补丁版本：

要将 Python 版本升级到最新的受支持补丁版本：

```console
$ uv python upgrade 3.12
```

要升级所有已安装的 Python 版本：

```console
$ uv python upgrade
```

升级后，uv 将优先使用新版本，但会保留现有版本，因为它可能仍被虚拟环境使用。

如果 Python 版本是在启用了 `python-upgrade` [预览功能](./preview.md)的情况下安装的，例如 `uv python install 3.12 --preview-features python-upgrade`，则使用该 Python 版本的虚拟环境将自动升级到新的补丁版本。

!!! note

    如果在选择加入预览模式*之前*创建了虚拟环境，则它不会被包含在自动升级中。

如果虚拟环境是使用明确请求的补丁版本创建的，例如 `uv venv -p 3.10.8`，则它不会被透明地升级到新版本。

### 次要版本目录

虚拟环境的自动升级是通过使用 Python 次要版本的目录实现的，例如：

```
~/.local/share/uv/python/cpython-3.12-macos-aarch64-none
```

这是一个指向特定补丁版本的符号链接（在 Unix 上）或交接点（在 Windows 上）：

```console
$ readlink ~/.local/share/uv/python/cpython-3.12-macos-aarch64-none
~/.local/share/uv/python/cpython-3.12.11-macos-aarch64-none
```

如果此链接被其他工具解析（例如，通过规范化 Python 解释器路径）并用于创建虚拟环境，则它不会被自动升级。

## 项目 Python 版本

在项目命令调用期间，uv 将遵循 `pyproject.toml` 文件中 `requires-python` 定义的 Python 要求。将使用第一个符合要求的 Python 版本，除非通过其他方式（例如通过 `.python-version` 文件或 `--python` 标志）请求了特定版本。

## 查看可用的 Python 版本

要列出已安装和可用的 Python 版本：

```console
$ uv python list
```

要过滤 Python 版本，请提供一个请求，例如，显示所有 Python 3.13 解释器：

```console
$ uv python list 3.13
```

或者，显示所有 PyPy 解释器：

```console
$ uv python list pypy
```

默认情况下，会隐藏其他平台和旧补丁版本的下载项。

要查看所有版本：

```console
$ uv python list --all-versions
```

要查看其他平台的 Python 版本：

```console
$ uv python list --all-platforms
```

要排除下载项，仅显示已安装的 Python 版本：

```console
$ uv python list --only-installed
```

有关更多详细信息，请参阅 [`uv python list`](../reference/cli.md#uv-python-list) 参考。

## 查找 Python 可执行文件

要查找 Python 可执行文件，请使用 `uv python find` 命令：

```console
$ uv python find
```

默认情况下，这将显示第一个可用的 Python 可执行文件的路径。有关如何发现可执行文件的详细信息，请参阅[发现规则](#发现-python-版本)。

此接口还支持许多[请求格式](#请求版本)，例如，查找版本为 3.11 或更高版本的 Python 可执行文件：

```console
$ uv python find '>=3.11'
```

默认情况下，`uv python find` 将包含来自虚拟环境的 Python 版本。如果在工作目录或任何父目录中找到 `.venv` 目录，或者设置了 `VIRTUAL_ENV` 环境变量，它将优先于 `PATH` 上的任何 Python 可执行文件。

要忽略虚拟环境，请使用 `--system` 标志：

```console
$ uv python find --system
```

## 发现 Python 版本

搜索 Python 版本时，会检查以下位置：

- `UV_PYTHON_INSTALL_DIR` 中的托管 Python 安装。
- `PATH` 上名为 `python`、`python3` 或 `python3.x`（在 macOS 和 Linux 上）或 `python.exe`（在 Windows 上）的 Python 解释器。
- 在 Windows 上，Windows 注册表中的 Python 解释器和 Microsoft Store Python 解释器（参见 `py --list-paths`）中与请求版本匹配的解释器。

在某些情况下，uv 允许使用来自虚拟环境的 Python 版本。在这种情况下，将在按照上述描述搜索安装之前，检查虚拟环境的解释器是否与请求兼容。有关详细信息，请参阅 [pip 兼容的虚拟环境发现](../pip/environments.md#discovery-of-python-environments) 文档。

在执行发现时，将忽略不可执行的文件。每个发现的解释器都会被查询元数据，以确保其满足[请求的 Python 版本](#请求版本)。如果查询失败，将跳过该解释器。如果解释器满足请求，则使用它而不再检查其他解释器。

在搜索托管的 Python 版本时，uv 会优先选择较新的版本。在搜索系统 Python 版本时，uv 将使用第一个兼容的版本——而不是最新的版本。

如果在系统上找不到 Python 版本，uv 将检查是否有兼容的托管 Python 版本可供下载。

## Python 预发布版本

默认情况下不会选择 Python 预发布版本。如果没有其他可用的安装匹配请求，则将使用 Python 预发布版本。例如，如果只有预发布版本可用，则将使用它，否则将使用稳定发布版本。类似地，如果提供了预发布 Python 可执行文件的路径，并且没有其他 Python 版本匹配该请求，则将使用预发布版本。

如果有可用的预发布 Python 版本且匹配请求，uv 不会转而下载稳定的 Python 版本。

## 自由线程 Python

uv 支持在 CPython 3.13+ 中发现和安装[自由线程](https://docs.python.org/3.14/glossary.html#term-free-threading) Python 变体。

默认情况下不会选择自由线程 Python 版本。仅当明确请求时，例如使用 `3.13t` 或 `3.13+freethreaded`，才会选择自由线程 Python 版本。

## 调试 Python 变体

uv 支持发现和安装 Python 的[调试版本](https://docs.python.org/3.14/using/configure.html#debug-build)，即启用了调试断言。

!!! important

    Python 的调试版本速度较慢，不适合一般用途。

如果没有其他可用的安装匹配请求，则将使用调试版本。例如，如果只有调试版本可用，则将使用它，否则将使用稳定发布版本。类似地，如果提供了调试 Python 可执行文件的路径，并且没有其他 Python 版本匹配该请求，则将使用调试版本。

可以使用例如 `3.13d` 或 `3.13+debug` 明确请求 Python 的调试版本。

!!! note

    由 uv 安装的 CPython 版本通常会剥离调试符号以减小分发大小。这些调试版本没有剥离调试符号，这在用 C 级调试器调试 Python 进程时可能很有用。

## 禁用自动 Python 下载

默认情况下，uv 会在需要时自动下载 Python 版本。

可以使用 [`python-downloads`](../reference/settings.md#python-downloads) 选项禁用此行为。默认情况下，它设置为 `automatic`；设置为 `manual` 以仅允许在 `uv python install` 期间下载 Python。

!!! tip

    `python-downloads` 设置可以在[持久性配置文件](./configuration-files.md)中设置以更改默认行为，或者可以将 `--no-python-downloads` 标志传递给任何 uv 命令。

## 要求或禁用托管的 Python 版本

默认情况下，uv 将尝试使用系统上找到的 Python 版本，仅在必要时下载托管的 Python 版本。要忽略系统 Python 版本，并仅使用托管的 Python 版本，请使用 `--managed-python` 标志：

```console
$ uv python list --managed-python
```

类似地，要忽略托管的 Python 版本并仅使用系统 Python 版本，请使用 `--no-managed-python` 标志：

```console
$ uv python list --no-managed-python
```

要在配置文件中更改 uv 的默认行为，请使用 [`python-preference` 设置](#调整-python-版本偏好)。

## 调整 Python 版本偏好

[`python-preference`](../reference/settings.md#python-preference) 设置决定是优先使用系统上已有的 Python 安装，还是优先使用由 uv 下载和安装的 Python 安装。

默认情况下，`python-preference` 设置为 `managed`，它优先选择托管的 Python 安装而不是系统的 Python 安装。但是，系统的 Python 安装仍然优先于下载托管的 Python 版本。

以下替代选项可用：

- `only-managed`：仅使用托管的 Python 安装；绝不使用系统的 Python 安装。等同于 `--managed-python`。
- `system`：优先选择系统的 Python 安装而不是托管的 Python 安装。
- `only-system`：仅使用系统的 Python 安装；绝不使用托管的 Python 安装。等同于 `--no-managed-python`。

!!! note

    可以在不更改偏好的情况下[禁用](#禁用自动-python-下载)自动 Python 版本下载。

## Python 实现支持

uv 支持 CPython、PyPy、Pyodide 和 GraalPy Python 实现。如果某个 Python 实现不受支持，uv 将无法发现其解释器。

可以使用长名称或短名称请求实现：

- CPython: `cpython`, `cp`
- PyPy: `pypy`, `pp`
- GraalPy: `graalpy`, `gp`
- Pyodide: `pyodide`

实现名称的请求不区分大小写。

有关支持的格式的更多详细信息，请参阅 [Python 版本请求](#请求版本) 文档。

## 托管的 Python 发行版

uv 支持下载和安装 CPython、PyPy 和 Pyodide 发行版。

### CPython 发行版

由于 Python 不发布官方的可分发 CPython 二进制文件，uv 转而使用来自 Astral [`python-build-standalone`](https://github.com/astral-sh/python-build-standalone) 项目的预构建发行版。`python-build-standalone` 也被许多其他 Python 项目使用，例如 [Mise](https://mise.jdx.dev/lang/python.html) 和 [bazelbuild/rules_python](https://github.com/bazelbuild/rules_python)。

uv 的 Python 发行版是自包含的、高度可移植且高性能的。虽然可以像 `pyenv` 等工具一样从源代码构建 Python，但这样做需要预先安装系统依赖项，并且创建优化的、高性能的构建（例如，启用 PGO 和 LTO）非常缓慢。

这些发行版存在一些行为上的怪癖，通常是出于可移植性的考虑；有关详细信息，请参阅 [`python-build-standalone` 怪癖](https://gregoryszorc.com/docs/python-build-standalone/main/quirks.html) 文档。

### PyPy 发行版

PyPy 发行版由 [PyPy 项目](https://pypy.org) 提供。

### Pyodide 发行版

Pyodide 发行版由 [Pyodide 项目](https://github.com/pyodide/pyodide) 提供。

Pyodide 是 CPython 针对 WebAssembly / Emscripten 平台的移植版本。

## 在 aarch64 上透明的 x86_64 仿真

macOS 和 Windows 都支持通过透明仿真在 aarch64 上运行 x86_64 二进制文件。这被称为 [Rosetta 2](https://support.apple.com/en-gb/102527) 或 [Windows on ARM (WoA) emulation](https://learn.microsoft.com/en-us/windows/arm/apps-on-arm-x86-emulation)。可以在 aarch64 上使用 x86_64 的 uv，也可以在 aarch64 上使用 x86_64 的 Python 解释器。任一 uv 二进制文件都可以使用任一 Python 解释器，但 Python 解释器需要与其架构（全是 x86_64 或全是 aarch64）对应的包。

## 在 Windows 注册表中的注册

在 Windows 上，安装托管的 Python 版本会将它们在 Windows 注册表中注册，遵循 [PEP 514](https://peps.python.org/pep-0514/) 的定义。

安装后，可以使用 `py` 启动器选择 Python 版本，例如：

```console
$ uv python install 3.13.1
$ py -V:Astral/CPython3.13.1
```

在卸载时，uv 将移除目标版本的注册表项以及任何损坏的注册表项。