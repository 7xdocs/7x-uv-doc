---
title: 项目工作流程
description:
  A guide to using uv to create and manage Python projects, including adding dependencies, running
  commands, and building publishable distributions.
---

# 项目工作流程

uv 支持管理 Python 项目，这些项目在 `pyproject.toml` 文件中定义其依赖关系。

## 创建新项目

你可以使用 `uv init` 命令创建一个新的 Python 项目：

```console
$ uv init hello-world
$ cd hello-world
```

或者，你可以在工作目录中初始化一个项目：

```console
$ mkdir hello-world
$ cd hello-world
$ uv init
```

uv 将创建以下文件：

```text
├── .gitignore
├── .python-version
├── README.md
├── main.py
└── pyproject.toml
```

`main.py` 文件包含一个简单的 "Hello world" 程序。使用 `uv run` 尝试运行它：

```console
$ uv run main.py
Hello from hello-world!
```

## 项目结构

一个项目由几个重要的部分组成，它们协同工作，使 uv 能够管理你的项目。
除了 `uv init` 创建的文件外，uv 会在你首次运行项目命令（即 `uv run`、`uv sync` 或 `uv lock`）时，在你的项目根目录中创建一个虚拟环境和 `uv.lock` 文件。

完整的列表如下所示：

```text
.
├── .venv
│   ├── bin
│   ├── lib
│   └── pyvenv.cfg
├── .python-version
├── README.md
├── main.py
├── pyproject.toml
└── uv.lock
```

### `pyproject.toml`

`pyproject.toml` 包含关于你项目的元数据：

```toml title="pyproject.toml"
[project]
name = "hello-world"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
dependencies = []
```

你将使用此文件来指定依赖项，以及项目的详细信息，例如其描述或许可证。你可以手动编辑此文件，或使用诸如 `uv add` 和 `uv remove` 之类的命令从终端管理你的项目。

!!! tip

    有关 `pyproject.toml` 格式入门的更多详细信息，请参阅官方的 [`pyproject.toml` 指南](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/)。

你还将使用此文件在 [`[tool.uv]`](../reference/settings.md) 部分中指定 uv [配置选项](../concepts/configuration-files.md)。

### `.python-version`

`.python-version` 文件包含项目的默认 Python 版本。此文件告诉 uv 在创建项目的虚拟环境时使用哪个 Python 版本。

### `.venv`

`.venv` 文件夹包含你项目的虚拟环境，这是一个与系统其余部分隔离的 Python 环境。这是 uv 安装你项目依赖项的地方。

有关更多详细信息，请参阅 [项目环境](../concepts/projects/layout.md#the-project-environment) 文档。

### `uv.lock`

`uv.lock` 是一个跨平台锁文件，包含关于你项目依赖项的确切信息。与用于指定项目广泛需求的 `pyproject.toml` 不同，锁文件包含安装在项目环境中的确切已解析版本。此文件应检入版本控制系统，以便在不同机器上实现一致且可复现的安装。

`uv.lock` 是一个人类可读的 TOML 文件，但由 uv 管理，不应手动编辑。

有关更多详细信息，请参阅 [锁文件](../concepts/projects/layout.md#the-lockfile) 文档。

## 管理依赖项

你可以使用 `uv add` 命令向你的 `pyproject.toml` 添加依赖项。这也会更新锁文件和项目环境：

```console
$ uv add requests
```

你也可以指定版本约束或替代来源：

```console
$ # 指定版本约束
$ uv add 'requests==2.31.0'

$ # 添加一个 git 依赖
$ uv add git+https://github.com/psf/requests
```

如果你正在从 `requirements.txt` 文件迁移，你可以使用 `uv add` 和 `-r` 标志来添加文件中的所有依赖项：

```console
$ # 从 `requirements.txt` 添加所有依赖项。
$ uv add -r requirements.txt -c constraints.txt
```

要移除一个包，你可以使用 `uv remove`：

```console
$ uv remove requests
```

要升级一个包，使用 `--upgrade-package` 标志运行 `uv lock`：

```console
$ uv lock --upgrade-package requests
```

`--upgrade-package` 标志将尝试将指定的包更新到最新的兼容版本，同时保持锁文件的其余部分不变。

有关更多详细信息，请参阅关于 [管理依赖项](../concepts/projects/dependencies.md) 的文档。

## 查看版本

`uv version` 命令可用于读取你包的版本。

要获取你包的版本，运行 `uv version`：

```console
$ uv version
hello-world 0.7.0
```

要获取不带包名的版本，使用 `--short` 选项：

```console
$ uv version --short
0.7.0
```

要以 JSON 格式获取版本信息，使用 `--output-format json` 选项：

```console
$ uv version --output-format json
{
    "package_name": "hello-world",
    "version": "0.7.0",
    "commit_info": null
}
```

有关更新你包版本的详细信息，请参阅 [发布指南](./package.md#updating-your-version)。

## 运行命令

`uv run` 可用于在你的项目环境中运行任意脚本或命令。

在每次调用 `uv run` 之前，uv 将验证锁文件是否与 `pyproject.toml` 保持最新，并且环境是否与锁文件保持最新，从而使你的项目保持同步而无需手动干预。`uv run` 保证你的命令在一致、锁定的环境中运行。

例如，使用 `flask`：

```console
$ uv add flask
$ uv run -- flask run -p 3000
```

或者，运行一个脚本：

```python title="example.py"
# Require a project dependency
import flask

print("hello world")
```

```console
$ uv run example.py
```

或者，你可以使用 `uv sync` 手动更新环境，然后在执行命令之前激活它：

=== "macOS and Linux"

    ```console
    $ uv sync
    $ source .venv/bin/activate
    $ flask run -p 3000
    $ python example.py
    ```

=== "Windows"

    ```pwsh-session
    PS> uv sync
    PS> .venv\Scripts\activate
    PS> flask run -p 3000
    PS> python example.py
    ```

!!! note

    必须激活虚拟环境才能在没有 `uv run` 的情况下在项目中运行脚本和命令。虚拟环境的激活方式因 shell 和平台而异。

有关更多详细信息，请参阅关于在项目中 [运行命令和脚本](../concepts/projects/run.md) 的文档。

## 构建分发包

`uv build` 可用于为你的项目构建源码分发包和二进制分发包（wheel）。

默认情况下，`uv build` 将在当前目录中构建项目，并将构建的产物放置在 `dist/` 子目录中：

```console
$ uv build
$ ls dist/
hello-world-0.1.0-py3-none-any.whl
hello-world-0.1.0.tar.gz
```

有关更多详细信息，请参阅关于 [构建项目](../concepts/projects/build.md) 的文档。

## 后续步骤

要了解更多关于使用 uv 进行项目工作的信息，请参阅 [项目概念](../concepts/projects/index.md) 页面和 [命令参考](../reference/cli.md#uv)。

或者，继续阅读以了解如何 [构建项目并将其发布到包索引](./package.md)。
