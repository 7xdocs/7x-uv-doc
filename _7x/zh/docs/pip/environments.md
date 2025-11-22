# 使用 Python 环境

每个 Python 安装都有一个环境，当使用 Python 时该环境处于活动状态。可以将包安装到环境中，以便从 Python 脚本中使用它们的模块。通常，最佳实践是不修改 Python 安装的环境。这对于操作系统附带的 Python 安装尤其重要，因为它们通常自行管理包。虚拟环境是一种将包与 Python 安装环境隔离开的轻量级方法。与 `pip` 不同，uv 默认要求使用虚拟环境。

## 创建虚拟环境

uv 支持创建虚拟环境，例如，要在 `.venv` 处创建虚拟环境：

```console
$ uv venv
```

可以指定特定的名称或路径，例如，要在 `my-name` 处创建虚拟环境：

```console
$ uv venv my-name
```

可以请求特定的 Python 版本，例如，要创建带有 Python 3.11 的虚拟环境：

```console
$ uv venv --python 3.11
```

请注意，这要求系统上已安装所请求的 Python 版本。但是，如果不可用，uv 将为您下载 Python。有关更多详细信息，请参阅 [Python 版本](../concepts/python-versions.md) 文档。

## 使用虚拟环境

当使用默认的虚拟环境名称时，uv 将在后续调用中自动找到并使用该虚拟环境。

```console
$ uv venv

$ # 在新的虚拟环境中安装一个包
$ uv pip install ruff
```

可以"激活"虚拟环境以使其中的包可用：

=== "macOS and Linux"

    ```console
    $ source .venv/bin/activate
    ```

=== "Windows"

    ```pwsh-session
    PS> .venv\Scripts\activate
    ```

!!! note

    Unix 上的默认激活脚本适用于符合 POSIX 标准的 shell，例如 `sh`、`bash` 或 `zsh`。
    对于常见的替代 shell，还有额外的激活脚本。

    === "fish"

        ```console
        $ source .venv/bin/activate.fish
        ```

    === "csh / tcsh"


        ```console
        $ source .venv/bin/activate.csh
        ```

    === "Nushell"

        ```console
        $ use .venv\Scripts\activate.nu
        ```

## 停用环境

要退出虚拟环境，请使用 `deactivate` 命令：

```console
$ deactivate
```

## 使用任意的 Python 环境

由于 uv 不依赖于 Python，它可以安装到自身环境之外的虚拟环境中。例如，设置 `VIRTUAL_ENV=/path/to/venv` 将导致 uv 安装到 `/path/to/venv`，无论 uv 自身安装在哪里。请注意，如果 `VIRTUAL_ENV` 被设置为一个**不是** [PEP 405 兼容](https://peps.python.org/pep-0405/#specification)的虚拟环境的目录，它将被忽略。

uv 也可以通过提供给 `uv pip sync` 或 `uv pip install` 的 `--python` 参数安装到任意的、甚至是非虚拟的环境中。例如，`uv pip install --python /path/to/python` 将安装到链接到 `/path/to/python` 解释器的环境中。

为方便起见，`uv pip install --system` 将安装到系统的 Python 环境中。使用 `--system` 大致相当于 `uv pip install --python $(which python)`，但请注意，链接到虚拟环境的可执行文件将被跳过。虽然我们通常推荐使用虚拟环境进行依赖管理，但 `--system` 在持续集成和容器化环境中是合适的。

`--system` 标志也用于选择加入对系统环境的修改。例如，`--python` 参数可用于请求一个 Python 版本（例如 `--python 3.12`），uv 将搜索满足该请求的解释器。如果 uv 找到一个系统解释器（例如 `/usr/lib/python3.12`），则需要 `--system` 标志来允许修改这个非虚拟的 Python 环境。没有 `--system` 标志，uv 将忽略任何不在虚拟环境中的解释器。相反，当提供了 `--system` 标志时，uv 将忽略任何*在*虚拟环境中的解释器。

跨平台和发行版在系统 Python 中安装包是出了名的困难。uv 支持常见的情况，但并非在所有情况下都有效。例如，由于[发行版对 `distutils`（而非 `sysconfig`）的补丁](https://ffy00.github.io/blog/02-python-debian-and-the-install-locations/)，在 Python 3.10 之前的 Debian 系统上安装到系统 Python 是不受支持的。虽然我们始终推荐使用虚拟环境，但在这些非标准环境中，uv 认为它们是必需的。

如果 uv 安装在某个 Python 环境中（例如，通过 `pip` 安装），它仍然可以用来修改其他环境。但是，当通过 `python -m uv` 调用时，uv 将默认使用父解释器的环境。通过 Python 调用 uv 会增加启动开销，不推荐在常规使用中使用。

uv 本身不依赖于 Python，但它需要定位一个 Python 环境来（1）将依赖安装到该环境中，以及（2）构建源码发行版。

## Python 环境的发现

当运行会改变环境的命令（如 `uv pip sync` 或 `uv pip install`）时，uv 将按以下顺序搜索虚拟环境：

-   基于 `VIRTUAL_ENV` 环境变量激活的虚拟环境。
-   基于 `CONDA_PREFIX` 环境变量激活的 Conda 环境。
-   当前目录或最近父目录中 `.venv` 处的虚拟环境。

如果未找到虚拟环境，uv 将提示用户通过 `uv venv` 在当前目录创建一个。

如果包含了 `--system` 标志，uv 将跳过虚拟环境，搜索已安装的 Python 版本。类似地，当运行不改变环境的命令（如 `uv pip compile`）时，uv 不*要求*虚拟环境——但是，仍然需要 Python 解释器。有关发现已安装 Python 版本的详细信息，请参阅 [Python 发现](../concepts/python-versions.md#discovery-of-python-versions) 的文档。