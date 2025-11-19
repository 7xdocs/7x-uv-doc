
# Project metadata
## [`build-constraint-dependencies`](#build-constraint-dependencies) {: #build-constraint-dependencies }

解决构建依赖时应用的约束。

构建约束用于限制在解析或安装期间构建包时选择的构建依赖版本。

将包包含为约束将_不会_在构建期间触发该包的安装；相反，该包必须在项目的构建依赖关系图中的其他地方被请求。

!!! note
    在 `uv lock`、`uv sync` 和 `uv run` 中，uv 只会从工作空间根目录的 `pyproject.toml` 读取 `build-constraint-dependencies`，并忽略其他工作空间成员或 `uv.toml` 文件中的任何声明。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 确保每当包对 setuptools 有构建依赖时，都使用 setuptools v60.0.0。
build-constraint-dependencies = ["setuptools==60.0.0"]
```

---

## [`conflicts`](#conflicts) {: #conflicts }

声明冲突（即互斥）的扩展或依赖组集合。

当两个或多个扩展具有互不兼容的依赖时，声明冲突非常有用。例如，扩展 `foo` 可能依赖于 `numpy==2.0.0`，而扩展 `bar` 依赖于 `numpy==2.1.0`。虽然这些依赖存在冲突，但可能预期用户不会同时激活 `foo` 和 `bar`，这使得尽管存在不兼容性，仍可以为项目生成通用解析。

通过明确此类冲突，uv 可以为项目生成通用解析，同时考虑到某些扩展和组的组合是互斥的。作为交换，如果用户尝试同时激活两个冲突的扩展，安装将会失败。

**默认值**: `[]`

**类型**: `list[list[dict]]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 要求 `package[extra1]` 和 `package[extra2]` 在不同的分支中解析，以使它们不能相互冲突。
conflicts = [
    [
        { extra = "extra1" },
        { extra = "extra2" },
    ]
]

# 要求依赖组 `group1` 和 `group2` 在不同的分支中解析，以使它们不能相互冲突。
conflicts = [
    [
        { group = "group1" },
        { group = "group2" },
    ]
]
```

---

## [`constraint-dependencies`](#constraint-dependencies) {: #constraint-dependencies }

解析项目依赖时应用的约束。

约束用于限制在解析期间选择的依赖版本。

将包包含为约束将_不会_自行触发该包的安装；相反，该包必须在项目的一阶或传递依赖中的其他地方被请求。

!!! note
    在 `uv lock`、`uv sync` 和 `uv run` 中，uv 只会从工作空间根目录的 `pyproject.toml` 读取 `constraint-dependencies`，并忽略其他工作空间成员或 `uv.toml` 文件中的任何声明。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 确保 grpcio 版本始终小于 1.65，如果它被直接或传递依赖请求。
constraint-dependencies = ["grpcio<1.65"]
```

---

## [`default-groups`](#default-groups) {: #default-groups }

默认安装的 `dependency-groups` 列表。

也可以是字面量 `"all"` 以默认启用所有组。

**默认值**: `["dev"]`

**类型**: `str | list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
default-groups = ["docs"]
```

---

## [`dependency-groups`](#dependency-groups) {: #dependency-groups }

`dependency-groups` 的附加设置。

目前这只能用于向依赖组添加 `requires-python` 约束（通常用于告知 uv 你的开发工具比实际项目有更高的 Python 要求）。

这不能用于定义依赖组，请使用顶层的 `[dependency-groups]` 表来定义。

**默认值**: `[]`

**类型**: `dict`

**示例用法**:

```toml title="pyproject.toml"

[tool.uv.dependency-groups]
my-group = {requires-python = ">=3.12"}
```

---

## [`dev-dependencies`](#dev-dependencies) {: #dev-dependencies }

项目的开发依赖。

开发依赖将在 `uv run` 和 `uv sync` 中默认安装，但不会出现在项目发布的元数据中。

不再推荐使用此字段。相反，请使用 `dependency-groups.dev` 字段，这是声明开发依赖的标准化方式。`tool.uv.dev-dependencies` 和 `dependency-groups.dev` 的内容会被合并以确定 `dev` 依赖组的最终要求。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
dev-dependencies = ["ruff==0.5.0"]
```

---

## [`environments`](#environments) {: #environments }

解析依赖所针对的支持环境列表。

默认情况下，uv 会在 `uv lock` 操作期间为所有可能的环境进行解析。但是，你可以限制支持的环境集以提高性能并避免解空间中出现无法满足的分支。

当使用 `--universal` 标志调用 `uv pip compile` 时，这些环境也将被遵守。

**默认值**: `[]`

**类型**: `str | list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 为 macOS 解析，但不为 Linux 或 Windows 解析。
environments = ["sys_platform == 'darwin'"]
```

---

## [`exclude-dependencies`](#exclude-dependencies) {: #exclude-dependencies }

解析项目依赖时要排除的依赖。

排除项用于防止包在解析期间被选中，无论是否有其他包请求它。当包被排除时，它将完全从依赖列表中省略。

将包包含为排除项将阻止其被安装，即使传递依赖请求它。这对于移除可选依赖或解决具有损坏依赖的包非常有用。

!!! note
    在 `uv lock`、`uv sync` 和 `uv run` 中，uv 只会从工作空间根目录的 `pyproject.toml` 读取 `exclude-dependencies`，并忽略其他工作空间成员或 `uv.toml` 文件中的任何声明。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 排除 Werkzeug 被安装，即使传递依赖请求它。
exclude-dependencies = ["werkzeug"]
```

---

## [`index`](#index) {: #index }

解析依赖时使用的索引。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

索引按定义的顺序考虑，因此第一个定义的索引具有最高优先级。此外，通过此设置提供的索引比通过 [`index_url`](#index-url) 或 [`extra_index_url`](#extra-index-url) 指定的任何索引具有更高的优先级。除非指定了替代的[索引策略](#index-strategy)，否则 uv 只会考虑包含给定包的第一个索引。

如果索引被标记为 `explicit = true`，它将专门用于那些通过 `[tool.uv.sources]` 明确选择它的依赖，如下所示：

```toml
[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cu121"
explicit = true

[tool.uv.sources]
torch = { index = "pytorch" }
```

如果索引被标记为 `default = true`，它将被移动到优先级列表的末尾，以便在解析包时给予最低优先级。此外，将索引标记为默认值将禁用 PyPI 默认索引。

**默认值**: `[]`

**类型**: `dict`

**示例用法**:

```toml title="pyproject.toml"

[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cu121"
```

---

## [`managed`](#managed) {: #managed }

项目是否由 uv 管理。如果为 `false`，当调用 `uv run` 时，uv 将忽略该项目。

**默认值**: `true`

**类型**: `bool`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
managed = false
```

---

## [`override-dependencies`](#override-dependencies) {: #override-dependencies }

解析项目依赖时应用的覆盖。

覆盖用于强制选择包的特定版本，而不管任何其他包请求的版本如何，也不管选择该版本是否通常构成无效解析。

虽然约束是_累加的_，即它们与组成包的要求相结合，但覆盖是_绝对的_，即它们完全替换任何组成包的要求。

将包包含为覆盖将_不会_自行触发该包的安装；相反，该包必须在项目的一阶或传递依赖中的其他地方被请求。

!!! note
    在 `uv lock`、`uv sync` 和 `uv run` 中，uv 只会从工作空间根目录的 `pyproject.toml` 读取 `override-dependencies`，并忽略其他工作空间成员或 `uv.toml` 文件中的任何声明。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 始终安装 Werkzeug 2.3.0，无论传递依赖请求哪个版本。
override-dependencies = ["werkzeug==2.3.0"]
```

---

## [`package`](#package) {: #package }

项目是否应被视为 Python 包，或非包（"虚拟"）项目。

包以可编辑模式构建并安装到虚拟环境中，因此需要构建后端，而虚拟项目_不_被构建或安装；相反，只有它们的依赖被包含在虚拟环境中。

创建包要求 `pyproject.toml` 中存在 `build-system`，并且项目结构符合构建后端的期望（例如，`src` 布局）。

**默认值**: `true`

**类型**: `bool`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
package = false
```

---

## [`required-environments`](#required-environments) {: #required-environments }

缺少源发行版的包所需的环境列表。

当包没有源发行版时，其可用性将限于其构建发行版（wheel）支持的平台。例如，如果包仅为 Linux 发布 wheel，那么它在 macOS 或 Windows 上将无法安装。

默认情况下，uv 要求每个包至少包含一个与指定 Python 版本兼容的 wheel。`required-environments` 设置可用于确保最终解析包含特定平台的 wheel，或者在没有此类 wheel 可用时失败。

虽然 `environments` 设置_限制_了 uv 在解析依赖时将考虑的环境集，但 `required-environments` _扩展_了 uv 在解析依赖时_必须_支持的平台集。

例如，`environments = ["sys_platform == 'darwin'"]` 将限制 uv 仅为 macOS 解析（忽略 Linux 和 Windows）。另一方面，`required-environments = ["sys_platform == 'darwin'"]` 将_要求_任何没有源发行版的包包含一个用于 macOS 的 wheel 才能安装。

**默认值**: `[]`

**类型**: `str | list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv]
# 要求包可用于 macOS ARM 和 x86（Intel）。
required-environments = [
    "sys_platform == 'darwin' and platform_machine == 'arm64'",
    "sys_platform == 'darwin' and platform_machine == 'x86_64'",
]
```

---

## [`sources`](#sources) {: #sources }

解析依赖时使用的源。

`tool.uv.sources` 使用附加源丰富依赖元数据，这些源在开发期间被纳入。依赖源可以是 Git 存储库、URL、本地路径或替代注册表。

有关更多信息，请参阅 [依赖项](../concepts/projects/dependencies.md)。

**默认值**: `{}`

**类型**: `dict`

**示例用法**:

```toml title="pyproject.toml"

