# 配置项目

## Python 版本要求

项目可以在 `pyproject.toml` 的 `project.requires-python` 字段中声明项目支持的 Python 版本。

建议设置 `requires-python` 值：

```toml title="pyproject.toml" hl_lines="4"
[project]
name = "example"
version = "0.1.0"
requires-python = ">=3.12"
```

Python 版本要求决定了项目中允许使用的 Python 语法，并影响依赖版本的选择（它们必须支持相同的 Python 版本范围）。

## 入口点

[入口点](https://packaging.python.org/en/latest/specifications/entry-points/#entry-points)是已安装包发布接口的官方术语。这些包括：

- [命令行接口](#命令行接口)
- [图形用户界面](#图形用户界面)
- [插件入口点](#插件入口点)

!!! important

    使用入口点表需要定义[构建系统](#构建系统)。

### 命令行接口

项目可以在 `pyproject.toml` 的 `[project.scripts]` 表中定义项目的命令行接口。

例如，声明一个名为 `hello` 的命令，该命令调用 `example` 模块中的 `hello` 函数：

```toml title="pyproject.toml"
[project.scripts]
hello = "example:hello"
```

然后，可以从控制台运行该命令：

```console
$ uv run hello
```

### 图形用户界面

项目可以在 `pyproject.toml` 的 `[project.gui-scripts]` 表中定义项目的图形用户界面。

!!! important

    这些仅在 Windows 上与[命令行接口](#命令行接口)不同，在 Windows 上它们由 GUI 可执行文件包装，因此可以在没有控制台的情况下启动。在其他平台上，它们的行为相同。

例如，声明一个名为 `hello` 的命令，该命令调用 `example` 模块中的 `app` 函数：

```toml title="pyproject.toml"
[project.gui-scripts]
hello = "example:app"
```

### 插件入口点

项目可以在 `pyproject.toml` 的 [`[project.entry-points]`](https://packaging.python.org/en/latest/guides/creating-and-discovering-plugins/#using-package-metadata) 表中定义用于插件发现的入口点。

例如，将 `example-plugin-a` 包注册为 `example` 的插件：

```toml title="pyproject.toml"
[project.entry-points.'example.plugins']
a = "example_plugin_a"
```

然后，在 `example` 中，将通过以下方式加载插件：

```python title="example/__init__.py"
from importlib.metadata import entry_points

for plugin in entry_points(group='example.plugins'):
    plugin.load()
```

!!! note

    `group` 键可以是任意值，不需要包含包名或 "plugins"。但是，建议使用包名对键进行命名空间划分，以避免与其他包发生冲突。

## 构建系统

构建系统决定了项目应如何打包和安装。项目可以在 `pyproject.toml` 的 `[build-system]` 表中声明和配置构建系统。

uv 使用构建系统的存在来确定项目是否包含应安装在项目虚拟环境中的包。如果未定义构建系统，uv 将不会尝试构建或安装项目本身，只会安装其依赖项。如果定义了构建系统，uv 将构建项目并将其安装到项目环境中。

可以向 `uv init` 提供 `--build-backend` 选项来创建具有适当布局的打包项目。可以向 `uv init` 提供 `--package` 选项来创建具有默认构建系统的打包项目。

!!! note

    虽然在没有构建系统定义的情况下，uv 不会构建和安装当前项目，但其他包中不需要存在 `[build-system]` 表。由于历史原因，如果未定义构建系统，则使用 `setuptools.build_meta:__legacy__` 来构建包。您依赖的包可能没有显式声明其构建系统，但仍然可以安装。类似地，如果您[添加对本地项目的依赖](./dependencies.md#path)或使用 `uv pip` 安装它，uv 将尝试构建和安装它，无论是否存在 `[build-system]` 表。

构建系统用于支持以下功能：

- 在发行版中包含或排除文件
- 可编辑安装行为
- 动态项目元数据
- 原生代码编译
- 供应共享库

要配置这些功能，请参阅您选择的构建系统的文档。

## 项目打包

如[构建系统](#构建系统)中所述，Python 项目必须经过构建才能安装。此过程通常称为"打包"。

如果您想执行以下操作，可能需要一个包：

- 向项目添加命令
- 将项目分发给其他人
- 使用 `src` 和 `test` 布局
- 编写库

如果您正在执行以下操作，则可能*不需要*包：

- 编写脚本
- 构建简单的应用程序
- 使用扁平布局

虽然 uv 通常使用[构建系统](#构建系统)的声明来确定是否应打包项目，但 uv 也允许使用 [`tool.uv.package`](../../reference/settings.md#package) 设置覆盖此行为。

设置 `tool.uv.package = true` 将强制构建项目并将其安装到项目环境中。如果未定义构建系统，uv 将使用 setuptools 传统后端。

设置 `tool.uv.package = false` 将强制*不*构建项目包并将其安装到项目环境中。在与项目交互时，uv 将忽略已声明的构建系统；但是，uv 仍将尊重显式尝试构建项目的操作，例如调用 `uv build`。

## 项目环境路径

`UV_PROJECT_ENVIRONMENT` 环境变量可用于配置项目虚拟环境路径（默认为 `.venv`）。

如果提供了相对路径，它将相对于工作区根目录进行解析。如果提供了绝对路径，它将按原样使用，即不会为环境创建子目录。如果提供的路径上不存在环境，uv 将创建它。

此选项可用于写入系统 Python 环境，但不推荐这样做。`uv sync` 默认会从环境中删除无关的包，因此可能会使系统处于损坏状态。

要以系统环境为目标，请将 `UV_PROJECT_ENVIRONMENT` 设置为 Python 安装的前缀。例如，在基于 Debian 的系统上，这通常是 `/usr/local`：

```console
$ python -c "import sysconfig; print(sysconfig.get_config_var('prefix'))"
/usr/local
```

要以该环境为目标，您需要导出 `UV_PROJECT_ENVIRONMENT=/usr/local`。

!!! important

    如果提供了绝对路径并且在多个项目中使用了该设置，则每个项目中的调用都将覆盖环境。此设置仅建议在 CI 或 Docker 镜像中用于单个项目。

!!! note

    默认情况下，uv 在项目操作期间不会读取 `VIRTUAL_ENV` 环境变量。如果 `VIRTUAL_ENV` 设置为与项目环境不同的路径，将显示警告。可以使用 `--active` 标志选择加入尊重 `VIRTUAL_ENV`。可以使用 `--no-active` 标志来静默警告。

## 构建隔离

默认情况下，根据 [PEP 517](https://peps.python.org/pep-0517/)，uv 在隔离的虚拟环境中构建所有包及其声明的构建依赖项。

有些包与这种构建隔离方法不兼容，无论是有意还是无意。

例如，像 [`flash-attn`](https://pypi.org/project/flash-attn/) 和 [`deepspeed`](https://pypi.org/project/deepspeed/) 这样的包需要针对项目环境中安装的相同版本的 PyTorch 进行构建；通过在隔离环境中构建它们，它们可能会无意中针对不同版本的 PyTorch 进行构建，导致运行时错误。

在其他情况下，包可能会在其声明的构建依赖项列表中意外遗漏必要的依赖项。例如，[`cchardet`](https://pypi.org/project/cchardet/) 要求在安装 `cchardet` 之前将 `cython` 安装在项目环境中，但未将其声明为构建依赖项。

为了解决这些问题，uv 支持两种单独的方法来修改构建隔离行为：

1. **扩展构建依赖项列表**：这允许您在隔离环境中安装包，但带有包本身未声明的额外构建依赖项，通过 [`extra-build-dependencies`](../../reference/settings.md#extra-build-dependencies) 设置。对于像 `flash-attn` 这样的包，您甚至可以强制这些构建依赖项（如 `torch`）与项目环境中安装或将要安装的包版本匹配。

2. **对特定包禁用构建隔离**：这允许您在非隔离环境中安装包。

在可能的情况下，我们建议扩展构建依赖项而不是完全禁用构建隔离，因为后一种方法要求构建依赖项在安装包本身*之前*安装在项目环境中，这可能导致更复杂的安装步骤、项目环境中包含无关的包，以及在其他上下文中重现项目环境时遇到困难。

### 扩展构建依赖项

要为特定包扩展构建依赖项列表，请将其添加到 `pyproject.toml` 中的 [`extra-build-dependencies`](../../reference/settings.md#extra-build-dependencies) 列表中。

例如，要使用 `cython` 作为额外的构建依赖项来构建 `cchardet`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["cchardet"]

[tool.uv.extra-build-dependencies]
cchardet = ["cython"]
```

为了确保构建依赖项与项目环境中安装或将要安装的包版本匹配，请在 `extra-build-dependencies` 表中设置 `match-runtime = true`。例如，要使用 `torch` 作为额外的构建依赖项来构建 `deepspeed`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["deepspeed", "torch"]

[tool.uv.extra-build-dependencies]
deepspeed = [{ requirement = "torch", match-runtime = true }]
```

这将确保 `deepspeed` 使用与项目环境中安装的相同版本的 `torch` 进行构建。

类似地，要使用 `torch` 作为额外的构建依赖项来构建 `flash-attn`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["flash-attn", "torch"]

[tool.uv.extra-build-dependencies]
flash-attn = [{ requirement = "torch", match-runtime = true }]

[tool.uv.extra-build-variables]
flash-attn = { FLASH_ATTENTION_SKIP_CUDA_BUILD = "TRUE" }
```

!!! note

    `FLASH_ATTENTION_SKIP_CUDA_BUILD` 环境变量确保 `flash-attn` 从兼容的预构建 wheel 安装，而不是尝试从源代码构建，后者需要访问 CUDA 开发工具包。如果 CUDA 工具包不可用，可以省略环境变量，`flash-attn` 将根据当前平台、Python 版本和 PyTorch 版本的可用性从预构建 wheel 安装。

类似地，[`deep_gemm`](https://github.com/deepseek-ai/DeepGEMM) 遵循相同的模式：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["deep_gemm", "torch"]

[tool.uv.sources]
deep_gemm = { git = "https://github.com/deepseek-ai/DeepGEMM" }

[tool.uv.extra-build-dependencies]
deep_gemm = [{ requirement = "torch", match-runtime = true }]
```

`extra-build-dependencies` 和 `extra-build-variables` 的使用在 uv 缓存中被跟踪，因此对这些设置的更改将触发受影响包的重新安装和重新构建。例如，在 `flash-attn` 的情况下，升级项目中使用的 `torch` 版本将随后触发使用新版本 `torch` 重新构建 `flash-attn`。

#### 动态元数据

`match-runtime = true` 的使用仅适用于声明静态元数据的包，如 `flash-attn`。如果静态元数据不可用，uv 需要在依赖项解析阶段构建包；因此，uv 无法确定最终将安装在项目环境中的构建依赖项的版本。

换句话说，如果 `flash-attn` 没有声明静态元数据，uv 将无法确定将安装在项目环境中的 `torch` 版本，因为它需要在解析 `torch` 版本之前构建 `flash-attn`。

作为一个具体示例，[`axolotl`](https://pypi.org/project/axolotl/) 是一个需要扩展构建依赖项的流行包，但没有声明静态元数据，因为包的依赖项根据项目环境中安装的 `torch` 版本而变化。在这种情况下，用户应改为指定他们打算在项目中使用的 `torch` 的确切版本，然后用该版本扩展构建依赖项。

例如，要针对 `torch==2.6.0` 构建 `axolotl`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["axolotl[deepspeed, flash-attn]", "torch==2.6.0"]

[tool.uv.extra-build-dependencies]
axolotl = ["torch==2.6.0"]
deepspeed = ["torch==2.6.0"]
flash-attn = ["torch==2.6.0"]
```

类似地，旧版本的 `flash-attn` 没有声明静态元数据，因此开箱即用地不支持 `match-runtime = true`。但与 `axolotl` 不同，`flash-attn` 没有根据构建环境的动态属性改变其依赖项。因此，用户可以通过 [`dependency-metadata`](../../reference/settings.md#dependency-metadata) 设置预先提供 `flash-attn` 元数据，从而避免在依赖项解析阶段构建包的需要。例如，要预先提供 `flash-attn` 元数据：

```toml title="pyproject.toml"
[[tool.uv.dependency-metadata]]
name = "flash-attn"
version = "2.6.3"
requires-dist = ["torch", "einops"]
```

!!! tip

    要确定像 `flash-attn` 这样的包的包元数据，请导航到相应的 Git 存储库，或在 [PyPI](https://pypi.org/project/flash-attn) 上查找并下载包的源发行版。包要求通常可以在 `setup.py` 或 `setup.cfg` 文件中找到。

    （如果包包含构建发行版，您可以解压缩它以找到 `METADATA` 文件；但是，构建发行版的存在将消除预先提供元数据的需要，因为它已经对 uv 可用。）

    `tool.uv.dependency-metadata` 中的 `version` 字段对于基于注册表的依赖项是可选的（当省略时，uv 将假定元数据适用于包的所有版本），但对于直接 URL 依赖项（如 Git 依赖项）是*必需的*。

### 禁用构建隔离

在没有构建隔离的情况下安装包要求包的构建依赖项在构建包本身*之前*安装在项目环境中。

例如，历史上，要在没有构建隔离的情况下安装 `cchardet`，您首先需要将 `cython` 和 `setuptools` 包安装在项目环境中，然后使用单独的命令在没有构建隔离的情况下安装 `cchardet`：

```console
$ uv venv
$ uv pip install cython setuptools
$ uv pip install cchardet --no-build-isolation
```

uv 通过允许您通过 `pyproject.toml` 中的 `no-build-isolation-package` 设置和命令行中的 `--no-build-isolation-package` 标志指定不应在隔离环境中构建的包来简化此过程。此外，当包被标记为禁用构建隔离时，uv 将执行两阶段安装，首先安装任何支持构建隔离的包，然后安装那些不支持构建隔离的包。因此，如果项目的构建依赖项作为项目依赖项包含在内，uv 将在安装需要禁用构建隔离的包之前自动安装它们。

例如，要在没有构建隔离的情况下安装 `cchardet`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["cchardet", "cython", "setuptools"]

[tool.uv]
no-build-isolation-package = ["cchardet"]
```

当运行 `uv sync` 时，uv 将首先在项目环境中安装 `cython` 和 `setuptools`，然后安装 `cchardet`（没有构建隔离）：

```console
$ uv sync --extra build
 + cchardet==2.1.7
 + cython==3.1.3
 + setuptools==80.9.0
```

类似地，要在没有构建隔离的情况下安装 `flash-attn`，请在 `pyproject.toml` 中包含以下内容：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["flash-attn", "torch"]

[tool.uv]
no-build-isolation-package = ["flash-attn"]
```

当运行 `uv sync` 时，uv 将首先在项目环境中安装 `torch`，然后安装 `flash-attn`（没有构建隔离）。由于 `torch` 既是项目依赖项又是构建依赖项，因此 `torch` 的版本在构建环境和运行时环境之间保证一致。

上述方法的一个缺点是它要求构建依赖项安装在项目环境中，这对于 `flash-attn`（在构建时和运行时都需要 `torch`）是合适的，但对于 `cchardet`（仅在构建时需要 `cython`）则不合适。

为了避免在项目环境中包含构建依赖项，uv 支持两步安装过程，允许您将构建依赖项与需要它们的包分开。

例如，`cchardet` 的构建依赖项可以隔离到可选的 `build` 组中，如下所示：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["cchardet"]

[project.optional-dependencies]
build = ["setuptools", "cython"]

[tool.uv]
no-build-isolation-package = ["cchardet"]
```

给定上述内容，用户将首先使用 `build` 可选组同步，然后不使用它以删除构建依赖项：

```console
$ uv sync --extra build
 + cchardet==2.1.7
 + cython==3.1.3
 + setuptools==80.9.0
$ uv sync
 - cython==3.1.3
 - setuptools==80.9.0
```

有些包，如 `cchardet`，仅在 `uv sync` 的*安装*阶段需要构建依赖项。其他包甚至在*解析*阶段解析项目依赖项时就需要其构建依赖项存在。

在这种情况下，可以使用较低级别的 `uv pip` API 在运行任何 `uv lock` 或 `uv sync` 命令之前安装构建依赖项。例如，给定：

```toml title="pyproject.toml"
[project]
name = "project"
version = "0.1.0"
description = "..."
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["flash-attn"]

[tool.uv]
no-build-isolation-package = ["flash-attn"]
```

您可以运行以下命令序列来同步 `flash-attn`：

```console
$ uv venv
$ uv pip install torch setuptools
$ uv sync
```

或者，用户可以通过 [`dependency-metadata`](../../reference/settings.md#dependency-metadata) 设置预先提供 `flash-attn` 元数据，从而避免在依赖项解析阶段构建包的需要。例如，要预先提供 `flash-attn` 元数据：

```toml title="pyproject.toml"
[[tool.uv.dependency-metadata]]
name = "flash-attn"
version = "2.6.3"
requires-dist = ["torch", "einops"]
```

## 可编辑模式

默认情况下，项目将以可编辑模式安装，这样对源代码的更改会立即反映在环境中。`uv sync` 和 `uv run` 都接受 `--no-editable` 标志，该标志指示 uv 以不可编辑模式安装项目。`--no-editable` 用于部署用例，例如构建 Docker 容器，其中项目应包含在部署环境中，而不依赖于原始源代码。

## 冲突依赖项

uv 一起解析所有项目依赖项，包括可选依赖项（"extras"）和依赖项组。如果在一个部分中声明的依赖项与另一个部分中的依赖项不兼容，uv 将无法解析项目的要求并报错。

uv 支持显式声明冲突的依赖项组。例如，声明 `optional-dependency` 组 `extra1` 和 `extra2` 不兼容：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { extra = "extra1" },
      { extra = "extra2" },
    ],
]
```

或者，声明开发依赖项组 `group1` 和 `group2` 不兼容：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { group = "group1" },
      { group = "group2" },
    ],
]
```

有关更多信息，请参阅[解析文档](../resolution.md#冲突依赖项)。

## 有限解析环境

如果您的项目支持更有限的平台或 Python 版本集，您可以通过 `environments` 设置来约束解决的平台集，该设置接受 PEP 508 环境标记的列表。例如，将锁文件限制为 macOS 和 Linux，并排除 Windows：

```toml title="pyproject.toml"
[tool.uv]
environments = [
    "sys_platform == 'darwin'",
    "sys_platform == 'linux'",
]
```

有关更多信息，请参阅[解析文档](../resolution.md#有限解析环境)。

## 必需环境

如果您的项目*必须*支持特定的平台或 Python 版本，您可以通过 `required-environments` 设置将该平台标记为必需。例如，要求项目支持 Intel macOS：

```toml title="pyproject.toml"
[tool.uv]
required-environments = [
    "sys_platform == 'darwin' and platform_machine == 'x86_64'",
]
```

`required-environments` 设置仅与不发布源发行版（如 PyTorch）的包相关，因为此类包*只能*安装在该包发布的预构建二进制发行版（wheels）集合覆盖的环境中。

有关更多信息，请参阅[解析文档](../resolution.md#必需环境)。