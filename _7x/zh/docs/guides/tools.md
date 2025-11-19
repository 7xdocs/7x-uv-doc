---
title: 使用工具
description:
  关于使用 uv 运行作为 Python 包发布的工具的指南，包括使用 uvx 进行一次性调用、请求特定工具版本、安装工具、升级工具等。
---

# 使用工具

许多 Python 包提供了可用作工具的应用程序。uv 具有专门的支持，可以轻松调用和安装这些工具。

## 运行工具

`uvx` 命令无需安装即可调用工具。

例如，要运行 `ruff`：

```console
$ uvx ruff
```

!!! note

    这完全等同于：

    ```console
    $ uv tool run ruff
    ```

    为方便起见，提供了 `uvx` 作为别名。

参数可以在工具名称后提供：

```console
$ uvx pycowsay hello from uv

  -------------
< hello from uv >
  -------------
   \   ^__^
    \  (oo)\_______
       (__)\       )\/\
           ||----w |
           ||     ||

```

使用 `uvx` 时，工具会被安装到临时的、隔离的环境中。

!!! note

    如果您在 [_项目_](../concepts/projects/index.md) 中运行工具，并且该工具要求安装您的项目（例如，使用 `pytest` 或 `mypy` 时），您应该使用 [`uv run`](./projects.md#running-commands) 而不是 `uvx`。否则，该工具将在与您的项目隔离的虚拟环境中运行。

    如果您的项目结构是扁平的（例如，没有使用 `src` 目录来存放模块），那么项目本身不需要安装，使用 `uvx` 即可。在这种情况下，只有当您希望在项目的依赖项中固定工具的版本时，使用 `uv run` 才有额外的好处。

## 命令与包名不同的情况

当调用 `uvx ruff` 时，uv 会安装提供 `ruff` 命令的 `ruff` 包。但有时包的名称和命令的名称并不相同。

可以使用 `--from` 选项来调用特定包中的命令，例如，由 `httpie` 包提供的 `http` 命令：

```console
$ uvx --from httpie http
```

## 请求特定版本

要运行特定版本的工具，请使用 `command@<version>`：

```console
$ uvx ruff@0.3.0 check
```

要运行工具的最新版本，请使用 `command@latest`：

```console
$ uvx ruff@latest check
```

`--from` 选项也可用于指定包版本，如上所述：

```console
$ uvx --from 'ruff==0.3.0' ruff check
```

或者，也可以约束版本范围：

```console
$ uvx --from 'ruff>0.2.0,<0.3.0' ruff check
```

请注意，`@` 语法不能用于除精确版本之外的任何其他用途。

## 请求附加功能

可以使用 `--from` 选项来运行带有附加功能的工具：

```console
$ uvx --from 'mypy[faster-cache,reports]' mypy --xml-report mypy_report
```

这也可以与版本选择结合使用：

```console
$ uvx --from 'mypy[faster-cache,reports]==1.13.0' mypy --xml-report mypy_report
```

## 请求不同的来源

`--from` 选项也可用于从替代来源安装。

例如，从 git 拉取：

```console
$ uvx --from git+https://github.com/httpie/cli httpie
```

您也可以从特定的命名分支拉取最新提交：

```console
$ uvx --from git+https://github.com/httpie/cli@master httpie
```

或者拉取特定的标签：

```console
$ uvx --from git+https://github.com/httpie/cli@3.2.4 httpie
```

甚至是特定的提交：

```console
$ uvx --from git+https://github.com/httpie/cli@2843b87 httpie
```

## 带有插件的命令

可以包含额外的依赖项，例如，在运行 `mkdocs` 时包含 `mkdocs-material`：

```console
$ uvx --with mkdocs-material mkdocs --help
```

## 安装工具

如果一个工具经常使用，将其安装到持久环境中并添加到 `PATH` 中，而不是重复调用 `uvx`，会很有用。

!!! tip

    `uvx` 是 `uv tool run` 的一个便捷别名。所有其他与工具交互的命令都需要完整的 `uv tool` 前缀。

要安装 `ruff`：

```console
$ uv tool install ruff
```

当工具被安装后，其可执行文件会被放置在一个位于 `PATH` 中的 `bin` 目录下，这使得无需 uv 即可运行该工具。如果它不在 `PATH` 中，将会显示警告，并且可以使用 `uv tool update-shell` 将其添加到 `PATH` 中。

安装 `ruff` 后，它应该就可以使用了：

```console
$ ruff --version
```

与 `uv pip install` 不同，安装工具并不会使其模块在当前环境中可用。例如，以下命令将会失败：

```console
$ python -c "import ruff"
```

这种隔离对于减少工具、脚本和项目的依赖项之间的交互和冲突非常重要。

与 `uvx` 不同，`uv tool install` 操作的是一个 _包_，并且会安装该工具提供的所有可执行文件。

例如，以下命令将安装 `http`、`https` 和 `httpie` 可执行文件：

```console
$ uv tool install httpie
```

此外，可以在不使用 `--from` 的情况下包含包版本：

```console
$ uv tool install 'httpie>0.1.0'
```

同样，对于包来源也是如此：

```console
$ uv tool install git+https://github.com/httpie/cli
```

与 `uvx` 一样，安装可以包含额外的包：

```console
$ uv tool install mkdocs --with mkdocs-material
```

可以使用 `--with-executables-from` 标志将多个相关的可执行文件一起安装到同一个工具环境中。例如，以下命令将安装来自 `ansible` 的可执行文件，以及由 `ansible-core` 和 `ansible-lint` 提供的可执行文件：

```console
$ uv tool install --with-executables-from ansible-core,ansible-lint ansible
```

## 升级工具

要升级工具，请使用 `uv tool upgrade`：

```console
$ uv tool upgrade ruff
```

工具升级将遵循安装工具时提供的版本约束。例如，`uv tool install ruff >=0.3,<0.4` 后跟 `uv tool upgrade ruff` 将会将 Ruff 升级到 `>=0.3,<0.4` 范围内的最新版本。

要替换版本约束，请使用 `uv tool install` 重新安装工具：

```console
$ uv tool install ruff>=0.4
```

要升级所有工具：

```console
$ uv tool upgrade --all
```

## 请求 Python 版本

默认情况下，uv 在运行、安装或升级工具时将使用您的默认 Python 解释器（它找到的第一个）。您可以使用 `--python` 选项指定要使用的 Python 解释器。

例如，在运行工具时请求特定的 Python 版本：

```console
$ uvx --python 3.10 ruff
```

或者，在安装工具时：

```console
$ uv tool install --python 3.10 ruff
```

或者，在升级工具时：

```console
$ uv tool upgrade --python 3.10 ruff
```

有关请求 Python 版本的更多详细信息，请参阅 [Python 版本](../concepts/python-versions.md#requesting-a-version) 概念页面。

## 旧版 Windows 脚本

工具还支持运行 [旧版 setuptools 脚本](https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools/#scripts)。这些脚本在安装后可以通过 `$(uv tool dir)\<tool-name>\Scripts` 使用。

目前仅支持具有 `.ps1`、`.cmd` 和 `.bat` 扩展名的旧版脚本。

例如，下面是一个运行命令提示符脚本的示例。

```console
$ uv tool run --from nuitka==2.6.7 nuitka.cmd --version
```

此外，您不需要指定扩展名。`uvx` 将自动按执行顺序（`.ps1`、`.cmd`、`.bat`）为您查找以这些扩展名结尾的文件。

```console
$ uv tool run --from nuitka==2.6.7 nuitka --version
```

## 下一步

要了解有关使用 uv 管理工具的更多信息，请参阅 [工具概念](../concepts/tools.md) 页面和 [命令参考](../reference/cli.md#uv-tool)。

或者，继续阅读以了解如何 [处理项目](./projects.md)。