[tool.uv.sources]
httpx = { git = "https://github.com/encode/httpx", tag = "0.27.0" }
pytest = { url = "https://files.pythonhosted.org/packages/6b/77/7440a06a8ead44c7757a64362dd22df5760f9b12dc5f11b6188cd2fc27a0/pytest-8.3.3-py3-none-any.whl" }
pydantic = { path = "/path/to/pydantic", editable = true }
```

---

## `build-backend`

uv 构建后端（`uv_build`）的设置。

请注意，这些设置仅在使用 `uv_build` 后端时适用，其他构建后端（如 hatchling）有自己的配置。

所有接受通配符的选项都使用来自 [PEP 639](https://packaging.python.org/en/latest/specifications/glob-patterns/) 的可移植通配符模式。

### [`data`](#build-backend_data) {: #build-backend_data }
<span id="data"></span>

wheel 的数据包含。

每个条目是一个目录，其内容被复制到 wheel 中对应的目录 `<name>-<version>.data/(purelib|platlib|headers|scripts|data)`。安装时，此数据根据 <https://docs.python.org/3.12/library/sysconfig.html#installation-paths> 的定义移动到其目标位置。通常，小数据文件通过将它们放在 Python 模块中来包含，而不是使用数据包含。

- `scripts`: 安装到可执行文件目录，在 Unix 上是 `<venv>/bin`，在 Windows 上是 `<venv>\Scripts`。当虚拟环境激活或使用 `uv run` 时，此目录被添加到 `PATH`，因此此数据类型可用于安装附加的二进制文件。对于 Python 入口点，请考虑改用 `project.scripts`。
- `data`: 安装到虚拟环境环境的根目录。

    警告：这可能会覆盖现有文件！

- `headers`: 安装到包含目录。构建使用此包作为构建要求的 Python 包的编译器使用包含目录查找附加头文件。
- `purelib` 和 `platlib`: 安装到 `site-packages` 目录。不建议使用这两个选项。

**默认值**: `{}`

**类型**: `dict[str, str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
data = { headers = "include/headers", scripts = "bin" }
```

---

### [`default-excludes`](#build-backend_default-excludes) {: #build-backend_default-excludes }
<span id="default-excludes"></span>

如果设置为 `false`，则不应用默认排除项。

默认排除项：`__pycache__`、`*.pyc` 和 `*.pyo`。

**默认值**: `true`

**类型**: `bool`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
default-excludes = false
```

---

### [`module-name`](#build-backend_module-name) {: #build-backend_module-name }
<span id="module-name"></span>

`module-root` 内的模块目录名称。

默认模块名称是包名，其中的点和破折号替换为下划线。

包名需要是有效的 Python 标识符，并且目录需要包含 `__init__.py`。存根包例外，其名称以 `-stubs` 结尾，词干是模块名，并且包含 `__init__.pyi` 文件。

对于具有单个模块的命名空间包，路径可以是点分的，例如 `foo.bar` 或 `foo-stubs.bar`。

对于具有多个模块的命名空间包，路径可以是列表，例如 `["foo", "bar"]`。我们建议每个包使用单个模块，将多个包拆分为工作空间。

请注意，使用此选项存在创建两个具有不同名称但具有相同模块名的包的风险。一起安装此类包会导致未指定的行为，通常是文件或目录树损坏。

**默认值**: `None`

**类型**: `str | list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-name = "sklearn"
```

---

### [`module-root`](#build-backend_module-root) {: #build-backend_module-root }
<span id="module-root"></span>

包含模块目录的目录。

常见值是 `src`（src 布局，默认值）或空路径（扁平布局）。

**默认值**: `"src"`

**类型**: `str`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
module-root = ""
```

---

### [`namespace`](#build-backend_namespace) {: #build-backend_namespace }
<span id="namespace"></span>

构建命名空间包。

构建 PEP 420 隐式命名空间包，允许多个根 `__init__.py`。

当命名空间包包含多个根 `__init__.py` 时使用此选项，对于具有单个根 `__init__.py` 的命名空间包，请改用点分的 `module-name`。

比较点分的 `module-name` 和 `namespace = true`，第一个示例可以用 `module-name = "cloud.database"` 表示：有一个根 `__init__.py` `database`。在第二个示例中，我们有三个根（`cloud.database`、`cloud.database_pro`、`billing.modules.database_pro`），因此需要 `namespace = true`。

```text
src
└── cloud
    └── database
        ├── __init__.py
        ├── query_builder
        │   └── __init__.py
        └── sql
            ├── parser.py
            └── __init__.py
```

```text
src
├── cloud
│   ├── database
│   │   ├── __init__.py
│   │   ├── query_builder
│   │   │   └── __init__.py
│   │   └── sql
│   │       ├── __init__.py
│   │       └── parser.py
│   └── database_pro
│       ├── __init__.py
│       └── query_builder.py
└── billing
    └── modules
        └── database_pro
            ├── __init__.py
            └── sql.py
```

**默认值**: `false`

**类型**: `bool`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
namespace = true
```

---

### [`source-exclude`](#build-backend_source-exclude) {: #build-backend_source-exclude }
<span id="source-exclude"></span>

从源发行版中排除的文件和目录的通配符表达式。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
source-exclude = ["*.bin"]
```

---

### [`source-include`](#build-backend_source-include) {: #build-backend_source-include }
<span id="source-include"></span>

附加包含在源发行版中的文件和目录的通配符表达式。

`pyproject.toml` 和模块目录的内容始终被包含。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
source-include = ["tests/**"]
```

---

### [`wheel-exclude`](#build-backend_wheel-exclude) {: #build-backend_wheel-exclude }
<span id="wheel-exclude"></span>

从 wheel 中排除的文件和目录的通配符表达式。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.build-backend]
wheel-exclude = ["*.bin"]
```

---

## `workspace`

### [`exclude`](#workspace_exclude) {: #workspace_exclude }
<span id="exclude"></span>

要排除作为工作空间成员的包。如果包同时匹配 `members` 和 `exclude`，它将被排除。

支持通配符和显式路径。

有关通配符语法的更多信息，请参阅 [`glob` 文档](https://docs.rs/glob/latest/glob/struct.Pattern.html)。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.workspace]
exclude = ["member1", "path/to/member2", "libs/*"]
```

---

### [`members`](#workspace_members) {: #workspace_members }
<span id="members"></span>

要包含作为工作空间成员的包。

支持通配符和显式路径。

