# Tools

Tools 是提供命令行接口的 Python 包。

!!! note

    关于如何使用 tools 接口的介绍，请参阅 [tools 指南](../guides/tools.md) —— 本文档讨论工具管理的细节。

## `uv tool` 接口

uv 包含一个专门的接口用于与工具交互。可以使用 `uv tool run` 在不安装工具的情况下调用它们，这种情况下，它们的依赖项会被安装在一个临时的虚拟环境中，该环境与当前项目隔离。

因为在不安装的情况下运行工具非常常见，所以提供了一个 `uvx` 别名来代替 `uv tool run` —— 这两个命令完全等效。为简洁起见，文档将主要引用 `uvx` 而不是 `uv tool run`。

工具也可以使用 `uv tool install` 安装，这种情况下，它们的可执行文件将 [在 `PATH` 上可用](#the-path) —— 仍然使用隔离的虚拟环境，但该环境在命令完成后不会被移除。

## 执行 vs 安装

在大多数情况下，使用 `uvx` 执行工具比安装工具更合适。安装工具在你需要该工具对系统上的其他程序可用时很有用，例如，如果你不控制的某个脚本需要该工具，或者如果你在 Docker 镜像中并希望让用户可以使用该工具。

## 工具环境

当使用 `uvx` 运行工具时，一个虚拟环境被存储在 uv 缓存目录中，并被视作可丢弃的，即，如果你运行 `uv cache clean`，该环境将被删除。该环境仅被缓存以减少重复调用的开销。如果环境被移除，一个新的环境将自动创建。

当使用 `uv tool install` 安装工具时，一个虚拟环境被创建在 [uv 工具目录](../reference/storage.md#tools) 中。除非工具被卸载，否则该环境不会被移除。如果环境被手动删除，工具将无法运行。

!!! important

    工具环境 _不_ 旨在被直接修改。强烈建议永远不要手动修改工具环境，例如，通过 `pip` 操作。

## 工具版本

除非请求特定版本，否则 `uv tool install` 将安装所请求工具的最新可用版本。`uvx` 将在 _第一次调用时_ 使用所请求工具的最新可用版本。之后，`uvx` 将使用工具的缓存版本，除非请求了不同的版本、缓存被清理或缓存被刷新。

例如，要运行特定版本的 Ruff：

```console
$ uvx ruff@0.6.0 --version
ruff 0.6.0
```

后续的 `uvx` 调用将使用最新的版本，而不是缓存的版本。

```console
$ uvx ruff --version
ruff 0.6.2
```

但是，如果 Ruff 发布了新版本，除非缓存被刷新，否则不会使用新版本。

要请求 Ruff 的最新版本并刷新缓存，使用 `@latest` 后缀：

```console
$ uvx ruff@latest --version
0.6.2
```

一旦工具使用 `uv tool install` 安装，`uvx` 将默认使用已安装的版本。

例如，安装旧版本的 Ruff 后：

```console
$ uv tool install ruff==0.5.0
```

`ruff` 和 `uvx ruff` 的版本是相同的：

```console
$ ruff --version
ruff 0.5.0
$ uvx ruff --version
ruff 0.5.0
```

但是，你可以通过显式请求最新版本来忽略已安装的版本，例如：

```console
$ uvx ruff@latest --version
0.6.2
```

或者，通过使用 `--isolated` 标志，这将避免刷新缓存但忽略已安装的版本：

```console
$ uvx --isolated ruff --version
0.6.2
```

`uv tool install` 也会遵守 `{package}@{version}` 和 `{package}@latest` 说明符，如：

```console
$ uv tool install ruff@latest
$ uv tool install ruff@0.6.0
```

## 升级工具

工具环境可以通过 `uv tool upgrade` 进行升级，或者通过后续的 `uv tool install` 操作完全重新创建。

要升级工具环境中的所有包：

```console
$ uv tool upgrade black
```

要升级工具环境中的单个包：

```console
$ uv tool upgrade black --upgrade-package click
```

工具升级将遵守安装工具时提供的版本约束。例如，`uv tool install black >=23,<24` 后接 `uv tool upgrade black` 将在 `>=23,<24` 范围内将 Black 升级到最新版本。

要替换版本约束，请使用 `uv tool install` 重新安装工具：

```console
$ uv tool install black>=24
```

类似地，工具升级将保留安装工具时提供的设置。例如，`uv tool install black --prerelease allow` 后接 `uv tool upgrade black` 将保留 `--prerelease allow` 设置。

!!! note

    工具升级将重新安装工具的可执行文件，即使它们没有改变。

要在升级期间重新安装包，使用 `--reinstall` 和 `--reinstall-package` 选项。

要重新安装工具环境中的所有包：

```console
$ uv tool upgrade black --reinstall
```

要重新安装工具环境中的单个包：

```console
$ uv tool upgrade black --reinstall-package click
```

## 包含额外的依赖项

可以在工具执行期间包含额外的包：

```console
$ uvx --with <extra-package> <tool>
```

并且，在工具安装期间：

```console
$ uv tool install --with <extra-package> <tool-package>
```

`--with` 选项可以多次提供以包含多个额外的包。

`--with` 选项支持包说明符，因此可以请求特定版本：

```console
$ uvx --with <extra-package>==<version> <tool-package>
```

可以使用 `-w` 简写代替 `--with` 选项：

```console
$ uvx -w <extra-package> <tool-package>
```

如果请求的版本与工具包的要求冲突，包解析将失败，命令将报错。

## 从额外包安装可执行文件

安装工具时，你可能希望将来自额外包的可执行文件包含在同一个工具环境中。这在你有关联工具需要协同工作，或者你想要安装多个共享依赖的可执行文件时很有用。

`--with-executables-from` 选项允许你指定额外的包，它们提供的可执行文件应与主工具一起安装：

```console
$ uv tool install --with-executables-from <package1>,<package2> <tool-package>
```

例如，要安装 Ansible 以及来自 `ansible-core` 和 `ansible-lint` 的可执行文件：

```console
$ uv tool install --with-executables-from ansible-core,ansible-lint ansible
```

这将把来自 `ansible`、`ansible-core` 和 `ansible-lint` 包的所有可执行文件安装到同一个工具环境中，使它们都在 `PATH` 上可用。

`--with-executables-from` 选项可以与其他安装选项结合使用：

```console
$ uv tool install --with-executables-from ansible-core --with mkdocs-material ansible
```

注意 `--with-executables-from` 与 `--with` 的不同之处在于：

- `--with` 将额外的包作为依赖项包含，但不安装它们的可执行文件
- `--with-executables-from` 既将包作为依赖项包含，也安装它们的可执行文件

## Python 版本

每个工具环境都链接到一个特定的 Python 版本。这使用了与其他由 uv 创建的虚拟环境相同的 Python 版本 [发现逻辑](./python-versions.md#discovery-of-python-versions)，但会忽略非全局的 Python 版本请求，如 `.python-version` 文件和来自 `pyproject.toml` 的 `requires-python` 值。

`--python` 选项可用于请求特定版本。更多详情请参阅 [Python 版本](./python-versions.md) 文档。

如果工具使用的 Python 版本 _被卸载_，工具环境将被破坏，工具可能无法使用。

## 工具可执行文件

工具可执行文件包括 Python 包提供的所有控制台入口点、脚本入口点和二进制脚本。工具可执行文件在 Unix 上被符号链接到 [可执行文件目录](../reference/storage.md#tool-executables)，在 Windows 上被复制。

!!! note

    工具包的依赖项提供的可执行文件不会被安装。

[可执行文件目录](../reference/storage.md#executable-directory) 必须位于 `PATH` 环境变量中，工具可执行文件才能从 shell 中可用。如果它不在 `PATH` 中，将显示警告。`uv tool update-shell` 命令可用于将可执行文件目录添加到常见 shell 配置文件的 `PATH` 中。

### 覆盖可执行文件

安装工具不会覆盖可执行文件目录中先前不是由 uv 安装的可执行文件。例如，如果之前使用 `pipx` 安装了一个工具，`uv tool install` 将会失败。可以使用 `--force` 标志来覆盖此行为。

## 与 `uv run` 的关系

调用 `uv tool run <name>`（或 `uvx <name>`）几乎等效于：

```console
$ uv run --no-project --with <name> -- <name>
```

但是，在使用 uv 的工具接口时，有几个显著的区别：

- 不需要 `--with` 选项 —— 所需的包是从命令名称推断出来的。
- 临时环境被缓存在一个专用位置。
- 不需要 `--no-project` 标志 —— 工具总是与项目隔离运行。
- 如果工具已经安装，`uv tool run` 将使用已安装的版本，但 `uv run` 不会。

如果工具不应该与项目隔离，例如在运行 `pytest` 或 `mypy` 时，那么应该使用 `uv run` 而不是 `uv tool run`。