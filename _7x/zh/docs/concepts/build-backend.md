# uv 构建后端

构建后端将源树（即目录）转换为源分发版或 wheel。

uv 支持所有构建后端（遵循 [PEP 517](https://peps.python.org/pep-0517/) 规范），但也提供了一个原生构建后端 (`uv_build`)，该后端与 uv 紧密集成以提升性能和用户体验。

## 选择构建后端

对于大多数 Python 项目而言，uv 构建后端是一个很好的选择。它拥有合理的默认值，旨在为大多数用户实现零配置，同时提供了灵活的配置以适应大多数 Python 项目结构。它与 uv 紧密集成，以改善消息传递和用户体验。它验证项目元数据和结构，防止常见错误。最后，它的速度非常快。

uv 构建后端目前**仅支持纯 Python 代码**。构建[带有扩展模块的库](../concepts/projects/init.md#projects-with-extension-modules)需要使用替代的构建后端。

!!! tip

    虽然该后端支持多种选项来配置您的项目结构，但当需要构建脚本或更灵活的项目布局时，请考虑使用 [hatchling](https://hatch.pypa.io/latest/config/build/#build-system) 构建后端。

## 使用 uv 构建后端

要在现有项目中使用 uv 作为构建后端，请将 `uv_build` 添加到您 `pyproject.toml` 文件中的 [`[build-system]`](../concepts/projects/config.md#build-systems) 部分：

```toml title="pyproject.toml"
[build-system]
requires = ["uv_build>=0.9.10,<0.10.0"]
build-backend = "uv_build"
```

!!! note

    uv 构建后端遵循与 uv 相同的[版本控制策略](../reference/policies/versioning.md)。在 `uv_build` 版本上包含一个上限可以确保在新版本发布时您的包仍能正确构建。

要创建一个使用 uv 构建后端的新项目，请使用 `uv init`：

```console
$ uv init
```

当项目被构建时，例如使用 [`uv build`](../guides/package.md)，uv 构建后端将被用于创建源分发版和 wheel。

## 捆绑的构建后端

该构建后端作为一个独立的包 (`uv_build`) 发布，该包针对可移植性和小二进制大小进行了优化。然而，`uv` 可执行文件也包含了一份构建后端的副本，如果其版本与 `uv_build` 要求兼容，则在由 uv 执行的构建过程中（例如在 `uv build` 期间）将会使用它。如果版本不兼容，则将使用兼容版本的 `uv_build` 包。其他构建前端，例如 `python -m build`，将始终使用 `uv_build` 包，通常会选择最新的兼容版本。

## 模块

Python 包预期包含一个或多个 Python 模块，模块是包含 `__init__.py` 的目录。默认情况下，预期在 `src/<package_name>/__init__.py` 处有一个单一的根模块。

例如，一个名为 `foo` 的项目结构将是：

```text
pyproject.toml
src
└── foo
    └── __init__.py
```

uv 对包名进行规范化以确定默认的模块名：包名被转换为小写，点号和破折号被替换为下划线，例如，`Foo-Bar` 将被转换为 `foo_bar`。

`src/` 目录是模块发现的默认目录。

这些默认值可以通过 `module-name` 和 `module-root` 设置来更改。例如，要在根目录中使用名为 `FOO` 的模块，项目结构如下：

```text
pyproject.toml
FOO
└── __init__.py
```

正确的构建配置将是：

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-name = "FOO"
module-root = ""
```

## 命名空间包

命名空间包适用于多个包将模块写入共享命名空间的用例。

命名空间包模块通过 `module-name` 中的 `.` 来标识。例如，要将模块 `bar` 打包到共享命名空间 `foo` 中，项目结构将是：

```text
pyproject.toml
src
└── foo
    └── bar
        └── __init__.py
```

并且 `module-name` 配置将是：

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-name = "foo.bar"
```

!!! important

    `foo` 目录中不包含 `__init__.py` 文件，因为它是一个共享的命名空间模块。

也可以拥有具有多个根模块的复杂命名空间包，例如，项目结构如下：

```text
pyproject.toml
src
├── foo
│   └── __init__.py
└── bar
    └── __init__.py
```

虽然我们不推荐这种结构（即您应该改用包含多个包的工作区），但通过将 `module-name` 设置为名称列表来支持它：

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-name = ["foo", "bar"]
```

对于具有许多模块或复杂命名空间的包，可以使用 `namespace = true` 选项来避免显式声明每个模块名，例如：

```toml title="pyproject.toml"
[tool.uv.build-backend]
namespace = true
```

!!! warning

    使用 `namespace = true` 会禁用安全检查。强烈建议在遗留项目之外使用显式的模块名列表。

`namespace` 选项也可以与 `module-name` 一起使用来显式声明根命名空间，例如，对于以下项目结构：

```text
pyproject.toml
src
└── foo
    ├── bar
    │   └── __init__.py
    └── baz
        └── __init__.py
```

推荐的配置是：

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-name = "foo"
namespace = true
```

## 存根包

该构建后端也支持构建类型存根包，这些包通过包名或模块名上的 `-stubs` 后缀来标识，例如 `foo-stubs`。类型存根包的模块名必须以 `-stubs` 结尾，因此 uv 不会将 `-` 规范化为下划线。此外，uv 将搜索 `__init__.pyi` 文件。例如，项目结构将是：

```text
pyproject.toml
src
└── foo-stubs
    └── __init__.pyi
```

类型存根模块也支持[命名空间包](#namespace-packages)。

## 文件包含与排除

构建后端负责确定源树中的哪些文件应被打包到分发版中。

为了确定在源分发版中包含哪些文件，uv 首先添加包含的文件和目录，然后移除排除的文件和目录。这意味着排除总是优先于包含。

默认情况下，uv 排除 `__pycache__`、`*.pyc` 和 `*.pyo`。

在构建源分发版时，以下文件和目录被包含：

- `pyproject.toml` 文件
- 位于 [`tool.uv.build-backend.module-root`](../reference/settings.md#build-backend_module-root) 下的[模块](#modules)。
- 由 `project.license-files` 和 `project.readme` 引用的文件。
- [`tool.uv.build-backend.data`](../reference/settings.md#build-backend_data) 下的所有目录。
- 匹配 [`tool.uv.build-backend.source-include`](../reference/settings.md#build-backend_source-include) 模式的所有文件。

从这些内容中，匹配 [`tool.uv.build-backend.source-exclude`](../reference/settings.md#build-backend_source-exclude) 和[默认排除项](../reference/settings.md#build-backend_default-excludes) 的项目将被移除。

在构建 wheel 时，以下文件和目录被包含：

- 位于 [`tool.uv.build-backend.module-root`](../reference/settings.md#build-backend_module-root) 下的[模块](#modules)。
- 由 `project.license-files` 引用的文件，这些文件被复制到 `.dist-info` 目录中。
- `project.readme` 文件，它被复制到项目元数据中。
- [`tool.uv.build-backend.data`](../reference/settings.md#build-backend_data) 下的所有目录，这些目录被复制到 `.data` 目录中。

从这些内容中，[`tool.uv.build-backend.source-exclude`](../reference/settings.md#build-backend_source-exclude)、[`tool.uv.build-backend.wheel-exclude`](../reference/settings.md#build-backend_wheel-exclude) 以及默认排除项将被移除。应用源分发版排除是为了避免从源树到 wheel 的构建比从源树到源分发版再到 wheel 的构建包含更多的文件。

没有特定的 wheel 包含项。必须只有一个顶级模块，并且所有数据文件必须位于模块根目录下或适当的[数据目录](../reference/settings.md#build-backend_data)中。大多数包将小数据存储在模块根目录下，与源代码放在一起。

!!! tip

    当通过非 uv 的前端（如 pip 或 `python -m build`）使用 uv 构建后端时，可以通过环境变量 `RUST_LOG=uv=debug` 或 `RUST_LOG=uv=verbose` 启用调试日志记录。当通过 uv 使用时，uv 构建后端共享 uv 的详细级别。

### 包含与排除语法

包含是锚定的，这意味着 `pyproject.toml` 仅包含 `<root>/pyproject.toml`，而不包含 `<root>/bar/pyproject.toml`。要递归地包含目录下的所有文件，请使用 `/**` 后缀，例如 `src/**`。递归包含也是锚定的，例如，`assets/**/sample.csv` 包含 `<root>/assets` 或其任何子目录中的所有 `sample.csv` 文件。

!!! note

    为了性能和可重现性，请避免使用没有锚点的模式，例如 `**/sample.csv`。

排除不是锚定的，这意味着 `__pycache__` 会排除所有名为 `__pycache__` 的目录，无论其父目录是什么。排除项的所有子项也会被排除。要锚定一个目录，请使用 `/` 前缀，例如，`/dist` 将仅排除 `<root>/dist`。

所有接受模式的字段都使用 [PEP 639](https://peps.python.org/pep-0639/#add-license-FILES-key) 中的简化可移植 glob 语法，并增加了可以使用反斜杠转义字符的功能。