有关通配符语法的更多信息，请参阅 [`glob` 文档](https://docs.rs/glob/latest/glob/struct.Pattern.html)。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

```toml title="pyproject.toml"
[tool.uv.workspace]
members = ["member1", "path/to/member2", "libs/*"]
```

---

# Configuration
## [`add-bounds`](#add-bounds) {: #add-bounds }

添加依赖时的默认版本限定符。

当向项目添加依赖时，如果未提供约束或 URL，则根据包的最新兼容版本添加约束。默认情况下，使用下限约束，例如 `>=1.2.3`。

当提供 `--frozen` 时，不执行解析，并且依赖总是无约束地添加。

此选项处于预览状态，可能在未来的任何版本中更改。

**默认值**: `"lower"`

**可能的值**:

- `"lower"`: 仅下限，例如 `>=1.2.3`
- `"major"`: 允许相同的主版本，类似于 semver 脱字符，例如 `>=1.2.3, <2.0.0`
- `"minor"`: 允许相同的次版本，类似于 semver 波浪号，例如 `>=1.2.3, <1.3.0`
- `"exact"`: 固定精确版本，例如 `==1.2.3`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    add-bounds = "major"
    ```
=== "uv.toml"

    ```toml
    add-bounds = "major"
    ```

---

## [`allow-insecure-host`](#allow-insecure-host) {: #allow-insecure-host }

允许与主机的不安全连接。

期望接收主机名（例如 `localhost`）、主机-端口对（例如 `localhost:8080`）或 URL（例如 `https://localhost`）。

警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 `--allow-insecure-host`，因为它绕过了 SSL 验证，可能使你暴露于 MITM 攻击。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    allow-insecure-host = ["localhost:8080"]
    ```
=== "uv.toml"

    ```toml
    allow-insecure-host = ["localhost:8080"]
    ```

---

## [`cache-dir`](#cache-dir) {: #cache-dir }

缓存目录的路径。

在 Linux 和 macOS 上默认为 `$XDG_CACHE_HOME/uv` 或 `$HOME/.cache/uv`，在 Windows 上默认为 `%LOCALAPPDATA%\uv\cache`。

**默认值**: `None`

**类型**: `str`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    cache-dir = "./.uv_cache"
    ```
=== "uv.toml"

    ```toml
    cache-dir = "./.uv_cache"
    ```

---

## [`cache-keys`](#cache-keys) {: #cache-keys }

缓存项目构建时要考虑的键。

缓存键使你能够指定在修改时应触发重建的文件或目录。默认情况下，只要项目目录中的 `pyproject.toml`、`setup.py` 或 `setup.cfg` 文件被修改，或者添加或删除了 `src` 目录，uv 就会重建项目，即：

```toml
cache-keys = [{ file = "pyproject.toml" }, { file = "setup.py" }, { file = "setup.cfg" }, { dir = "src" }]
```

例如：如果项目使用动态元数据从 `requirements.txt` 文件读取其依赖，你可以指定 `cache-keys = [{ file = "requirements.txt" }, { file = "pyproject.toml" }]` 以确保每当 `requirements.txt` 文件被修改时重建项目（除了监视 `pyproject.toml`）。

支持通配符，遵循 [`glob`](https://docs.rs/glob/0.3.1/glob/struct.Pattern.html) crate 的语法。例如，要使缓存每当项目目录或其任何子目录中的 `.toml` 文件被修改时失效，你可以指定 `cache-keys = [{ file = "**/*.toml" }]`。请注意，使用通配符可能代价高昂，因为 uv 可能需要遍历文件系统以确定是否有任何文件已更改。

缓存键还可以包括版本控制信息。例如，如果项目使用 `setuptools_scm` 从 Git 提交读取其版本，你可以指定 `cache-keys = [{ git = { commit = true }, { file = "pyproject.toml" }]` 以将当前 Git 提交哈希包含在缓存键中（除了 `pyproject.toml`）。Git 标签也通过 `cache-keys = [{ git = { commit = true, tags = true } }]` 支持。

缓存键还可以包括环境变量。例如，如果项目依赖 `MACOSX_DEPLOYMENT_TARGET` 或其他环境变量来确定其行为，你可以指定 `cache-keys = [{ env = "MACOSX_DEPLOYMENT_TARGET" }]` 以在环境变量更改时使缓存失效。

缓存键仅影响定义它们的 `pyproject.toml` 所定义的项目（与影响工作空间中的所有成员相对），并且所有路径和通配符都相对于项目目录解释。

**默认值**: `[{ file = "pyproject.toml" }, { file = "setup.py" }, { file = "setup.cfg" }]`

**类型**: `list[dict]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    cache-keys = [{ file = "pyproject.toml" }, { file = "requirements.txt" }, { git = { commit = true } }]
    ```
=== "uv.toml"

    ```toml
    cache-keys = [{ file = "pyproject.toml" }, { file = "requirements.txt" }, { git = { commit = true } }]
    ```

---

## [`check-url`](#check-url) {: #check-url }

检查索引 URL 以查找现有文件，跳过重复上传。

此选项允许重试仅在部分文件上传后失败的发布，并处理由于并行上传相同文件而导致的错误。

在上传之前，检查索引。如果索引中已存在完全相同的文件，则不会上传该文件。如果上传期间发生错误，再次检查索引，以处理并行上传两次相同文件的情况。

确切行为因索引而异。上传到 PyPI 时，即使没有 `--check-url`，上传相同文件也会成功，而大多数其他索引会出错。

索引必须提供受支持的哈希之一（SHA-256、SHA-384 或 SHA-512）。

**默认值**: `None`

**类型**: `str`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    check-url = "https://test.pypi.org/simple"
    ```
=== "uv.toml"

    ```toml
    check-url = "https://test.pypi.org/simple"
    ```

---

## [`compile-bytecode`](#compile-bytecode) {: #compile-bytecode }

安装后将 Python 文件编译为字节码。

默认情况下，uv 不会将 Python（`.py`）文件编译为字节码（`__pycache__/*.pyc`）；相反，编译在模块首次导入时延迟执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。

启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以保持一致性。与 pip 一样，它也会忽略错误。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    compile-bytecode = true
    ```
=== "uv.toml"

    ```toml
    compile-bytecode = true
    ```

---

## [`concurrent-builds`](#concurrent-builds) {: #concurrent-builds }

uv 在任何给定时间并发构建的源发行版的最大数量。

默认为可用 CPU 核心数。

**默认值**: `None`

**类型**: `int`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    concurrent-builds = 4
    ```
=== "uv.toml"

    ```toml
    concurrent-builds = 4
    ```

---

## [`concurrent-downloads`](#concurrent-downloads) {: #concurrent-downloads }

uv 在任何给定时间执行的并发下载的最大数量。

**默认值**: `50`

**类型**: `int`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    concurrent-downloads = 4
    ```
=== "uv.toml"

    ```toml
    concurrent-downloads = 4
    ```

---

## [`concurrent-installs`](#concurrent-installs) {: #concurrent-installs }

安装和解压包时使用的线程数。

默认为可用 CPU 核心数。

**默认值**: `None`

**类型**: `int`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    concurrent-installs = 4
    ```
=== "uv.toml"

    ```toml
    concurrent-installs = 4
    ```

---

## [`config-settings`](#config-settings) {: #config-settings }

传递给 [PEP 517](https://peps.python.org/pep-0517/) 构建后端的设置，指定为 `KEY=VALUE` 对。

**默认值**: `{}`

**类型**: `dict`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    config-settings = { editable_mode = "compat" }
    ```
=== "uv.toml"

    ```toml
    config-settings = { editable_mode = "compat" }
    ```

---

## [`config-settings-package`](#config-settings-package) {: #config-settings-package }

为特定包传递给 [PEP 517](https://peps.python.org/pep-0517/) 构建后端的设置，指定为 `KEY=VALUE` 对。

接受从包名到字符串键值对的映射。

**默认值**: `{}`

**类型**: `dict`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    config-settings-package = { numpy = { editable_mode = "compat" } }
    ```
=== "uv.toml"

    ```toml
    config-settings-package = { numpy = { editable_mode = "compat" } }
    ```

---

## [`dependency-metadata`](#dependency-metadata) {: #dependency-metadata }

项目依赖（直接或传递）的预定义静态元数据。当提供时，使解析器能够使用指定的元数据，而不是查询注册表或从源构建相关包。

元数据应根据 [Metadata 2.3](https://packaging.python.org/en/latest/specifications/core-metadata/) 标准提供，但仅以下字段被遵守：

- `name`: 包的名称。
- （可选）`version`: 包的版本。如果省略，元数据将应用于包的所有版本。
- （可选）`requires-dist`: 包的依赖（例如 `werkzeug>=0.14`）。
- （可选）`requires-python`: 包所需的 Python 版本（例如 `>=3.10`）。
- （可选）`provides-extra`: 包提供的扩展。

**默认值**: `[]`

**类型**: `list[dict]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    dependency-metadata = [
        { name = "flask", version = "1.0.0", requires-dist = ["werkzeug"], requires-python = ">=3.6" },
    ]
    ```
=== "uv.toml"

    ```toml
    dependency-metadata = [
        { name = "flask", version = "1.0.0", requires-dist = ["werkzeug"], requires-python = ">=3.6" },
    ]
    ```

---

## [`exclude-newer`](#exclude-newer) {: #exclude-newer }

将候选包限制为在给定时间点之前上传的包。

接受 [RFC 3339](https://www.rfc-editor.org/rfc/rfc3339.html) 的超集（例如 `2006-12-02T02:07:43Z`）。需要完整的时间戳以确保解析器在不同时区之间表现一致。

**默认值**: `None`

**类型**: `str`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    exclude-newer = "2006-12-02T02:07:43Z"
    ```
=== "uv.toml"

    ```toml
    exclude-newer = "2006-12-02T02:07:43Z"
    ```

---

## [`exclude-newer-package`](#exclude-newer-package) {: #exclude-newer-package }

将特定包的候选包限制为在给定日期之前上传的包。

接受字典格式的包-日期对。

**默认值**: `None`

**类型**: `dict`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    exclude-newer-package = { tqdm = "2022-04-04T00:00:00Z" }
    ```
=== "uv.toml"

    ```toml
    exclude-newer-package = { tqdm = "2022-04-04T00:00:00Z" }
    ```

---

## [`extra-build-dependencies`](#extra-build-dependencies) {: #extra-build-dependencies }

包的附加构建依赖。

这允许使用附加包扩展项目的依赖的 PEP 517 构建环境。这对于假定存在 `pip` 等包但未将它们声明为构建依赖的包非常有用。

**默认值**: `[]`

**类型**: `dict`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    extra-build-dependencies = { pytest = ["setuptools"] }
    ```
=== "uv.toml"

    ```toml
    extra-build-dependencies = { pytest = ["setuptools"] }
    ```

---

## [`extra-build-variables`](#extra-build-variables) {: #extra-build-variables }

构建某些包时要设置的额外环境变量。

环境变量将在构建指定包时添加到环境中。

**默认值**: `{}`

**类型**: `dict[str, dict[str, str]]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    extra-build-variables = { flash-attn = { FLASH_ATTENTION_SKIP_CUDA_BUILD = "TRUE" } }
    ```
=== "uv.toml"

    ```toml
    extra-build-variables = { flash-attn = { FLASH_ATTENTION_SKIP_CUDA_BUILD = "TRUE" } }
    ```

---

## [`extra-index-url`](#extra-index-url) {: #extra-index-url }

要使用的额外包索引 URL，除了 `--index-url`。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

通过此标志提供的所有索引优先于由 [`index_url`](#index-url) 或 [`index`](#index) 与 `default = true` 指定的索引。当提供多个索引时，较早的值优先。

要控制存在多个索引时 uv 的解析策略，请参阅 [`index_strategy`](#index-strategy)。

（已弃用：改用 `index`。）

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    extra-index-url = ["https://download.pytorch.org/whl/cpu"]
    ```
=== "uv.toml"

    ```toml
    extra-index-url = ["https://download.pytorch.org/whl/cpu"]
    ```

---

## [`find-links`](#find-links) {: #find-links }

搜索候选发行版的位置，除了注册表索引中找到的位置。

如果是路径，则目标必须是顶层包含 wheel 文件（`.whl`）或源发行版（例如 `.tar.gz` 或 `.zip`）的目录。

如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    find-links = ["https://download.pytorch.org/whl/torch_stable.html"]
    ```
=== "uv.toml"

    ```toml
    find-links = ["https://download.pytorch.org/whl/torch_stable.html"]
    ```

---

## [`fork-strategy`](#fork-strategy) {: #fork-strategy }

在 Python 版本和平台之间选择给定包的多个版本时使用的策略。

默认情况下，uv 将优化为每个支持的 Python 版本（`requires-python`）选择每个包的最新版本，同时最小化跨平台选择的版本数量。

在 `fewest` 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的较旧版本。

**默认值**: `"requires-python"`

**可能的值**:

- `"fewest"`: 优化为每个包选择最少数量的版本。如果较旧版本与更广泛支持的 Python 版本或平台兼容，则优先选择它们。
- `"requires-python"`: 优化为每个支持的 Python 版本选择每个包的最新支持版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    fork-strategy = "fewest"
    ```
=== "uv.toml"

    ```toml
    fork-strategy = "fewest"
    ```

---

## [`index`](#index) {: #index }

解析依赖时使用的包索引。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

索引按定义的顺序考虑，因此第一个定义的索引具有最高优先级。此外，通过此设置提供的索引比通过 [`index_url`](#index-url) 或 [`extra_index_url`](#extra-index-url) 指定的任何索引具有更高的优先级。除非指定了替代的[索引策略](#index-strategy)，否则 uv 只会考虑包含给定包的第一个索引。

如果索引被标记为 `explicit = true`，它将专门用于那些通过 `[tool.uv.sources]` 明确选择它的依赖，如下所示：

```toml
[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cu121"
explicit = true

[tool.uv.sources]
torch = { index = "pytorch" }
```

如果索引被标记为 `default = true`，它将被移动到优先级列表的末尾，以便在解析包时给予最低优先级。此外，将索引标记为默认值将禁用 PyPI 默认索引。

**默认值**: `"[]"`

**类型**: `dict`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [[tool.uv.index]]
    name = "pytorch"
    url = "https://download.pytorch.org/whl/cu121"
    ```
=== "uv.toml"

    ```toml
    [[tool.uv.index]]
    name = "pytorch"
    url = "https://download.pytorch.org/whl/cu121"
    ```

---

## [`index-strategy`](#index-strategy) {: #index-strategy }

针对多个索引 URL 进行解析时使用的策略。

默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（`first-index`）。这防止了"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。

**默认值**: `"first-index"`

**可能的值**:

- `"first-index"`: 仅使用第一个返回给定包名匹配结果的索引中的结果。
- `"unsafe-first-match"`: 在所有索引中搜索每个包名，耗尽第一个索引中的版本后再继续下一个。
- `"unsafe-best-match"`: 在所有索引中搜索每个包名，优先选择找到的"最佳"版本。如果包版本在多个索引中，仅查看第一个索引的条目。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    index-strategy = "unsafe-best-match"
    ```
=== "uv.toml"

    ```toml
    index-strategy = "unsafe-best-match"
    ```

---

## [`index-url`](#index-url) {: #index-url }

Python 包索引的 URL（默认为：<https://pypi.org/simple>）。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

通过此设置提供的索引比通过 [`extra_index_url`](#extra-index-url) 或 [`index`](#index) 指定的任何索引具有更低的优先级。

（已弃用：改用 `index`。）

**默认值**: `"https://pypi.org/simple"`

**类型**: `str`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    index-url = "https://test.pypi.org/simple"
    ```
=== "uv.toml"

    ```toml
    index-url = "https://test.pypi.org/simple"
    ```

---

## [`keyring-provider`](#keyring-provider) {: #keyring-provider }

尝试使用 `keyring` 进行索引 URL 的身份验证。

目前仅支持 `--keyring-provider subprocess`，它配置 uv 使用 `keyring` CLI 处理身份验证。

**默认值**: `"disabled"`

**类型**: `str`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    keyring-provider = "subprocess"
    ```
=== "uv.toml"

    ```toml
    keyring-provider = "subprocess"
    ```

---

## [`link-mode`](#link-mode) {: #link-mode }

从全局缓存安装包时使用的方法。

在 macOS 上默认为 `clone`（也称为写时复制），在 Linux 和 Windows 上默认为 `hardlink`。

警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（`uv cache clean`）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。

**默认值**: `"clone" (macOS) 或 "hardlink" (Linux, Windows)`

**可能的值**:

- `"clone"`: 从 wheel 克隆（即写时复制）包到 `site-packages` 目录。
- `"copy"`: 从 wheel 复制包到 `site-packages` 目录。
- `"hardlink"`: 从 wheel 硬链接包到 `site-packages` 目录。
- `"symlink"`: 从 wheel 符号链接包到 `site-packages` 目录。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    link-mode = "copy"
    ```
=== "uv.toml"

    ```toml
    link-mode = "copy"
    ```

---

## [`native-tls`](#native-tls) {: #native-tls }

是否从平台的本机证书存储加载 TLS 证书。

默认情况下，uv 从捆绑的 `webpki-roots` crate 加载证书。`webpki-roots` 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。

但是，在某些情况下，你可能希望使用平台的本机证书存储，特别是如果你依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    native-tls = true
    ```
=== "uv.toml"

    ```toml
    native-tls = true
    ```

---

## [`no-binary`](#no-binary) {: #no-binary }

不要安装预构建的 wheel。

给定的包将从源构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-binary = true
    ```
=== "uv.toml"

    ```toml
    no-binary = true
    ```

---

## [`no-binary-package`](#no-binary-package) {: #no-binary-package }

不要为特定包安装预构建的 wheel。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-binary-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    no-binary-package = ["ruff"]
    ```

---

## [`no-build`](#no-build) {: #no-build }

不要构建源发行版。

启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将出错退出。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-build = true
    ```
=== "uv.toml"

    ```toml
    no-build = true
    ```

---

## [`no-build-isolation`](#no-build-isolation) {: #no-build-isolation }

构建源发行版时禁用隔离。

假定 [PEP 518](https://peps.python.org/pep-0518/) 指定的构建依赖已安装。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-build-isolation = true
    ```
=== "uv.toml"

    ```toml
    no-build-isolation = true
    ```

---

## [`no-build-isolation-package`](#no-build-isolation-package) {: #no-build-isolation-package }

为特定包构建源发行版时禁用隔离。

假定包的 [PEP 518](https://peps.python.org/pep-0518/) 指定的构建依赖已安装。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-build-isolation-package = ["package1", "package2"]
    ```
=== "uv.toml"

    ```toml
    no-build-isolation-package = ["package1", "package2"]
    ```

---

## [`no-build-package`](#no-build-package) {: #no-build-package }

不要为特定包构建源发行版。

**默认值**: `[]`

**类型**: `list[str]`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-build-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    no-build-package = ["ruff"]
    ```

---

## [`no-cache`](#no-cache) {: #no-cache }

避免从缓存读取或写入缓存，而是在操作期间使用临时目录。

**默认值**: `false`

**类型**: `bool`

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-cache = true
    ```
=== "uv.toml"

    ```toml
    no-cache = true
    ```

---

## [`no-index`](#no-index) {: #no-index }

忽略所有注册表索引（例如 PyPI），而是依赖直接 URL 依赖和通过 `--find-links` 提供的依赖。

**默认值**: `false`

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-index = true
    ```
=== "uv.toml"

    ```toml
    no-index = true
    ```

---

## [`no-sources`](#no-sources) {: #no-sources }

解析依赖时忽略 `tool.uv.sources` 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何本地或 Git 源。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    no-sources = true
    ```
=== "uv.toml"

    ```toml
    no-sources = true
    ```

---

## [`offline`](#offline) {: #offline }

禁用网络访问，仅依赖本地缓存的数据和本地可用的文件。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    offline = true
    ```
=== "uv.toml"

    ```toml
    offline = true
    ```

---

## [`prerelease`](#prerelease) {: #prerelease }

考虑预发布版本时使用的策略。

默认情况下，uv 将接受_仅_发布预发布版本的包的预发布版本，以及在其声明的限定符中包含显式预发布标记的一阶要求（`if-necessary-or-explicit`）。

**默认值**: `"if-necessary-or-explicit"$

**可能的值**:

- `"disallow"`: 不允许所有预发布版本。
- `"allow"`: 允许所有预发布版本。
- `"if-necessary"`: 如果包的所有版本都是预发布版本，则允许预发布版本。
- `"explicit"`: 对于在其版本要求中具有显式预发布标记的一阶包，允许预发布版本。
- `"if-necessary-or-explicit"`: 如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    prerelease = "allow"
    ```
=== "uv.toml"

    ```toml
    prerelease = "allow"
    ```

---

## [`preview`](#preview) {: #preview }

是否启用实验性、预览功能。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    preview = true
    ```
=== "uv.toml"

    ```toml
    preview = true
    ```

---

## [`publish-url`](#publish-url) {: #publish-url }

发布包到 Python 包索引的 URL（默认为：<https://upload.pypi.org/legacy/>）。

**默认值**: `"https://upload.pypi.org/legacy/"$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    publish-url = "https://test.pypi.org/legacy/"
    ```
=== "uv.toml"

    ```toml
    publish-url = "https://test.pypi.org/legacy/"
    ```

---

## [`pypy-install-mirror`](#pypy-install-mirror) {: #pypy-install-mirror }

用于下载托管 PyPy 安装的镜像 URL。

默认情况下，托管 PyPy 安装从 [downloads.python.org](https://downloads.python.org/) 下载。可以设置此变量为镜像 URL 以使用不同的 PyPy 安装源。提供的 URL 将替换，例如，`https://downloads.python.org/pypy/pypy3.8-v7.3.7-osx64.tar.bz2` 中的 `https://downloads.python.org/pypy`。

可以通过使用 `file://` URL 方案从本地目录读取发行版。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    pypy-install-mirror = "https://downloads.python.org/pypy"
    ```
=== "uv.toml"

    ```toml
    pypy-install-mirror = "https://downloads.python.org/pypy"
    ```

---

## [`python-downloads`](#python-downloads) {: #python-downloads }

是否允许 Python 下载。

**默认值**: `"automatic"$

**可能的值**:

- `"automatic"`: 需要时自动下载托管 Python 安装。
- `"manual"`: 不自动下载托管 Python 安装；需要显式安装。
- `"never"`: 绝不允许 Python 下载。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    python-downloads = "manual"
    ```
=== "uv.toml"

    ```toml
    python-downloads = "manual"
    ```

---

## [`python-downloads-json-url`](#python-downloads-json-url) {: #python-downloads-json-url }

指向自定义 Python 安装 JSON 的 URL。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    python-downloads-json-url = "/etc/uv/python-downloads.json"
    ```
=== "uv.toml"

    ```toml
    python-downloads-json-url = "/etc/uv/python-downloads.json"
    ```

---

## [`python-install-mirror`](#python-install-mirror) {: #python-install-mirror }

下载托管 Python 安装的镜像 URL。

默认情况下，托管 Python 安装从 [`python-build-standalone`](https://github.com/astral-sh/python-build-standalone) 下载。可以设置此变量为镜像 URL 以使用不同的 Python 安装源。提供的 URL 将替换，例如，`https://github.com/astral-sh/python-build-standalone/releases/download/20240713/cpython-3.12.4%2B20240713-aarch64-apple-darwin-install_only.tar.gz` 中的 `https://github.com/astral-sh/python-build-standalone/releases/download`。

可以通过使用 `file://` URL 方案从本地目录读取发行版。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    python-install-mirror = "https://github.com/astral-sh/python-build-standalone/releases/download"
    ```
=== "uv.toml"

    ```toml
    python-install-mirror = "https://github.com/astral-sh/python-build-standalone/releases/download"
    ```

---

## [`python-preference`](#python-preference) {: #python-preference }

是优先使用系统上已存在的 Python 安装，还是优先使用由 uv 下载和安装的 Python 安装。

**默认值**: `"managed"$

**可能的值**:

- `"only-managed"`: 仅使用托管的 Python 安装；绝不使用系统 Python 安装。
- `"managed"`: 优先使用托管的 Python 安装而不是系统 Python 安装。
- `"system"`: 优先使用系统 Python 安装而不是托管的 Python 安装。
- `"only-system"`: 仅使用系统 Python 安装；绝不使用托管的 Python 安装。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    python-preference = "managed"
    ```
=== "uv.toml"

    ```toml
    python-preference = "managed"
    ```

---

## [`reinstall`](#reinstall) {: #reinstall }

重新安装所有包，无论它们是否已安装。隐含 `refresh`。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    reinstall = true
    ```
=== "uv.toml"

    ```toml
    reinstall = true
    ```

---

## [`reinstall-package`](#reinstall-package) {: #reinstall-package }

重新安装特定包，无论它是否已安装。隐含 `refresh-package`。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    reinstall-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    reinstall-package = ["ruff"]
    ```

---

## [`required-version`](#required-version) {: #required-version }

强制要求 uv 的版本。

如果在运行时 uv 的版本不符合要求，uv 将出错退出。

接受 [PEP 440](https://peps.python.org/pep-0440/) 限定符，如 `==0.5.0` 或 `>=0.5.0`。

**默认值**: `null$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    required-version = ">=0.5.0"
    ```
=== "uv.toml"

    ```toml
    required-version = ">=0.5.0"
    ```

---

## [`resolution`](#resolution) {: #resolution }

为给定包要求选择不同兼容版本时使用的策略。

默认情况下，uv 将使用每个包的最新兼容版本（`highest`）。

**默认值**: `"highest"$

**可能的值**:

- `"highest"`: 解析每个包的最高兼容版本。
- `"lowest"`: 解析每个包的最低兼容版本。
- `"lowest-direct"`: 解析任何直接依赖的最低兼容版本，以及任何传递依赖的最高兼容版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    resolution = "lowest-direct"
    ```
=== "uv.toml"

    ```toml
    resolution = "lowest-direct"
    ```

---

## [`trusted-publishing`](#trusted-publishing) {: #trusted-publishing }

配置可信发布。

默认情况下，uv 在受支持的环境中运行时检查可信发布，但如果未配置则忽略它。

uv 支持的可信发布环境包括 GitHub Actions 和 GitLab CI/CD。

**默认值**: `automatic$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    trusted-publishing = "always"
    ```
=== "uv.toml"

    ```toml
    trusted-publishing = "always"
    ```

---

## [`upgrade`](#upgrade) {: #upgrade }

允许包升级，忽略任何现有输出文件中的固定版本。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    upgrade = true
    ```
=== "uv.toml"

    ```toml
    upgrade = true
    ```

---

## [`upgrade-package`](#upgrade-package) {: #upgrade-package }

允许特定包的升级，忽略任何现有输出文件中的固定版本。

接受独立的包名（`ruff`）和版本限定符（`ruff<0.5.0`）。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv]
    upgrade-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    upgrade-package = ["ruff"]
    ```

---

## `pip`

特定于 `uv pip` 命令行的设置。

这些值在 `uv pip` 命名空间之外运行命令时将被忽略（例如 `uv lock`、`uvx`）。

### [`all-extras`](#pip_all-extras) {: #pip_all-extras }
<span id="all-extras"></span>

包含所有可选依赖。

仅适用于 `pyproject.toml`、`setup.py` 和 `setup.cfg` 源。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    all-extras = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    all-extras = true
    ```

---

### [`allow-empty-requirements`](#pip_allow-empty-requirements) {: #pip_allow-empty-requirements }
<span id="allow-empty-requirements"></span>

允许使用空要求的 `uv pip sync`，这将清除环境中的所有包。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    allow-empty-requirements = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    allow-empty-requirements = true
    ```

---

### [`annotation-style`](#pip_annotation-style) {: #pip_annotation-style }
<span id="annotation-style"></span>

输出文件中包含的注释注解的样式，用于指示每个包的来源。

**默认值**: `"split"$

**可能的值**:

- `"line"`: 在单行、逗号分隔的行上呈现注解。
- `"split"`: 在每个注解自己的行上呈现每个注解。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    annotation-style = "line"
    ```
=== "uv.toml"

    ```toml
    [pip]
    annotation-style = "line"
    ```

---

### [`break-system-packages`](#pip_break-system-packages) {: #pip_break-system-packages }
<span id="break-system-packages"></span>

允许 uv 修改 `EXTERNALLY-MANAGED` Python 安装。

警告：`--break-system-packages` 旨在用于持续集成（CI）环境中，当安装到由外部包管理器（如 `apt`）管理的 Python 安装时。应谨慎使用，因为此类 Python 安装明确建议不要由其他包管理器（如 uv 或 pip）修改。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    break-system-packages = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    break-system-packages = true
    ```

---

### [`compile-bytecode`](#pip_compile-bytecode) {: #pip_compile-bytecode }
<span id="compile-bytecode"></span>

安装后将 Python 文件编译为字节码。

默认情况下，uv 不会将 Python（`.py`）文件编译为字节码（`__pycache__/*.pyc`）；相反，编译在模块首次导入时延迟执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。

启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以保持一致性。与 pip 一样，它也会忽略错误。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    compile-bytecode = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    compile-bytecode = true
    ```

---

### [`config-settings`](#pip_config-settings) {: #pip_config-settings }
<span id="config-settings"></span>

传递给 [PEP 517](https://peps.python.org/pep-0517/) 构建后端的设置，指定为 `KEY=VALUE` 对。

**默认值**: `{}$

**类型**: `dict$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    config-settings = { editable_mode = "compat" }
    ```
=== "uv.toml"

    ```toml
    [pip]
    config-settings = { editable_mode = "compat" }
    ```

---

### [`config-settings-package`](#pip_config-settings-package) {: #pip_config-settings-package }
<span id="config-settings-package"></span>

为特定包传递给 [PEP 517](https://peps.python.org/pep-0517/) 构建后端的设置，指定为 `KEY=VALUE` 对。

**默认值**: `{}$

**类型**: `dict$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    config-settings-package = { numpy = { editable_mode = "compat" } }
    ```
=== "uv.toml"

    ```toml
    [pip]
    config-settings-package = { numpy = { editable_mode = "compat" } }
    ```

---

### [`custom-compile-command`](#pip_custom-compile-command) {: #pip_custom-compile-command }
<span id="custom-compile-command"></span>

包含在 `uv pip compile` 生成的输出文件顶部的头部注释。

用于反映包装 `uv pip compile` 的自定义构建脚本和命令。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    custom-compile-command = "./custom-uv-compile.sh"
    ```
=== "uv.toml"

    ```toml
    [pip]
    custom-compile-command = "./custom-uv-compile.sh"
    ```

---

### [`dependency-metadata`](#pip_dependency-metadata) {: #pip_dependency-metadata }
<span id="dependency-metadata"></span>

项目依赖（直接或传递）的预定义静态元数据。当提供时，使解析器能够使用指定的元数据，而不是查询注册表或从源构建相关包。

元数据应根据 [Metadata 2.3](https://packaging.python.org/en/latest/specifications/core-metadata/) 标准提供，但仅以下字段被遵守：

- `name`: 包的名称。
- （可选）`version`: 包的版本。如果省略，元数据将应用于包的所有版本。
- （可选）`requires-dist`: 包的依赖（例如 `werkzeug>=0.14`）。
- （可选）`requires-python`: 包所需的 Python 版本（例如 `>=3.10`）。
- （可选）`provides-extra`: 包提供的扩展。

**默认值**: `[]$

**类型**: `list[dict]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    dependency-metadata = [
        { name = "flask", version = "1.0.0", requires-dist = ["werkzeug"], requires-python = ">=3.6" },
    ]
    ```
=== "uv.toml"

    ```toml
    [pip]
    dependency-metadata = [
        { name = "flask", version = "1.0.0", requires-dist = ["werkzeug"], requires-python = ">=3.6" },
    ]
    ```

---

### [`emit-build-options`](#pip_emit-build-options) {: #pip_emit-build-options }
<span id="emit-build-options"></span>

在 `uv pip compile` 生成的输出文件中包含 `--no-binary` 和 `--only-binary` 条目。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    emit-build-options = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    emit-build-options = true
    ```

---

### [`emit-find-links`](#pip_emit-find-links) {: #pip_emit-find-links }
<span id="emit-find-links"></span>

在 `uv pip compile` 生成的输出文件中包含 `--find-links` 条目。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    emit-find-links = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    emit-find-links = true
    ```

---

### [`emit-index-annotation`](#pip_emit-index-annotation) {: #pip_emit-index-annotation }
<span id="emit-index-annotation"></span>

包含注释注解，指示用于解析每个包的索引（例如 `# from https://pypi.org/simple`）。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    emit-index-annotation = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    emit-index-annotation = true
    ```

---

### [`emit-index-url`](#pip_emit-index-url) {: #pip_emit-index-url }
<span id="emit-index-url"></span>

在 `uv pip compile` 生成的输出文件中包含 `--index-url` 和 `--extra-index-url` 条目。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    emit-index-url = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    emit-index-url = true
    ```

---

### [`emit-marker-expression`](#pip_emit-marker-expression) {: #pip_emit-marker-expression }
<span id="emit-marker-expression"></span>

是否发出一个标记字符串，指示固定依赖集有效的条件。

即使标记表达式为假，固定的依赖也可能有效，但当表达式为真时，要求已知是正确的。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    emit-marker-expression = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    emit-marker-expression = true
    ```

---

### [`exclude-newer`](#pip_exclude-newer) {: #pip_exclude-newer }
<span id="exclude-newer"></span>

将候选包限制为在给定时间点之前上传的包。

接受 [RFC 3339](https://www.rfc-editor.org/rfc/rfc3339.html) 的超集（例如 `2006-12-02T02:07:43Z`）。需要完整的时间戳以确保解析器在不同时区之间表现一致。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    exclude-newer = "2006-12-02T02:07:43Z"
    ```
=== "uv.toml"

    ```toml
    [pip]
    exclude-newer = "2006-12-02T02:07:43Z"
    ```

---

### [`exclude-newer-package`](#pip_exclude-newer-package) {: #pip_exclude-newer-package }
<span id="exclude-newer-package"></span>

将特定包的候选包限制为在给定日期之前上传的包。

接受字典格式的包-日期对。

**默认值**: `None$

**类型**: `dict$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    exclude-newer-package = { tqdm = "2022-04-04T00:00:00Z" }
    ```
=== "uv.toml"

    ```toml
    [pip]
    exclude-newer-package = { tqdm = "2022-04-04T00:00:00Z"
    }
    ```

---

### [`extra`](#pip_extra) {: #pip_extra }
<span id="extra"></span>

包含来自指定扩展的可选依赖；可以多次提供。

仅适用于 `pyproject.toml`、`setup.py` 和 `setup.cfg` 源。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    extra = ["dev", "docs"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    extra = ["dev", "docs"]
    ```

---

### [`extra-build-dependencies`](#pip_extra-build-dependencies) {: #pip_extra-build-dependencies }
<span id="extra-build-dependencies"></span>

包的附加构建依赖。

这允许使用附加包扩展项目的依赖的 PEP 517 构建环境。这对于假定存在 `pip` 等包但未将它们声明为构建依赖的包非常有用。

**默认值**: `[]$

**类型**: `dict$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    extra-build-dependencies = { pytest = ["setuptools"] }
    ```
=== "uv.toml"

    ```toml
    [pip]
    extra-build-dependencies = { pytest = ["setuptools"] }
    ```

---

### [`extra-build-variables`](#pip_extra-build-variables) {: #pip_extra-build-variables }
<span id="extra-build-variables"></span>

构建某些包时要设置的额外环境变量。

环境变量将在构建指定包时添加到环境中。

**默认值**: `{}$

**类型**: `dict[str, dict[str, str]]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    extra-build-variables = { flash-attn = { FLASH_ATTENTION_SKIP_CUDA_BUILD = "TRUE" } }
    ```
=== "uv.toml"

    ```toml
    [pip]
    extra-build-variables = { flash-attn = { FLASH_ATTENTION_SKIP_CUDA_BUILD = "TRUE" } }
    ```

---

### [`extra-index-url`](#pip_extra-index-url) {: #pip_extra-index-url }
<span id="extra-index-url"></span>

要使用的额外包索引 URL，除了 `--index-url`。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

通过此标志提供的所有索引优先于由 [`index_url`](#index-url) 指定的索引。当提供多个索引时，较早的值优先。

要控制存在多个索引时 uv 的解析策略，请参阅 [`index_strategy`](#index-strategy)。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    extra-index-url = ["https://download.pytorch.org/whl/cpu"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    extra-index-url = ["https://download.pytorch.org/whl/cpu"]
    ```

---

### [`find-links`](#pip_find-links) {: #pip_find-links }
<span id="find-links"></span>

搜索候选发行版的位置，除了注册表索引中找到的位置。

如果是路径，则目标必须是顶层包含 wheel 文件（`.whl`）或源发行版（例如 `.tar.gz` 或 `.zip`）的目录。

如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    find-links = ["https://download.pytorch.org/whl/torch_stable.html"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    find-links = ["https://download.pytorch.org/whl/torch_stable.html"]
    ```

---

### [`fork-strategy`](#pip_fork-strategy) {: #pip_fork-strategy }
<span id="fork-strategy"></span>

在 Python 版本和平台之间选择给定包的多个版本时使用的策略。

默认情况下，uv 将优化为每个支持的 Python 版本（`requires-python`）选择每个包的最新版本，同时最小化跨平台选择的版本数量。

在 `fewest` 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的较旧版本。

**默认值**: `"requires-python"$

**可能的值**:

- `"fewest"`: 优化为每个包选择最少数量的版本。如果较旧版本与更广泛支持的 Python 版本或平台兼容，则优先选择它们。
- `"requires-python"`: 优化为每个支持的 Python 版本选择每个包的最新支持版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    fork-strategy = "fewest"
    ```
=== "uv.toml"

    ```toml
    [pip]
    fork-strategy = "fewest"
    ```

---

### [`generate-hashes`](#pip_generate-hashes) {: #pip_generate-hashes }
<span id="generate-hashes"></span>

在输出文件中包含发行版哈希。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    generate-hashes = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    generate-hashes = true
    ```

---

### [`group`](#pip_group) {: #pip_group }
<span id="group"></span>

包含以下依赖组。

**默认值**: `None$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    group = ["dev", "docs"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    group = ["dev", "docs"]
    ```

---

### [`index-strategy`](#pip_index-strategy) {: #pip_index-strategy }
<span id="index-strategy"></span>

针对多个索引 URL 进行解析时使用的策略。

默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（`first-index`）。这防止了"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。

**默认值**: `"first-index"$

**可能的值**:

- `"first-index"`: 仅使用第一个返回给定包名匹配结果的索引中的结果。
- `"unsafe-first-match"`: 在所有索引中搜索每个包名，耗尽第一个索引中的版本后再继续下一个。
- `"unsafe-best-match"`: 在所有索引中搜索每个包名，优先选择找到的"最佳"版本。如果包版本在多个索引中，仅查看第一个索引的条目。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    index-strategy = "unsafe-best-match"
    ```
=== "uv.toml"

    ```toml
    [pip]
    index-strategy = "unsafe-best-match"
    ```

---

### [`index-url`](#pip_index-url) {: #pip_index-url }
<span id="index-url"></span>

Python 包索引的 URL（默认为：<https://pypi.org/simple>）。

接受符合 [PEP 503](https://peps.python.org/pep-0503/)（简单存储库 API）的存储库，或按相同格式布局的本地目录。

通过此设置提供的索引比通过 [`extra_index_url`](#extra-index-url) 指定的任何索引具有更低的优先级。

**默认值**: `"https://pypi.org/simple"$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    index-url = "https://test.pypi.org/simple"
    ```
=== "uv.toml"

    ```toml
    [pip]
    index-url = "https://test.pypi.org/simple"
    ```

---

### [`keyring-provider`](#pip_keyring-provider) {: #pip_keyring-provider }
<span id="keyring-provider"></span>

尝试使用 `keyring` 进行索引 URL 的身份验证。

目前仅支持 `--keyring-provider subprocess`，它配置 uv 使用 `keyring` CLI 处理身份验证。

**默认值**: `disabled$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    keyring-provider = "subprocess"
    ```
=== "uv.toml"

    ```toml
    [pip]
    keyring-provider = "subprocess"
    ```

---

### [`link-mode`](#pip_link-mode) {: #pip_link-mode }
<span id="link-mode"></span>

从全局缓存安装包时使用的方法。

在 macOS 上默认为 `clone`（也称为写时复制），在 Linux 和 Windows 上默认为 `hardlink`。

警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（`uv cache clean`）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。

**默认值**: `"clone" (macOS) 或 "hardlink" (Linux, Windows)`

**可能的值**:

- `"clone"`: 从 wheel 克隆（即写时复制）包到 `site-packages` 目录。
- `"copy"`: 从 wheel 复制包到 `site-packages` 目录。
- `"hardlink"`: 从 wheel 硬链接包到 `site-packages` 目录。
- `"symlink"`: 从 wheel 符号链接包到 `site-packages` 目录。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    link-mode = "copy"
    ```
=== "uv.toml"

    ```toml
    [pip]
    link-mode = "copy"
    ```

---

### [`no-annotate`](#pip_no-annotate) {: #pip_no-annotate }
<span id="no-annotate"></span>

从 `uv pip compile` 生成的输出文件中排除指示每个包来源的注释注解。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-annotate = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-annotate = true
    ```

---

### [`no-binary`](#pip_no-binary) {: #pip_no-binary }
<span id="no-binary"></span>

不要安装预构建的 wheel。

给定的包将从源构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。

可以提供多个包。使用 `:all:` 禁用所有包的二进制文件。
使用 `:none:` 清除先前指定的包。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-binary = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-binary = ["ruff"]
    ```

---

### [`no-build`](#pip_no-build) {: #pip_no-build }
<span id="no-build"></span>

不要构建源发行版。

启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将出错退出。

`--only-binary :all:` 的别名。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-build = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-build = true
    ```

---

### [`no-build-isolation`](#pip_no-build-isolation) {: #pip_no-build-isolation }
<span id="no-build-isolation"></span>

构建源发行版时禁用隔离。

假定 [PEP 518](https://peps.python.org/pep-0518/) 指定的构建依赖已安装。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-build-isolation = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-build-isolation = true
    ```

---

### [`no-build-isolation-package`](#pip_no-build-isolation-package) {: #pip_no-build-isolation-package }
<span id="no-build-isolation-package"></span>

为特定包构建源发行版时禁用隔离。

假定包的 [PEP 518](https://peps.python.org/pep-0518/) 指定的构建依赖已安装。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-build-isolation-package = ["package1", "package2"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-build-isolation-package = ["package1", "package2"]
    ```

---

### [`no-deps`](#pip_no-deps) {: #pip_no-deps }
<span id="no-deps"></span>

忽略包依赖，而是仅将命令行上明确列出的那些包添加到生成的要求文件中。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-deps = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-deps = true
    ```

---

### [`no-emit-package`](#pip_no-emit-package) {: #pip_no-emit-package }
<span id="no-emit-package"></span>

指定要从输出解析中省略的包。其依赖仍将包含在解析中。等效于 pip-compile 的 `--unsafe-package` 选项。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-emit-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-emit-package = ["ruff"]
    ```

---

### [`no-extra`](#pip_no-extra) {: #pip_no-extra }
<span id="no-extra"></span>

如果提供了 `all-extras`，则排除指定的可选依赖。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    all-extras = true
    no-extra = ["dev", "docs"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    all-extras = true
    no-extra = ["dev", "docs"]
    ```

---

### [`no-header`](#pip_no-header) {: #pip_no-header }
<span id="no-header"></span>

从 `uv pip compile` 生成的输出文件中排除顶部的注释头部。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-header = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-header = true
    ```

---

### [`no-index`](#pip_no-index) {: #pip_no-index }
<span id="no-index"></span>

忽略所有注册表索引（例如 PyPI），而是依赖直接 URL 依赖和通过 `--find-links` 提供的依赖。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-index = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-index = true
    ```

---

### [`no-sources`](#pip_no-sources) {: #pip_no-sources }
<span id="no-sources"></span>

解析依赖时忽略 `tool.uv.sources` 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何本地或 Git 源。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-sources = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-sources = true
    ```

---

### [`no-strip-extras`](#pip_no-strip-extras) {: #pip_no-strip-extras }
<span id="no-strip-extras"></span>

在输出文件中包含扩展。

默认情况下，uv 会剥离扩展，因为由扩展引入的任何包已经作为依赖直接包含在输出文件中。此外，使用 `--no-strip-extras` 生成的输出文件不能用作 `install` 和 `sync` 调用中的约束文件。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-strip-extras = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-strip-extras = true
    ```

---

### [`no-strip-markers`](#pip_no-strip-markers) {: #pip_no-strip-markers }
<span id="no-strip-markers"></span>

在 `uv pip compile` 生成的输出文件中包含环境标记。

默认情况下，uv 会剥离环境标记，因为 `compile` 生成的解析仅保证对目标环境正确。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    no-strip-markers = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    no-strip-markers = true
    ```

---

### [`only-binary`](#pip_only-binary) {: #pip_only-binary }
<span id="only-binary"></span>

仅使用预构建的 wheel；不要构建源发行版。

启用后，解析将不会运行来自给定包的代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将出错退出。

可以提供多个包。使用 `:all:` 禁用所有包的二进制文件。
使用 `:none:` 清除先前指定的包。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    only-binary = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    only-binary = ["ruff"]
    ```

---

### [`output-file`](#pip_output-file) {: #pip_output-file }
<span id="output-file"></span>

将 `uv pip compile` 生成的要求写入给定的 `requirements.txt` 文件。

如果文件已存在，则在解析依赖时将优先使用现有版本，除非还指定了 `--upgrade`。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    output-file = "requirements.txt"
    ```
=== "uv.toml"

    ```toml
    [pip]
    output-file = "requirements.txt"
    ```

---

### [`prefix`](#pip_prefix) {: #pip_prefix }
<span id="prefix"></span>

将包安装到指定目录下的 `lib`、`bin` 和其他顶级文件夹中，就像该位置存在虚拟环境一样。

通常， prefer 使用 `--python` 安装到备用环境中，因为通过 `--prefix` 安装的脚本和其他工件将引用安装解释器，而不是添加到 `--prefix` 目录的任何解释器，从而使它们不可移植。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    prefix = "./prefix"
    ```
=== "uv.toml"

    ```toml
    [pip]
    prefix = "./prefix"
    ```

---

### [`prerelease`](#pip_prerelease) {: #pip_prerelease }
<span id="prerelease"></span>

考虑预发布版本时使用的策略。

默认情况下，uv 将接受_仅_发布预发布版本的包的预发布版本，以及在其声明的限定符中包含显式预发布标记的一阶要求（`if-necessary-or-explicit`）。

**默认值**: `"if-necessary-or-explicit"$

**可能的值**:

- `"disallow"`: 不允许所有预发布版本。
- `"allow"`: 允许所有预发布版本。
- `"if-necessary"`: 如果包的所有版本都是预发布版本，则允许预发布版本。
- `"explicit"`: 对于在其版本要求中具有显式预发布标记的一阶包，允许预发布版本。
- `"if-necessary-or-explicit"`: 如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    prerelease = "allow"
    ```
=== "uv.toml"

    ```toml
    [pip]
    prerelease = "allow"
    ```

---

### [`python`](#pip_python) {: #pip_python }
<span id="python"></span>

应安装包的 Python 解释器。

默认情况下，uv 安装到当前工作目录或任何父目录中的虚拟环境中。`--python` 选项允许你指定不同的解释器，旨在用于持续集成（CI）环境或其他自动化工作流。

支持的格式：
- `3.10` 在 Windows 上查找注册表中安装的 Python 3.10（参见 `py --list-paths`），或在 Linux 和 macOS 上查找 `python3.10`。
- `python3.10` 或 `python.exe` 在 `PATH` 中查找具有给定名称的二进制文件。
- `/home/ferris/.local/bin/python3.10` 使用给定路径的确切 Python。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    python = "3.10"
    ```
=== "uv.toml"

    ```toml
    [pip]
    python = "3.10"
    ```

---

### [`python-platform`](#pip_python-platform) {: #pip_python-platform }
<span id="python-platform"></span>

应为其解析要求的平台。

表示为"目标三元组"，一个描述目标平台 CPU、供应商和操作系统名称的字符串，如 `x86_64-unknown-linux-gnu` 或 `aarch64-apple-darwin`。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    python-platform = "x86_64-unknown-linux-gnu"
    ```
=== "uv.toml"

    ```toml
    [pip]
    python-platform = "x86_64-unknown-linux-gnu"
    ```

---

### [`python-version`](#pip_python-version) {: #pip_python-version }
<span id="python-version"></span>

解析的要求应支持的最低 Python 版本（例如 `3.8` 或 `3.8.17`）。

如果省略补丁版本，则假定最小补丁版本。例如，`3.8` 映射到 `3.8.0`。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    python-version = "3.8"
    ```
=== "uv.toml"

    ```toml
    [pip]
    python-version = "3.8"
    ```

---

### [`reinstall`](#pip_reinstall) {: #pip_reinstall }
<span id="reinstall"></span>

重新安装所有包，无论它们是否已安装。隐含 `refresh`。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    reinstall = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    reinstall = true
    ```

---

### [`reinstall-package`](#pip_reinstall-package) {: #pip_reinstall-package }
<span id="reinstall-package"></span>

重新安装特定包，无论它是否已安装。隐含 `refresh-package`。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    reinstall-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    reinstall-package = ["ruff"]
    ```

---

### [`require-hashes`](#pip_require-hashes) {: #pip_require-hashes }
<span id="require-hashes"></span>

要求每个要求都有匹配的哈希。

哈希检查模式是全有或全无。如果启用，_所有_要求必须提供相应的哈希或哈希集。此外，如果启用，_所有_要求必须要么固定到精确版本（例如 `==1.0.0`），要么通过直接 URL 指定。

哈希检查模式引入了许多附加约束：

- 不支持 Git 依赖。
- 不支持可编辑安装。
- 不支持本地依赖，除非它们指向特定的 wheel（`.whl`）或源存档（`.zip`、`.tar.gz`），而不是目录。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    require-hashes = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    require-hashes = true
    ```

---

### [`resolution`](#pip_resolution) {: #pip_resolution }
<span id="resolution"></span>

为给定包要求选择不同兼容版本时使用的策略。

默认情况下，uv 将使用每个包的最新兼容版本（`highest`）。

**默认值**: `"highest"$

**可能的值**:

- `"highest"`: 解析每个包的最高兼容版本。
- `"lowest"`: 解析每个包的最低兼容版本。
- `"lowest-direct"`: 解析任何直接依赖的最低兼容版本，以及任何传递依赖的最高兼容版本。

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    resolution = "lowest-direct"
    ```
=== "uv.toml"

    ```toml
    [pip]
    resolution = "lowest-direct"
    ```

---

### [`strict`](#pip_strict) {: #pip_strict }
<span id="strict"></span>

验证 Python 环境，以检测具有缺失依赖和其他问题的包。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    strict = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    strict = true
    ```

---

### [`system`](#pip_system) {: #pip_system }
<span id="system"></span>

将包安装到系统 Python 环境中。

默认情况下，uv 安装到当前工作目录或任何父目录中的虚拟环境中。`--system` 选项指示 uv 改用系统 `PATH` 中找到的第一个 Python。

警告：`--system` 旨在用于持续集成（CI）环境中，应谨慎使用，因为它可以修改系统 Python 安装。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    system = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    system = true
    ```

---

### [`target`](#pip_target) {: #pip_target }
<span id="target"></span>

将包安装到指定目录中，而不是虚拟或系统 Python 环境中。包将安装在目录的顶层。

**默认值**: `None$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    target = "./target"
    ```
=== "uv.toml"

    ```toml
    [pip]
    target = "./target"
    ```

---

### [`torch-backend`](#pip_torch-backend) {: #pip_torch-backend }
<span id="torch-backend"></span>

获取 PyTorch 生态系统中的包时使用的后端。

设置后，uv 将忽略为 PyTorch 生态系统中的包配置的索引 URL，而是使用定义的后端。

例如，当设置为 `cpu` 时，uv 将使用仅 CPU 的 PyTorch 索引；当设置为 `cu126` 时，uv 将使用用于 CUDA 12.6 的 PyTorch 索引。

`auto` 模式将尝试根据当前安装的 CUDA 驱动程序检测适当的 PyTorch 索引。

此选项处于预览状态，可能在未来的任何版本中更改。

**默认值**: `null$

**类型**: `str$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    torch-backend = "auto"
    ```
=== "uv.toml"

    ```toml
    [pip]
    torch-backend = "auto"
    ```

---

### [`universal`](#pip_universal) {: #pip_universal }
<span id="universal"></span>

执行通用解析，尝试生成与所有操作系统、架构和 Python 实现兼容的单个 `requirements.txt` 输出文件。

在通用模式下，当前 Python 版本（或用户提供的 `--python-version`）将被视为下限。例如，`--universal --python-version 3.7` 将为 Python 3.7 及更高版本生成通用解析。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    universal = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    universal = true
    ```

---

### [`upgrade`](#pip_upgrade) {: #pip_upgrade }
<span id="upgrade"></span>

允许包升级，忽略任何现有输出文件中的固定版本。

**默认值**: `false$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    upgrade = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    upgrade = true
    ```

---

### [`upgrade-package`](#pip_upgrade-package) {: #pip_upgrade-package }
<span id="upgrade-package"></span>

允许特定包的升级，忽略任何现有输出文件中的固定版本。

接受独立的包名（`ruff`）和版本限定符（`ruff<0.5.0`）。

**默认值**: `[]$

**类型**: `list[str]$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    upgrade-package = ["ruff"]
    ```
=== "uv.toml"

    ```toml
    [pip]
    upgrade-package = ["ruff"]
    ```

---

### [`verify-hashes`](#pip_verify-hashes) {: #pip_verify-hashes }
<span id="verify-hashes"></span>

验证要求文件中提供的任何哈希。

与 `--require-hashes` 不同，`--verify-hashes` 不要求所有要求都有哈希；相反，它将仅限于验证那些确实包含哈希的要求的哈希。

**默认值**: `true$

**类型**: `bool$

**示例用法**:

=== "pyproject.toml"

    ```toml
    [tool.uv.pip]
    verify-hashes = true
    ```
=== "uv.toml"

    ```toml
    [pip]
    verify-hashes = true
    ```
