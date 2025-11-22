# 管理依赖项

## 依赖项字段

项目的依赖项在以下几个字段中定义：

- [`project.dependencies`](#project-dependencies): 发布的依赖项。
- [`project.optional-dependencies`](#optional-dependencies): 发布的可选依赖项，或称为"extras"。
- [`dependency-groups`](#dependency-groups): 用于开发的本地依赖项。
- [`tool.uv.sources`](#dependency-sources): 开发期间依赖项的替代源。

!!! note

    即使项目不打算发布，也可以使用 `project.dependencies` 和 `project.optional-dependencies` 字段。`dependency-groups` 是最近标准化的功能，可能尚未被所有工具支持。

uv 支持使用 `uv add` 和 `uv remove` 修改项目的依赖项，但也可以通过直接编辑 `pyproject.toml` 来更新依赖项元数据。

## 添加依赖项

要添加依赖项：

```console
$ uv add httpx
```

将在 `project.dependencies` 字段中添加一个条目：

```toml title="pyproject.toml" hl_lines="4"
[project]
name = "example"
version = "0.1.0"
dependencies = ["httpx>=0.27.2"]
```

可以使用 [`--dev`](#development-dependencies)、[`--group`](#dependency-groups) 或 [`--optional`](#optional-dependencies) 标志将依赖项添加到替代字段。

依赖项将包含一个约束，例如 `>=0.27.2`，表示包的最新兼容版本。可以使用 [`--bounds`](../../reference/settings.md#add-bounds) 调整边界类型，或者直接提供约束：

```console
$ uv add "httpx>=0.20"
```

当从包注册表以外的源添加依赖项时，uv 将在源字段中添加一个条目。例如，从 GitHub 添加 `httpx`：

```console
$ uv add "httpx @ git+https://github.com/encode/httpx"
```

`pyproject.toml` 将包含一个 [Git 源条目](#git)：

```toml title="pyproject.toml" hl_lines="8-9"
[project]
name = "example"
version = "0.1.0"
dependencies = [
    "httpx",
]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx" }
```

如果依赖项无法使用，uv 将显示错误：

```console
$ uv add "httpx>9999"
  × No solution found when resolving dependencies:
  ╰─▶ Because only httpx<=1.0.0b0 is available and your project depends on httpx>9999,
      we can conclude that your project's requirements are unsatisfiable.
```

### 从 requirements 文件导入依赖项

在 `requirements.txt` 文件中声明的依赖项可以使用 `-r` 选项添加到项目中：

```
uv add -r requirements.txt
```

有关更多详细信息，请参阅 [pip 迁移指南](../../guides/migration/pip-to-project.md#importing-requirements-files)。

## 移除依赖项

要移除依赖项：

```console
$ uv remove httpx
```

可以使用 `--dev`、`--group` 或 `--optional` 标志从特定表中移除依赖项。

如果为被移除的依赖项定义了[源](#dependency-sources)，并且没有其他对该依赖项的引用，则该源也将被移除。

## 更改依赖项

要更改现有依赖项，例如，为 `httpx` 使用不同的约束：

```console
$ uv add "httpx>0.1.0"
```

!!! note

    在此示例中，我们正在更改 `pyproject.toml` 中依赖项的约束。依赖项的锁定版本仅在新约束需要满足时才会更改。要强制将包版本升级到约束范围内的最新版本，请使用 `--upgrade-package <name>`，例如：

    ```console
    $ uv add "httpx>0.1.0" --upgrade-package httpx
    ```

    有关升级包的更多详细信息，请参阅 [lockfile](./sync.md#upgrading-locked-package-versions) 文档。

请求不同的依赖项源将更新 `tool.uv.sources` 表，例如，在开发期间使用本地路径的 `httpx`：

```console
$ uv add "httpx @ ../httpx"
```

## 平台特定依赖项

为确保依赖项仅在特定平台或特定 Python 版本上安装，请使用[环境标记](https://peps.python.org/pep-0508/#environment-markers)。

例如，在 Linux 上安装 `jax`，但不在 Windows 或 macOS 上安装：

```console
$ uv add "jax; sys_platform == 'linux'"
```

生成的 `pyproject.toml` 将在依赖项定义中包含环境标记：

```toml title="pyproject.toml" hl_lines="6"
[project]
name = "project"
version = "0.1.0"
requires-python = ">=3.11"
dependencies = ["jax; sys_platform == 'linux'"]
```

类似地，在 Python 3.11 及更高版本中包含 `numpy`：

```console
$ uv add "numpy; python_version >= '3.11'"
```

有关可用标记和运算符的完整枚举，请参阅 Python 的[环境标记](https://peps.python.org/pep-0508/#environment-markers)文档。

!!! tip

    依赖项源也可以[按平台更改](#platform-specific-sources)。

## 项目依赖项

`project.dependencies` 表表示上传到 PyPI 或构建 wheel 时使用的依赖项。各个依赖项使用[依赖项说明符](https://packaging.python.org/en/latest/specifications/dependency-specifiers/)语法指定，该表遵循 [PEP 621](https://packaging.python.org/en/latest/specifications/pyproject-toml/) 标准。

`project.dependencies` 定义了项目所需的包列表，以及在安装它们时应使用的版本约束。每个条目包括一个依赖项名称和版本。条目可能包含用于平台特定包的 extras 或环境标记。例如：

```toml title="pyproject.toml"
[project]
name = "albatross"
version = "0.1.0"
dependencies = [
  # 此范围内的任何版本
  "tqdm >=4.66.2,<5",
  # torch 的确切此版本
  "torch ==2.2.2",
  # 安装带有 torch extra 的 transformers
  "transformers[torch] >=4.39.3,<5",
  # 仅在较旧的 python 版本上安装此包
  # 有关更多信息，请参阅“环境标记”
  "importlib_metadata >=7.1.0,<8; python_version < '3.10'",
  "mollymawk ==0.1.0"
]
```

## 依赖项源

`tool.uv.sources` 表使用替代依赖项源扩展了标准依赖项表，这些源在开发期间使用。

依赖项源添加了对 `project.dependencies` 标准不支持的一些常见模式的支持，例如可编辑安装和相对路径。例如，要从相对于项目根目录的目录安装 `foo`：

```toml title="pyproject.toml" hl_lines="7"
[project]
name = "example"
version = "0.1.0"
dependencies = ["foo"]

[tool.uv.sources]
foo = { path = "./packages/foo" }
```

uv 支持以下依赖项源：

- [Index](#index): 从特定包索引解析的包。
- [Git](#git): Git 仓库。
- [URL](#url): 远程 wheel 或源码分发。
- [Path](#path): 本地 wheel、源码分发或项目目录。
- [Workspace](#workspace-member): 当前工作空间的成员。

!!! important

    源仅由 uv 遵守。如果使用其他工具，则仅使用标准项目表中的定义。如果使用其他工具进行开发，则源表中提供的任何元数据都需要以该其他工具的格式重新指定。

### Index

要从特定索引添加 Python 包，请使用 `--index` 选项：

```console
$ uv add torch --index pytorch=https://download.pytorch.org/whl/cpu
```

uv 将把索引存储在 `[[tool.uv.index]]` 中，并添加一个 `[tool.uv.sources]` 条目：

```toml title="pyproject.toml"
[project]
dependencies = ["torch"]

[tool.uv.sources]
torch = { index = "pytorch" }

[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cpu"
```

!!! tip

    由于 PyTorch 索引的具体情况，上述示例仅适用于 x86-64 Linux。有关设置 PyTorch 的更多信息，请参阅 [PyTorch 指南](../../guides/integration/pytorch.md)。

使用 `index` 源会将包*固定*到给定的索引——它不会从其他索引下载。

定义索引时，可以包含一个 `explicit` 标志，以指示该索引应*仅*用于在 `tool.uv.sources` 中明确指定它的包。如果未设置 `explicit`，则如果在其他地方找不到，其他包可能会从该索引解析。

```toml title="pyproject.toml" hl_lines="4"
[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cpu"
explicit = true
```

### Git

要添加 Git 依赖项源，请在 Git 兼容的 URL 前加上 `git+`。

例如：

```console
$ # 通过 HTTP(S) 安装。
$ uv add git+https://github.com/encode/httpx

$ # 通过 SSH 安装。
$ uv add git+ssh://git@github.com/encode/httpx
```

```toml title="pyproject.toml" hl_lines="5"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx" }
```

可以请求特定的 Git 引用，例如，一个标签：

```console
$ uv add git+https://github.com/encode/httpx --tag 0.27.0
```

```toml title="pyproject.toml" hl_lines="7"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx", tag = "0.27.0" }
```

或者，一个分支：

```console
$ uv add git+https://github.com/encode/httpx --branch main
```

```toml title="pyproject.toml" hl_lines="7"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx", branch = "main" }
```

或者，一个修订版本（提交）：

```console
$ uv add git+https://github.com/encode/httpx --rev 326b9431c761e1ef1e00b9f760d1f654c8db48c6
```

```toml title="pyproject.toml" hl_lines="7"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx", rev = "326b9431c761e1ef1e00b9f760d1f654c8db48c6" }
```

如果包不在仓库根目录中，可以指定一个 `subdirectory`：

```console
$ uv add git+https://github.com/langchain-ai/langchain#subdirectory=libs/langchain
```

```toml title="pyproject.toml"
[project]
dependencies = ["langchain"]

[tool.uv.sources]
langchain = { git = "https://github.com/langchain-ai/langchain", subdirectory = "libs/langchain" }
```

### URL

要添加 URL 源，请提供一个指向 wheel（以 `.whl` 结尾）或源码分发（通常以 `.tar.gz` 或 `.zip` 结尾；有关所有支持的格式，请参阅[此处](../../concepts/resolution.md#source-distribution)）的 `https://` URL。

例如：

```console
$ uv add "https://files.pythonhosted.org/packages/5c/2d/3da5bdf4408b8b2800061c339f240c1802f2e82d55e50bd39c5a881f47f0/httpx-0.27.0.tar.gz"
```

将生成一个包含以下内容的 `pyproject.toml`：

```toml title="pyproject.toml" hl_lines="5"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { url = "https://files.pythonhosted.org/packages/5c/2d/3da5bdf4408b8b2800061c339f240c1802f2e82d55e50bd39c5a881f47f0/httpx-0.27.0.tar.gz" }
```

URL 依赖项也可以使用 `{ url = <url> }` 语法在 `pyproject.toml` 中手动添加或编辑。如果源码分发不在存档根目录中，可以指定 `subdirectory`。

### Path

要添加路径源，请提供 wheel（以 `.whl` 结尾）、源码分发（通常以 `.tar.gz` 或 `.zip` 结尾；有关所有支持的格式，请参阅[此处](../../concepts/resolution.md#source-distribution)）或包含 `pyproject.toml` 的目录的路径。

例如：

```console
$ uv add /example/foo-0.1.0-py3-none-any.whl
```

将生成一个包含以下内容的 `pyproject.toml`：

```toml title="pyproject.toml"
[project]
dependencies = ["foo"]

[tool.uv.sources]
foo = { path = "/example/foo-0.1.0-py3-none-any.whl" }
```

路径也可以是相对路径：

```console
$ uv add ./foo-0.1.0-py3-none-any.whl
```

或者，指向项目目录的路径：

```console
$ uv add ~/projects/bar/
```

!!! important

    当使用目录作为路径依赖项时，uv 默认会尝试将目标构建并安装为一个包。有关详细信息，请参阅[虚拟依赖项](#virtual-dependencies)文档。

默认情况下，路径依赖项不使用[可编辑安装](#editable-dependencies)。可以为项目目录请求可编辑安装：

```console
$ uv add --editable ../projects/bar/
```

这将生成一个包含以下内容的 `pyproject.toml`：

```toml title="pyproject.toml"
[project]
dependencies = ["bar"]

[tool.uv.sources]
bar = { path = "../projects/bar", editable = true }
```

!!! tip

    对于同一仓库中的多个包，[_工作空间_](./workspaces.md) 可能是更好的选择。

### Workspace member

要声明对工作空间成员的依赖，请使用 `{ workspace = true }` 添加成员名称。所有工作空间成员必须明确声明。工作空间成员始终是[可编辑的](#editable-dependencies)。有关工作空间的更多详细信息，请参阅 [workspace](./workspaces.md) 文档。

```toml title="pyproject.toml"
[project]
dependencies = ["foo==0.1.0"]

[tool.uv.sources]
foo = { workspace = true }

[tool.uv.workspace]
members = [
  "packages/foo"
]
```

### 平台特定源

您可以通过为源提供与[依赖项说明符](https://packaging.python.org/en/latest/specifications/dependency-specifiers/)兼容的环境标记，将源限制在给定的平台或 Python 版本。

例如，要在 macOS 上从 GitHub 拉取 `httpx`，请使用以下内容：

```toml title="pyproject.toml" hl_lines="8"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx", tag = "0.27.2", marker = "sys_platform == 'darwin'" }
```

通过在源上指定标记，uv 仍将在所有平台上包含 `httpx`，但将在 macOS 上从 GitHub 下载源，并在所有其他平台上回退到 PyPI。

### 多个源

您可以通过提供源列表来为单个依赖项指定多个源，这些源通过 [PEP 508](https://peps.python.org/pep-0508/#environment-markers) 兼容的环境标记来消除歧义。

例如，在 macOS 和 Linux 上拉取不同的 `httpx` 标签：

```toml title="pyproject.toml" hl_lines="6-7"
[project]
dependencies = ["httpx"]

[tool.uv.sources]
httpx = [
  { git = "https://github.com/encode/httpx", tag = "0.27.2", marker = "sys_platform == 'darwin'" },
  { git = "https://github.com/encode/httpx", tag = "0.24.1", marker = "sys_platform == 'linux'" },
]
```

此策略扩展到基于环境标记使用不同的索引。例如，根据平台从不同的 PyTorch 索引安装 `torch`：

```toml title="pyproject.toml" hl_lines="6-7"
[project]
dependencies = ["torch"]

[tool.uv.sources]
torch = [
  { index = "torch-cpu", marker = "platform_system == 'Darwin'"},
  { index = "torch-gpu", marker = "platform_system == 'Linux'"},
]

[[tool.uv.index]]
name = "torch-cpu"
url = "https://download.pytorch.org/whl/cpu"
explicit = true

[[tool.uv.index]]
name = "torch-gpu"
url = "https://download.pytorch.org/whl/cu124"
explicit = true
```

### 禁用源

要指示 uv 忽略 `tool.uv.sources` 表（例如，模拟使用包的已发布元数据进行解析），请使用 `--no-sources` 标志：

```console
$ uv lock --no-sources
```

使用 `--no-sources` 也会阻止 uv 发现任何可以满足给定依赖项的[工作空间成员](#workspace-member)。

## 可选依赖项

发布为库的项目通常会使其某些功能成为可选的，以减少默认的依赖树。例如，Pandas 有一个 [`excel` extra](https://pandas.pydata.org/docs/getting_started/install.html#excel-files) 和一个 [`plot` extra](https://pandas.pydata.org/docs/getting_started/install.html#visualization)，以避免在有人明确要求之前安装 Excel 解析器和 `matplotlib`。Extras 使用 `package[<extra>]` 语法请求，例如 `pandas[plot, excel]`。

可选依赖项在 `[project.optional-dependencies]` 中指定，这是一个 TOML 表，将 extra 名称映射到其依赖项，遵循[依赖项说明符](#dependency-specifiers)语法。

可选依赖项可以像普通依赖项一样在 `tool.uv.sources` 中有条目。

```toml title="pyproject.toml"
[project]
name = "pandas"
version = "1.0.0"

[project.optional-dependencies]
plot = [
  "matplotlib>=3.6.3"
]
excel = [
  "odfpy>=1.4.1",
  "openpyxl>=3.1.0",
  "python-calamine>=0.1.7",
  "pyxlsb>=1.0.10",
  "xlrd>=2.0.1",
  "xlsxwriter>=3.0.5"
]
```

要添加可选依赖项，请使用 `--optional <extra>` 选项：

```console
$ uv add httpx --optional network
```

!!! note

    如果您的可选依赖项相互冲突，除非您明确[将它们声明为冲突](./config.md#conflicting-dependencies)，否则解析将失败。

源也可以声明为仅适用于特定的可选依赖项。例如，根据可选的 `cpu` 或 `gpu` extra 从不同的 PyTorch 索引拉取 `torch`：

```toml title="pyproject.toml"
[project]
dependencies = []

[project.optional-dependencies]
cpu = [
  "torch",
]
gpu = [
  "torch",
]

[tool.uv.sources]
torch = [
  { index = "torch-cpu", extra = "cpu" },
  { index = "torch-gpu", extra = "gpu" },
]

[[tool.uv.index]]
name = "torch-cpu"
url = "https://download.pytorch.org/whl/cpu"

[[tool.uv.index]]
name = "torch-gpu"
url = "https://download.pytorch.org/whl/cu124"
```

## 开发依赖项

与可选依赖项不同，开发依赖项是本地专用的，在发布到 PyPI 或其他索引时*不会*包含在项目要求中。因此，开发依赖项不包含在 `[project]` 表中。

开发依赖项可以像普通依赖项一样在 `tool.uv.sources` 中有条目。

要添加开发依赖项，请使用 `--dev` 标志：

```console
$ uv add --dev pytest
```

uv 使用 `[dependency-groups]` 表（在 [PEP 735](https://peps.python.org/pep-0735/) 中定义）来声明开发依赖项。上述命令将创建一个 `dev` 组：

```toml title="pyproject.toml"
[dependency-groups]
dev = [
  "pytest >=8.1.1,<9"
]
```

`dev` 组是特殊处理的；有 `--dev`、`--only-dev` 和 `--no-dev` 标志来切换其依赖项的包含或排除。有关禁用所有默认组的信息，请参阅 `--no-default-groups`。此外，`dev` 组[默认同步](#default-groups)。

### 依赖项组

开发依赖项可以使用 `--group` 标志划分为多个组。

例如，要在 `lint` 组中添加开发依赖项：

```console
$ uv add --group lint ruff
```

这将生成以下 `[dependency-groups]` 定义：

```toml title="pyproject.toml"
[dependency-groups]
dev = [
  "pytest"
]
lint = [
  "ruff"
]
```

一旦定义了组，可以使用 `--all-groups`、`--no-default-groups`、`--group`、`--only-group` 和 `--no-group` 选项来包含或排除它们的依赖项。

!!! tip

    `--dev`、`--only-dev` 和 `--no-dev` 标志分别等同于 `--group dev`、`--only-group dev` 和 `--no-group dev`。

uv 要求所有依赖项组彼此兼容，并在创建 lockfile 时一起解析所有组。

如果一个组中声明的依赖项与另一个组中的依赖项不兼容，uv 将无法解析项目的要求并报错。

!!! note

    如果您的依赖项组相互冲突，除非您明确[将它们声明为冲突](./config.md#conflicting-dependencies)，否则解析将失败。

### 嵌套组

一个依赖项组可以包含其他依赖项组，例如：

```toml title="pyproject.toml"
[dependency-groups]
dev = [
  {include-group = "lint"},
  {include-group = "test"}
]
lint = [
  "ruff"
]
test = [
  "pytest"
]
```

被包含组的依赖项不能与组中声明的其他依赖项冲突。

### 默认组

默认情况下，uv 在环境中包含 `dev` 依赖项组（例如，在 `uv run` 或 `uv sync` 期间）。可以使用 `tool.uv.default-groups` 设置更改要包含的默认组。

```toml title="pyproject.toml"
[tool.uv]
default-groups = ["dev", "foo"]
```

要默认启用所有依赖项组，请使用 `"all"` 而不是列出组名：

```toml title="pyproject.toml"
[tool.uv]
default-groups = "all"
```

!!! tip

    要在 `uv run` 或 `uv sync` 期间禁用此行为，请使用 `--no-default-groups`。
    要排除特定的默认组，请使用 `--no-group <name>`。

### 组的 `requires-python`

默认情况下，依赖项组必须与项目的 `requires-python` 范围兼容。

如果依赖项组需要与项目不同的 Python 版本范围，您可以在 `[tool.uv.dependency-groups]` 中为组指定 `requires-python`，例如：

```toml title="pyproject.toml" hl_lines="9-10"
[project]
name = "example"
version = "0.0.0"
requires-python = ">=3.10"

[dependency-groups]
dev = ["pytest"]

[tool.uv.dependency-groups]
dev = {requires-python = ">=3.12"}
```

### 传统的 `dev-dependencies`

在 `[dependency-groups]` 标准化之前，uv 使用 `tool.uv.dev-dependencies` 字段来指定开发依赖项，例如：

```toml title="pyproject.toml"
[tool.uv]
dev-dependencies = [
  "pytest"
]
```

在此部分声明的依赖项将与 `dependency-groups.dev` 中的内容合并。最终，`dev-dependencies` 字段将被弃用并移除。

!!! note

    如果存在 `tool.uv.dev-dependencies` 字段，`uv add --dev` 将使用现有部分而不是添加新的 `dependency-groups.dev` 部分。

## 构建依赖项

如果项目结构为 [Python 包](./config.md#build-systems)，它可以声明构建项目所需但运行项目不需要的依赖项。这些依赖项在 `[build-system]` 表中的 `build-system.requires` 下指定，遵循 [PEP 518](https://peps.python.org/pep-0518/)。

例如，如果项目使用 `setuptools` 作为其构建后端，则应声明 `setuptools` 为构建依赖项：

```toml title="pyproject.toml"
[project]
name = "pandas"
version = "0.1.0"

[build-system]
requires = ["setuptools>=42"]
build-backend = "setuptools.build_meta"
```

默认情况下，uv 在解析构建依赖项时会遵守 `tool.uv.sources`。例如，要使用 `setuptools` 的本地版本进行构建，请将源添加到 `tool.uv.sources`：

```toml title="pyproject.toml"
[project]
name = "pandas"
version = "0.1.0"

[build-system]
requires = ["setuptools>=42"]
build-backend = "setuptools.build_meta"

[tool.uv.sources]
setuptools = { path = "./packages/setuptools" }
```

发布包时，我们建议运行 `uv build --no-sources` 以确保在禁用 `tool.uv.sources` 时包能正确构建，就像使用其他构建工具（如 [`pypa/build`](https://github.com/pypa/build)）时的情况一样。

## 可编辑依赖项

对带有 Python 包的目录进行常规安装时，会先构建一个 wheel，然后将该 wheel 安装到虚拟环境中，复制所有源文件。当包源文件被编辑时，虚拟环境将包含过时的版本。

可编辑安装通过向虚拟环境中的项目添加链接（一个 `.pth` 文件）来解决此问题，该链接指示解释器直接包含源文件。

可编辑安装有一些限制（主要是：构建后端需要支持它们，并且在导入之前不会重新编译原生模块），但它们对于开发很有用，因为虚拟环境将始终使用包的最新更改。

uv 默认对工作空间包使用可编辑安装。

要添加可编辑依赖项，请使用 `--editable` 标志：

```console
$ uv add --editable ./path/foo
```

或者，选择在工作空间中不使用可编辑依赖项：

```console
$ uv add --no-editable ./path/foo
```

## 虚拟依赖项

uv 允许依赖项是“虚拟的”，在这种情况下，依赖项本身不作为[包](./config.md#project-packaging)安装，但其依赖项会被安装。

默认情况下，依赖项从不虚拟。

具有 [`path` 源](#path) 的依赖项可以是虚拟的，如果它明确设置了 [`tool.uv.package = false`](../../reference/settings.md#package)。与使用 uv *在*依赖项目中工作不同，即使未声明[构建系统](./config.md#build-systems)，该包也会被构建。

要将依赖项视为虚拟的，请在源上设置 `package = false`：

```toml title="pyproject.toml"
[project]
dependencies = ["bar"]

[tool.uv.sources]
bar = { path = "../projects/bar", package = false }
```

如果依赖项设置了 `tool.uv.package = false`，可以通过在源上声明 `package = true` 来覆盖它：

```toml title="pyproject.toml"
[project]
dependencies = ["bar"]

[tool.uv.sources]
bar = { path = "../projects/bar", package = true }
```

类似地，具有 [`workspace` 源](#workspace-member) 的依赖项可以是虚拟的，如果它明确设置了 [`tool.uv.package = false`](../../reference/settings.md#package)。即使未声明[构建系统](./config.md#build-systems)，工作空间成员也会被构建。

*不是*依赖项的工作空间成员默认可以是虚拟的，例如，如果父 `pyproject.toml` 是：

```toml title="pyproject.toml"
[project]
name = "parent"
version = "1.0.0"
dependencies = []

[tool.uv.workspace]
members = ["child"]
```

并且子 `pyproject.toml` 排除了构建系统：

```toml title="pyproject.toml"
[project]
name = "child"
version = "1.0.0"
dependencies = ["anyio"]
```

那么 `child` 工作空间成员将不会被安装，但传递依赖项 `anyio` 会被安装。

相反，如果父级声明了对 `child` 的依赖：

```toml title="pyproject.toml"
[project]
name = "parent"
version = "1.0.0"
dependencies = ["child"]

[tool.uv.sources]
child = { workspace = true }

[tool.uv.workspace]
members = ["child"]
```

那么 `child` 将被构建和安装。

## 依赖项说明符

uv 使用标准的[依赖项说明符](https://packaging.python.org/en/latest/specifications/dependency-specifiers/)，最初在 [PEP 508](https://peps.python.org/pep-0508/) 中定义。依赖项说明符按顺序由以下部分组成：

- 依赖项名称
- 您想要的 extras（可选）
- 版本说明符
- 环境标记（可选）

版本说明符以逗号分隔并相加，例如，`foo >=1.2.3,<2,!=1.4.0` 被解释为“`foo` 的一个版本，至少为 1.2.3，但小于 2，且不是 1.4.0”。

如果需要，说明符会用尾随零填充，因此 `foo ==2` 也匹配 foo 2.0.0。

星号可以与 equals 一起用于最后一位数字，例如，`foo ==2.1.*` 将接受 2.1 系列的任何发布。类似地，`~=` 匹配最后一位数字相等或更高的版本，例如，`foo ~=1.2` 等于 `foo >=1.2,<2`，而 `foo ~=1.2.3` 等于 `foo >=1.2.3,<1.3`。

Extras 在名称和版本之间的方括号中用逗号分隔，例如，`pandas[excel,plot] ==2.2`。extra 名称之间的空格被忽略。

某些依赖项仅在特定环境中需要，例如，特定的 Python 版本或操作系统。例如，要为 `importlib.metadata` 模块安装 `importlib-metadata` 回溯，请使用 `importlib-metadata >=7.1.0,<8; python_version < '3.10'`。要在 Windows 上安装 `colorama`（但在其他平台上省略它），请使用 `colorama >=0.4.6,<5; platform_system == "Windows"`。

标记与 `and`、`or` 和括号组合使用，例如，`aiohttp >=3.7.4,<4; (sys_platform != 'win32' or implementation_name != 'pypy') and python_version >= '3.10'`。请注意，标记内的版本必须加引号，而标记*外*的版本*不得*加引号。
