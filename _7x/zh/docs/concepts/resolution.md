# Resolution

Resolution（解析）是将需求列表转换为满足这些需求的包版本列表的过程。解析需要递归搜索兼容的包版本，确保所请求的需求得到满足，并且所请求包的需求是兼容的。

## Dependencies（依赖）

大多数项目和包都有依赖项。依赖项是当前包正常工作所需的其他包。包将其依赖项定义为 _requirements_（需求），大致是包名称和可接受版本的组合。当前项目定义的依赖项称为 _direct dependencies_（直接依赖）。当前项目的每个依赖项添加的依赖项称为 _indirect_ 或 _transitive dependencies_（间接或传递依赖）。

!!! note

    有关依赖项的详细信息，请参阅 Python 打包文档中的 [dependency specifiers page](https://packaging.python.org/en/latest/specifications/dependency-specifiers/)。

## Basic examples（基础示例）

为了帮助演示解析过程，请考虑以下依赖项：

<!-- prettier-ignore -->
- 项目依赖于 `foo` 和 `bar`。
- `foo` 有一个版本 1.0.0：
    - `foo 1.0.0` 依赖于 `lib>=1.0.0`。
- `bar` 有一个版本 1.0.0：
    - `bar 1.0.0` 依赖于 `lib>=2.0.0`。
- `lib` 有两个版本，1.0.0 和 2.0.0。两个版本都没有依赖项。

在此示例中，解析器必须找到一组满足项目需求的包版本。由于 `foo` 和 `bar` 都只有一个版本，因此将使用这些版本。解析还必须包括传递依赖项，因此必须选择一个 `lib` 的版本。`foo 1.0.0` 允许 `lib` 的所有可用版本，但 `bar 1.0.0` 需要 `lib>=2.0.0`，因此必须使用 `lib 2.0.0`。

在某些解析中，可能有多个有效的解决方案。考虑以下依赖项：

<!-- prettier-ignore -->
- 项目依赖于 `foo` 和 `bar`。
- `foo` 有两个版本，1.0.0 和 2.0.0：
    - `foo 1.0.0` 没有依赖项。
    - `foo 2.0.0` 依赖于 `lib==2.0.0`。
- `bar` 有两个版本，1.0.0 和 2.0.0：
    - `bar 1.0.0` 没有依赖项。
    - `bar 2.0.0` 依赖于 `lib==1.0.0`
- `lib` 有两个版本，1.0.0 和 2.0.0。两个版本都没有依赖项。

在此示例中，必须选择 `foo` 和 `bar` 的某个版本；但是，确定哪个版本需要考虑 `foo` 和 `bar` 每个版本的依赖项。`foo 2.0.0` 和 `bar 2.0.0` 不能一起安装，因为它们在所需的 `lib` 版本上存在冲突，因此解析器必须选择 `foo 1.0.0`（与 `bar 2.0.0` 一起）或 `bar 1.0.0`（与 `foo 1.0.0` 一起）。两者都是有效的解决方案，不同的解析算法可能会产生任一结果。

## Platform markers（平台标记）

标记允许向需求附加一个表达式，指示何时应使用该依赖项。例如 `bar ; python_version < "3.9"` 表示 `bar` 应仅安装在 Python 3.9 及更早版本上。

标记用于根据当前环境或平台调整包的依赖项。例如，标记可用于根据操作系统、CPU 架构、Python 版本、Python 实现等修改依赖项。

!!! note

    有关标记的更多详细信息，请参阅 Python 打包文档中的 [environment markers](https://packaging.python.org/en/latest/specifications/dependency-specifiers/#environment-markers) 部分。

标记对于解析很重要，因为它们的值会改变所需的依赖项。通常，Python 包解析器使用 _当前_ 平台的标记来确定要使用哪些依赖项，因为包通常正被 _安装_ 到当前平台上。然而，对于 _锁定_ 依赖项，这存在问题 —— lockfile 将仅适用于使用创建 lockfile 的同一平台的开发人员。为了解决这个问题，存在与平台无关或"通用"的解析器。

uv 同时支持 [平台特定解析](#platform-specific-resolution) 和 [通用解析](#universal-resolution)。

## Platform-specific resolution（平台特定解析）

默认情况下，uv 的 pip 接口，即 [`uv pip compile`](../pip/compile.md)，会产生一个平台特定的解析，类似于 `pip-tools`。无法在 uv 的项目接口中使用平台特定解析。

uv 还支持使用 `--python-platform` 和 `--python-version` 选项为特定的、替代的平台和 Python 版本进行解析。例如，如果在 macOS 上使用 Python 3.12，可以使用 `uv pip compile --python-platform linux --python-version 3.10 requirements.in` 来为 Linux 上的 Python 3.10 生成解析。与通用解析不同，在平台特定解析期间，提供的 `--python-version` 是要使用的确切 Python 版本，而不是下限。

!!! note

    Python 的环境标记暴露的关于当前机器的信息远多于简单的 `--python-platform` 参数所能表达的。例如，macOS 上的 `platform_version` 标记包括内核构建的时间，这（理论上）可以编码在包需求中。uv 的解析器尽最大努力生成一个与目标 `--python-platform` 上运行的任何机器兼容的解析，这对于大多数用例应该足够了，但对于复杂的包和平台组合可能会损失保真度。

## Universal resolution（通用解析）

uv 的 lockfile (`uv.lock`) 是使用通用解析创建的，并且跨平台可移植。这确保了为项目工作的每个人的依赖项都被锁定，无论操作系统、架构和 Python 版本如何。uv lockfile 由 [project](../concepts/projects/index.md) 命令创建和修改，例如 `uv lock`、`uv sync` 和 `uv add`。

通用解析在 uv 的 pip 接口中也可用，即 [`uv pip compile`](../pip/compile.md)，通过 `--universal` 标志。生成的 requirements 文件将包含标记，以指示每个依赖项适用于哪个平台。

在通用解析期间，如果一个包需要针对不同平台使用不同的版本或 URL，它可能会被多次列出 —— 标记将决定使用哪个版本。通用解析通常比平台特定解析更具约束性，因为我们需要考虑所有标记的需求。

在通用解析期间，所有必需的包必须与 `pyproject.toml` 中声明的 `requires-python` 的 _整个_ 范围兼容。例如，如果项目的 `requires-python` 是 `>=3.8`，并且给定依赖项的所有版本都需要 Python 3.9 或更高版本，则解析将失败，因为该依赖项缺少适用于（例如）Python 3.8（项目支持范围的下限）的可用版本。换句话说，项目的 `requires-python` 必须是其所有依赖项的 `requires-python` 的子集。

当为给定依赖项选择兼容版本时，uv 将（[默认情况下](#multi-version-resolution)）尝试为每个受支持的 Python 版本选择最新的兼容版本。例如，如果项目的 `requires-python` 是 `>=3.8`，并且依赖项的最新版本需要 Python 3.9 或更高版本，而所有先前的版本支持 Python 3.8，则解析器将为运行 Python 3.9 或更高版本的用户选择最新版本，并为运行 Python 3.8 的用户选择先前的版本。

在评估依赖项的 `requires-python` 范围时，uv 仅考虑下限并完全忽略上限。例如，`>=3.8, <4` 被视为 `>=3.8`。遵循 `requires-python` 的上限通常会导致形式上正确但实际上不正确的解析，因为，例如，解析器将回溯到第一个发布时省略上限的版本（参见：[`Requires-Python` upper limits](https://discuss.python.org/t/requires-python-upper-limits/12663)）。

## Limited resolution environments（受限解析环境）

默认情况下，通用解析器尝试为所有平台和 Python 版本求解。

如果你的项目仅支持有限的平台或 Python 版本集，你可以通过 `environments` 设置来约束求解的平台集，该设置接受一个 [PEP 508 环境标记](https://packaging.python.org/en/latest/specifications/dependency-specifiers/#environment-markers) 列表。换句话说，你可以使用 `environments` 设置来 _减少_ 受支持的平台集。

例如，要将 lockfile 限制为 macOS 和 Linux，并避免为 Windows 求解：

```toml title="pyproject.toml"
[tool.uv]
environments = [
    "sys_platform == 'darwin'",
    "sys_platform == 'linux'",
]
```

或者，避免为替代的 Python 实现求解：

```toml title="pyproject.toml"
[tool.uv]
environments = [
    "implementation_name == 'cpython'"
]
```

`environments` 设置中的条目必须是不相交的（即，它们不能重叠）。例如，`sys_platform == 'darwin'` 和 `sys_platform == 'linux'` 是不相交的，但 `sys_platform == 'darwin'` 和 `python_version >= '3.9'` 不是，因为两者可能同时为真。

## Required environments（必需环境）

在 Python 生态系统中，包可以作为源代码分发、构建分发（wheel）或两者发布；但要安装一个包，需要构建分发。如果一个包缺少构建分发，或者缺少当前平台或 Python 版本的构建分发（构建分发通常是平台特定的），uv 将尝试从源代码构建该包，然后安装生成的构建分发。

一些包（如 PyTorch）发布构建分发，但省略了源代码分发。这样的包 _仅_ 在提供了构建分发的平台上可安装。例如，如果一个包为 Linux 发布了构建分发，但没有为 macOS 或 Windows 发布，那么该包将 _仅_ 在 Linux 上可安装。

缺少源代码分发的包会给通用解析带来问题，因为通常至少会有一个平台或 Python 版本无法安装该包。

默认情况下，uv 要求每个这样的包至少包含一个与目标 Python 版本兼容的 wheel。`required-environments` 设置可用于确保生成的解析包含特定平台的 wheel，或者在没有此类 wheel 可用时失败。该设置接受一个 [PEP 508 环境标记](https://packaging.python.org/en/latest/specifications/dependency-specifiers/#environment-markers) 列表。

虽然 `environments` 设置 _限制_ 了 uv 在解析依赖项时将考虑的环境集，但 `required-environments` _扩展_ 了 uv 在解析依赖项时 _必须_ 支持的平台集。

例如，`environments = ["sys_platform == 'darwin'"]` 会将 uv 限制为仅针对 macOS 求解（忽略 Linux 和 Windows）。另一方面，`required-environments = ["sys_platform == 'darwin'"]` 将 _要求_ 任何没有源代码分发的包都包含一个适用于 macOS 的 wheel 才能安装（如果没有这样的 wheel 可用则会失败）。

实际上，`required-environments` 对于声明对非最新平台的显式支持非常有用，因为这通常需要回溯到这些包最新发布版本之前的版本。例如，要保证任何仅提供构建分发的包都支持 Intel macOS：

```toml title="pyproject.toml"
[tool.uv]
required-environments = [
    "sys_platform == 'darwin' and platform_machine == 'x86_64'"
]
```

## Dependency preferences（依赖偏好）

如果解析输出文件存在，即 uv lockfile (`uv.lock`) 或 requirements 输出文件 (`requirements.txt`)，uv 将 _优先_ 使用那里列出的依赖版本。类似地，如果要将包安装到虚拟环境中，uv 将优先使用已安装的版本（如果存在）。这意味着，除非请求了不兼容的版本或使用 `--upgrade` 明确请求升级，否则锁定的或已安装的版本不会更改。

## Resolution strategy（解析策略）

默认情况下，uv 尝试使用每个包的最新版本。例如，`uv pip install flask>=2.0.0` 将安装 Flask 的最新版本，例如 3.0.0。如果 `flask>=2.0.0` 是项目的依赖项，则只会使用 `flask` 3.0.0。这很重要，例如，因为运行测试不会检查项目是否实际上与其声明的 `flask` 2.0.0 下限兼容。

使用 `--resolution lowest`，uv 将为所有依赖项（直接和间接（传递））安装最低可能的版本。或者，`--resolution lowest-direct` 将对所有直接依赖项使用最低兼容版本，而对所有其他依赖项使用最新兼容版本。uv 将始终对构建依赖项使用最新版本。

例如，给定以下 `requirements.in` 文件：

```python title="requirements.in"
flask>=2.0.0
```

运行 `uv pip compile requirements.in` 将产生以下 `requirements.txt` 文件：

```python title="requirements.txt"
# This file was autogenerated by uv via the following command:
#    uv pip compile requirements.in
blinker==1.7.0
    # via flask
click==8.1.7
    # via flask
flask==3.0.0
itsdangerous==2.1.2
    # via flask
jinja2==3.1.2
    # via flask
markupsafe==2.1.3
    # via
    #   jinja2
    #   werkzeug
werkzeug==3.0.1
    # via flask
```

但是，`uv pip compile --resolution lowest requirements.in` 将产生：

```python title="requirements.in"
# This file was autogenerated by uv via the following command:
#    uv pip compile requirements.in --resolution lowest
click==7.1.2
    # via flask
flask==2.0.0
itsdangerous==2.0.0
    # via flask
jinja2==3.0.0
    # via flask
markupsafe==2.0.0
    # via jinja2
werkzeug==2.0.0
    # via flask
```

发布库时，建议在持续集成中分别使用 `--resolution lowest` 或 `--resolution lowest-direct` 运行测试，以确保与声明的下限兼容。

## Pre-release handling（预发布版本处理）

默认情况下，uv 在以下两种情况下会在依赖解析期间接受预发布版本：

1. 如果该包是直接依赖项，并且其版本说明符包含预发布说明符（例如，`flask>=2.0.0rc1`）。
1. 如果包 _所有_ 已发布的版本都是预发布版本。

如果由于传递性预发布导致依赖解析失败，uv 将提示使用 `--prerelease allow` 以允许所有依赖项的预发布版本。

或者，可以将传递依赖项添加为 [约束](#dependency-constraints) 或直接依赖项（即在 `requirements.in` 或 `pyproject.toml` 中），并带有预发布版本说明符（例如，`flask>=2.0.0rc1`）以选择加入对该特定依赖项的预发布支持。

预发布版本是
[ notoriously difficult](https://pubgrub-rs-guide.netlify.app/limitations/prerelease_versions) 建模的，并且是其他打包工具中频繁出现错误的来源。uv 的预发布处理是 _有意_ 受限的，并且需要用户选择加入预发布以确保正确性。

更多详细信息，请参阅 [Pre-release compatibility](../pip/compatibility.md#pre-release-compatibility)。

## Multi-version resolution（多版本解析）

在通用解析期间，一个包可能会在同一 lockfile 中多次列出不同的版本或 URL，因为不同的平台或 Python 版本可能需要不同的版本。

`--fork-strategy` 设置可用于控制 uv 如何在 (1) 最小化所选版本数量和 (2) 为每个平台选择最新可能版本之间进行权衡。前者导致跨平台的一致性更高，而后者导致在可能的情况下使用更新的包版本。

默认情况下（`--fork-strategy requires-python`），uv 将优化为每个受支持的 Python 版本选择每个包的最新版本，同时最小化跨平台所选版本的数量。

例如，当使用 Python 要求 `>=3.8` 解析 `numpy` 时，uv 将选择以下版本：

```txt
numpy==1.24.4 ; python_version == "3.8"
numpy==2.0.2 ; python_version == "3.9"
numpy==2.2.0 ; python_version >= "3.10"
```

此解析反映了 NumPy 2.2.0 及更高版本需要至少 Python 3.10，而早期版本与 Python 3.8 和 3.9 兼容的事实。

在 `--fork-strategy fewest` 下，uv 将改为最小化每个包所选版本的数量，优先选择与更广泛支持的 Python 版本或平台兼容的较旧版本。

例如，在上述场景中，uv 将为所有 Python 版本选择 `numpy==1.24.4`，而不是为 Python 3.9 升级到 `numpy==2.0.2`，为 Python 3.10 及更高版本升级到 `numpy==2.2.0`。

## Dependency constraints（依赖约束）

与 pip 类似，uv 支持约束文件（`--constraint constraints.txt`），这些文件限制了给定包的可接受版本范围。约束文件类似于需求文件，但仅作为约束列出不会导致包被包含在解析中。相反，只有当请求的包已经作为直接或传递依赖项被引入时，约束才会生效。约束对于减少传递依赖项的可用版本范围很有用。它们还可以用于使解析与其他一组已解析版本保持同步，无论两个集合之间有哪些包重叠。

## Dependency overrides（依赖覆盖）

依赖覆盖允许通过覆盖包的声明依赖项来绕过不成功或不理想的解析。当你知道依赖项与包的某个版本兼容，尽管元数据指示不兼容时，覆盖是一个有用的最后手段。

例如，如果一个传递依赖项声明了需求 `pydantic>=1.0,<2.0`，但确实与 `pydantic>=2.0` 兼容，用户可以通过在覆盖中包含 `pydantic>=1.0,<3` 来覆盖声明的依赖项，从而允许解析器选择更新版本的 `pydantic`。

具体来说，如果 `pydantic>=1.0,<3` 作为覆盖包含，uv 将忽略所有关于 `pydantic` 的声明需求，用覆盖替换它们。在上面的例子中，`pydantic>=1.0,<2.0` 需求将被完全忽略，并替换为 `pydantic>=1.0,<3`。

虽然约束只能 _减少_ 包的可接受版本集，但覆盖可以 _扩展_ 可接受版本集，为错误的上限版本提供逃生舱口。与约束一样，覆盖不会添加对包的依赖项，并且仅当包在直接或传递依赖项中被请求时才生效。

在 `pyproject.toml` 中，使用 `tool.uv.override-dependencies` 来定义覆盖列表。在 pip 兼容接口中，可以使用 `--override` 选项传递与约束文件格式相同的文件。

如果为同一个包提供了多个覆盖，则必须使用 [标记](#platform-markers) 来区分它们。如果一个包有一个带标记的依赖项，在使用覆盖时，它会被无条件替换 —— 无论标记评估为真还是假都无关紧要。

## Dependency metadata（依赖元数据）

在解析期间，uv 需要解析它遇到的每个包的元数据，以确定其依赖项。此元数据通常作为包索引中的静态文件提供；但是，对于仅提供源代码分发的包，元数据可能无法预先获得。

在这种情况下，uv 必须构建包以确定其元数据（例如，通过调用 `setup.py`）。这可能会在解析期间引入性能损失。此外，它要求包可以在所有平台上构建，这可能不成立。

例如，你可能有一个应该仅在 Linux 上构建和安装的包，但在 macOS 或 Windows 上无法成功构建。虽然 uv 可以为此场景构建一个完全有效的 lockfile，但这样做需要构建包，这将在非 Linux 平台上失败。

`tool.uv.dependency-metadata` 表可用于为此类依赖项预先提供静态元数据，从而允许 uv 跳过构建步骤并使用提供的元数据。

例如，要预先为 `chumpy` 提供元数据，请在其 `pyproject.toml` 中包含其 `dependency-metadata`：

```toml
[[tool.uv.dependency-metadata]]
name = "chumpy"
version = "0.70"
requires-dist = ["numpy>=1.8.1", "scipy>=0.13.0", "six>=1.11.0"]
```

这些声明旨在用于包 _不_ 预先声明静态元数据的情况，尽管它们对于需要 [禁用构建隔离](./projects/config.md#build-isolation) 的包也很有用。在这种情况下，预先声明包元数据可能比在解析包之前创建自定义构建环境更容易。

例如，过去版本的 `flash-attn` 没有声明静态元数据。通过预先声明 `flash-attn` 的元数据，uv 可以在不从源代码构建包（这本身需要安装 `torch`）的情况下解析 `flash-attn`：

```toml
[project]
name = "project"
version = "0.1.0"
requires-python = ">=3.12"
dependencies = ["flash-attn"]

[tool.uv.sources]
flash-attn = { git = "https://github.com/Dao-AILab/flash-attention", tag = "v2.6.3" }

[[tool.uv.dependency-metadata]]
name = "flash-attn"
version = "2.6.3"
requires-dist = ["torch", "einops"]
```

与依赖覆盖类似，`tool.uv.dependency-metadata` 也可用于包的元数据不正确或不完整，或者包在包索引中不可用的情况。虽然依赖覆盖允许全局覆盖包的可允许版本，但元数据覆盖允许覆盖 _特定包_ 的声明元数据。

!!! note

    `tool.uv.dependency-metadata` 中的 `version` 字段对于基于注册表的依赖项是可选的（如果省略，uv 将假定元数据适用于该包的所有版本），但对于直接 URL 依赖项（如 Git 依赖项）是 _必需的_。

`tool.uv.dependency-metadata` 表中的条目遵循 [Metadata 2.3](https://packaging.python.org/en/latest/specifications/core-metadata/) 规范，尽管 uv 仅读取 `name`、`version`、`requires-dist`、`requires-python` 和 `provides-extra`。`version` 字段也被视为可选。如果省略，元数据将用于指定包的所有版本。

## Conflicting dependencies（冲突依赖）

uv 要求项目声明的所有依赖项彼此兼容，并在创建 lockfile 时一起解析所有依赖项。这包括项目依赖项、可选依赖项（"extras"）和依赖组（开发依赖项）。

如果在一个 extra 中声明的依赖项与另一个 extra 中的依赖项不兼容，uv 将无法解析项目的需求并报错。例如，考虑两组相互冲突的可选依赖项：

```toml title="pyproject.toml"
[project.optional-dependencies]
extra1 = ["numpy==2.1.2"]
extra2 = ["numpy==2.0.0"]
```

如果你使用上述依赖项运行 `uv lock`，解析将失败：

```console
$ uv lock
  x No solution found when resolving dependencies:
  `-> Because myproject[extra2] depends on numpy==2.0.0 and myproject[extra1] depends on numpy==2.1.2, we can conclude that myproject[extra1] and
      myproject[extra2] are incompatible.
      And because your project requires myproject[extra1] and myproject[extra2], we can conclude that your projects's requirements are unsatisfiable.
```

为了解决这个问题，uv 支持显式声明冲突。如果你指定 `extra1` 和 `extra2` 是冲突的，uv 将分别解析它们。在 `tool.uv` 部分指定冲突：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { extra = "extra1" },
      { extra = "extra2" },
    ],
]
```

现在，运行 `uv lock` 将成功。但是，你现在不能同时安装 `extra1` 和 `extra2`：

```console
$ uv sync --extra extra1 --extra extra2
Resolved 3 packages in 14ms
error: extra `extra1`, extra `extra2` are incompatible with the declared conflicts: {`myproject[extra1]`, `myproject[extra2]`}
```

发生此错误是因为同时安装 `extra1` 和 `extra2` 会导致在同一环境中安装两个不同版本的包。

上述处理冲突可选依赖项的策略也适用于依赖组：

```toml title="pyproject.toml"
[dependency-groups]
group1 = ["numpy==2.1.2"]
group2 = ["numpy==2.0.0"]

[tool.uv]
conflicts = [
    [
      { group = "group1" },
      { group = "group2" },
    ],
]
```

与冲突 extras 的唯一区别是你需要使用 `group` 键而不是 `extra`。

当使用包含多个项目的工作区时，同样的限制适用 —— uv 要求所有工作区成员彼此兼容。类似地，可以跨工作区成员声明冲突。

例如，考虑以下工作区：

```toml title="member1/pyproject.toml"
[project]
name = "member1"

[project.optional-dependencies]
extra1 = ["numpy==2.1.2"]
```

```toml title="member2/pyproject.toml"
[project]
name = "member2"

[project.optional-dependencies]
extra2 = ["numpy==2.0.0"]
```

要声明这些不同工作区成员中 extras 之间的冲突，请使用 `package` 键：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { package = "member1", extra = "extra1" },
      { package = "member2", extra = "extra2" },
    ],
]
```

一个工作区成员的项目依赖项（即 `project.dependencies`）与另一个成员的 extra 发生冲突也是可能的，例如：

```toml title="member1/pyproject.toml"
[project]
name = "member1"
dependencies = ["numpy==2.1.2"]
```

```toml title="member2/pyproject.toml"
[project]
name = "member2"

[project.optional-dependencies]
extra2 = ["numpy==2.0.0"]
```

这个冲突也可以使用 `package` 键声明：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { package = "member1" },
      { package = "member2", extra = "extra2" },
    ],
]
```

类似地，某些工作区成员可能具有冲突的项目依赖项：

```toml title="member1/pyproject.toml"
[project]
name = "member1"
dependencies = ["numpy==2.1.2"]
```

```toml title="member2/pyproject.toml"
[project]
name = "member2"
dependencies = ["numpy==2.0.0"]
```

这个冲突也可以使用 `package` 键声明：

```toml title="pyproject.toml"
[tool.uv]
conflicts = [
    [
      { package = "member1" },
      { package = "member2" },
    ],
]
```

这些工作区成员将无法一起安装，例如，工作区根目录不能定义：

```toml title="pyproject.toml"
[project]
name = "root"
dependencies = ["member1", "member2"]
```

## Lower bounds（下限）

默认情况下，`uv add` 会向依赖项添加上限，并且当使用 uv 管理项目时，如果直接依赖项没有下限，uv 会发出警告。

下限在"快乐路径"中并不关键，但在存在依赖冲突的情况下非常重要。例如，考虑一个需要两个包的项目，并且这些包具有冲突的依赖项。解析器需要检查两个包约束范围内的所有版本组合 —— 如果所有组合都冲突，则会报告错误，因为依赖项不可满足。如果没有下限，解析器可以（并且经常）回溯到包的最旧版本。这不仅有问题，因为它速度慢，而且包的旧版本通常无法构建，或者解析器最终可能选择一个足够旧的版本，以至于它不依赖于冲突的包，但也不适用于你的代码。

在编写库时，下限尤其关键。声明你的库适用的每个依赖项的最低版本，并验证这些界限是否正确 —— 使用 [`--resolution lowest` 或 `--resolution lowest-direct`](#resolution-strategy) 进行测试。否则，用户可能会收到你的库的某个依赖项的旧版本、不兼容版本，并且库将因意外错误而失败。

## Reproducible resolutions（可重现的解析）

uv 支持 `--exclude-newer` 选项，以将解析限制在特定日期之前发布的分发版，从而允许无论新包发布如何都能重现安装。日期可以指定为 [RFC 3339](https://www.rfc-editor.org/rfc/rfc3339.html) 时间戳（例如，`2006-12-02T02:07:43Z`）或本地日期（相同格式，例如，`2006-12-02`），使用你系统配置的时区。

请注意，包索引必须支持 [`PEP 700`](https://peps.python.org/pep-0700/) 中指定的 `upload-time` 字段。如果给定分发版不存在该字段，则该分发版将被视为不可用。PyPI 为所有包提供 `upload-time`。

为确保可重现性，对于不可满足解析的消息不会提及由于 `--exclude-newer` 标志而排除了分发版 —— 较新的分发版将被视为不存在。

!!! note

    `--exclude-newer` 选项仅应用于从注册表读取的包（而不是，例如，Git 依赖项）。此外，当使用 `uv pip` 接口时，除非提供了 `--reinstall` 标志，否则 uv 不会降级先前安装的包，在这种情况下，uv 将执行新的解析。

## Source distribution（源代码分发）

[PEP 625](https://peps.python.org/pep-0625/) 规定包必须将源代码分发作为 gzip tarball (`.tar.gz`) 存档分发。在此规范之前，还允许其他需要向后兼容支持的存档格式。uv 支持读取和提取以下格式的存档：

- gzip tarball (`.tar.gz`, `.tgz`)
- bzip2 tarball (`.tar.bz2`, `.tbz`)
- xz tarball (`.tar.xz`, `.txz`)
- zstd tarball (`.tar.zst`)
- lzip tarball (`.tar.lz`)
- lzma tarball (`.tar.lzma`)
- zip (`.zip`)

## Lockfile versioning（Lockfile 版本控制）

`uv.lock` 文件使用版本化模式。模式版本包含在 lockfile 的 `version` 字段中。

任何给定版本的 uv 都可以读取和写入具有相同模式版本的 lockfile，但会拒绝具有更高模式版本的 lockfile。例如，如果你的 uv 版本支持模式 v1，那么如果遇到现有的模式 v2 的 lockfile，`uv lock` 将报错。

支持模式 v2 的 uv 版本 _可能_ 能够读取模式 v1 的 lockfile，如果模式更新是向后兼容的。但是，这不能保证，如果遇到模式版本过时的 lockfile，uv 可能会退出并报错。

模式版本被视为公共 API 的一部分，因此仅在次要版本中作为破坏性更改进行更新（参见 [Versioning](../reference/policies/versioning.md)）。因此，给定次要 uv 版本中的所有 uv 补丁版本都保证具有完整的 lockfile 兼容性。换句话说，lockfile 可能仅在跨次要版本时被拒绝。

lockfile 的 `revision` 字段用于跟踪 lockfile 的向后兼容更改。例如，向分发版添加新字段。修订版的更改不会导致旧版本的 uv 报错。

## Learn more（了解更多）

有关解析器内部结构的更多详细信息，请参阅 [resolver reference](../reference/internals/resolver.md) 文档。