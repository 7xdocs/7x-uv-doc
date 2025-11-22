
# 与 `pip` 和 `pip-tools` 的兼容性

uv 被设计为常见 `pip` 和 `pip-tools` 工作流的直接替代品。

非正式地说，其意图是让现有的 `pip` 和 `pip-tools` 用户可以在不改变其打包工作流核心内容的情况下切换到 uv；并且在大多数情况下，将 `pip install` 替换为 `uv pip install` 应该"直接工作"。

然而，uv _并不_ 旨在成为 `pip` 的 _精确_ 克隆，你越偏离常见的 `pip` 工作流，就越有可能遇到行为上的差异。在某些情况下，这些差异可能是已知且故意的；在其他情况下，它们可能是实现细节的结果；而在另一些情况下，它们可能是错误。

本文档概述了 uv 与 `pip` 之间的已知差异，包括原理、解决方法以及对未来兼容性的意图说明。

## 配置文件和环境变量

uv 不读取特定于 `pip` 的配置文件或环境变量，例如 `pip.conf` 或 `PIP_INDEX_URL`。

读取针对其他工具的配置文件和环境变量存在许多缺点：

1. 它需要与目标工具进行错误对错误的兼容性，因为用户最终会依赖格式、解析器等中的错误。
2. 如果目标工具以某种方式 _更改_ 了格式，那么 uv 就会被锁定必须以等效的方式更改。
3. 如果该配置以某种方式进行了版本控制，uv 需要知道用户期望使用目标工具的 _哪个版本_。
4. 它阻止 uv 引入目标工具中不存在的任何设置或配置，因为否则 `pip.conf`（或类似文件）将无法再与 `pip` 一起使用。
5. 它可能导致用户混淆，因为 uv 会读取实际上不影响其行为的设置，并且许多用户可能 _不_ 期望 uv 读取针对其他工具的配置文件。

相反，uv 支持其自己的环境变量，例如 `UV_INDEX_URL`。uv 还支持在 `uv.toml` 文件或 `pyproject.toml` 的 `[tool.uv.pip]` 部分中进行持久配置。有关更多信息，请参阅[配置文件](../concepts/configuration-files.md)。

## 预发布版本兼容性

默认情况下，uv 在两种情况下会在依赖解析期间接受预发布版本：

1. 如果包是直接依赖项，并且其版本标记包含预发布说明符（例如，`flask>=2.0.0rc1`）。
2. 如果包的 _所有_ 已发布版本都是预发布版本。

如果由于传递性预发布导致依赖解析失败，uv 将提示用户使用 `--prerelease allow` 重新运行，以允许所有依赖项使用预发布版本。

或者，你可以将传递性依赖项添加到你的 `requirements.in` 文件中，并带有预发布说明符（例如，`flask>=2.0.0rc1`），以选择加入对该特定依赖项的预发布支持。

总之，uv 需要预先知道解析器是否应该接受给定包的预发布版本。而 `pip`，_可能_ 会尊重传递性依赖项中的预发布标识符，这取决于解析器遇到相关说明符的顺序（[#1641](https://github.com/astral-sh/uv/issues/1641#issuecomment-1981402429)）。

预发布版本是
[众所周知的难以](https://pubgrub-rs-guide.netlify.app/limitations/prerelease_versions) 建模的，
并且是打包工具中常见的错误来源。即使被视为参考实现的 `pip`，在预发布处理方面也存在许多悬而未决的问题
（[#12469](https://github.com/pypa/pip/issues/12469),
[#12470](https://github.com/pypa/pip/issues/12470),
[#40505](https://discuss.python.org/t/handling-of-pre-releases-when-backtracking/40505/20), 等）。
uv 的预发布处理是 _有意_ 受限的，并且 _有意_ 要求用户选择加入预发布版本，以确保正确性。

将来，uv _可能_ 会支持传递性依赖项中的预发布标识符。然而，这很可能取决于 Python 打包规范的发展。现有的 PEP
[并未涵盖"依赖解析"](https://discuss.python.org/t/handling-of-pre-releases-when-backtracking/40505/17)，
而是侧重于 _单个_ 版本说明符的行为。因此，更广泛的打包生态系统中关于预发布的正确和预期行为存在未解决的问题。

## 存在于多个索引上的包

在 uv 和 `pip` 中，用户都可以指定多个包索引，以从中搜索给定包的可用版本。然而，uv 和 `pip` 在处理存在于多个索引上的包时有所不同。

例如，假设一家公司在私有索引 (`--extra-index-url`) 上发布了内部版本的 `requests`，但也默认允许从 PyPI 安装包。在这种情况下，私有的 `requests` 会与 PyPI 上的公共 [`requests`](https://pypi.org/project/requests/) 冲突。

当 uv 跨多个索引搜索包时，它会按顺序迭代索引（优先考虑 `--extra-index-url` 而不是默认索引），并在找到匹配项后立即停止搜索。这意味着如果一个包存在于多个索引上，uv 会将其候选版本限制在包含该包的第一个索引中存在的版本。

而 `pip` 则会合并来自所有索引的候选版本，并从合并的集合中选择最佳版本，尽管它
[不保证搜索索引的顺序](https://github.com/pypa/pip/issues/5045#issuecomment-369521345)，
并且期望包在名称和版本上是唯一的，即使跨索引也是如此。

uv 的行为是，如果一个包存在于内部索引上，它应该始终从内部索引安装，而不是从 PyPI 安装。其目的是防止"依赖混淆"
攻击，在这种攻击中，攻击者在 PyPI 上发布了一个与内部包同名的恶意包，从而导致安装恶意包而不是内部包。例如，参见
2022 年 12 月的 [`torchtriton` 攻击](https://pytorch.org/blog/compromised-nightly-dependency/)。

从 v0.1.39 开始，用户可以通过 `--index-strategy` 命令行选项或 `UV_INDEX_STRATEGY` 环境变量选择加入 `pip` 风格的多索引行为，该选项支持以下值：

- `first-index`（默认）：跨所有索引搜索每个包，将候选版本限制在包含该包的第一个索引中存在的版本，优先考虑 `--extra-index-url` 索引而不是默认索引 URL。
- `unsafe-first-match`：跨所有索引搜索每个包，但优先选择具有兼容版本的第一个索引，即使其他索引上有更新的版本。
- `unsafe-best-match`：跨所有索引搜索每个包，并从候选版本的合并集合中选择最佳版本。

虽然 `unsafe-best-match` 最接近 `pip` 的行为，但它使用户面临"依赖混淆"攻击的风险。

uv 还支持将包固定到专用索引（参见：[_索引_](../concepts/indexes.md#pinning-a-package-to-an-index)），使得给定的包 _总是_ 从特定索引安装。

## PEP 517 构建隔离

uv 默认使用 [PEP 517](https://peps.python.org/pep-0517/) 构建隔离（类似于 `pip install --use-pep517`），遵循 `pypa/build` 并预期 `pip` 将来会默认使用 PEP 517 构建（[pypa/pip#9175](https://github.com/pypa/pip/issues/9175)）。

如果一个包由于缺少构建时依赖项而安装失败，请尝试使用更新版本的包；如果问题仍然存在，请考虑向包维护者提交问题，请求他们更新打包设置以声明正确的 PEP 517 构建时依赖项。

作为一种应急方案，你可以预安装包的构建依赖项，然后使用 `--no-build-isolation` 运行 `uv pip install`，如下所示：

```shell
uv pip install wheel && uv pip install --no-build-isolation biopython==1.77
```

有关已知在 PEP 517 构建隔离下失败的包列表，请参阅 [#2252](https://github.com/astral-sh/uv/issues/2252)。

## 传递性 URL 依赖项

虽然 uv 包含对 URL 依赖项（例如，`ruff @ https://...`）的一流支持，但它在处理 _传递性_ URL 依赖项方面与 pip 有两个不同之处。

首先，uv 假设非 URL 依赖项不会将 URL 依赖项引入解析中。换句话说，它假设从注册表获取的依赖项本身不依赖于 URL。如果非 URL 依赖项 _确实_ 引入了 URL 依赖项，uv 将在解析期间拒绝该 URL 依赖项。（请注意，PyPI 不允许已发布的包依赖于 URL 依赖项；其他注册表可能更宽松。）

其次，如果使用直接 URL 依赖项定义了约束 (`--constraint`) 或覆盖 (`--override`)，并且被约束的包有自己的直接 URL 依赖项，那么如果该 URL 没有在输入需求集合的其他地方被引用，uv _可能_ 会在解析期间拒绝该传递性直接 URL 依赖项。

如果 uv 拒绝了传递性 URL 依赖项，最佳做法是将该 URL 依赖项作为直接依赖项提供给相关的 `pyproject.toml` 或 `requirement.in` 文件，因为上述约束不适用于直接依赖项。

## 默认使用虚拟环境

`uv pip install` 和 `uv pip sync` 设计为默认在虚拟环境中工作。

具体来说，uv 总是将包安装到当前激活的虚拟环境中，或者搜索当前目录或任何父目录中名为 `.venv` 的虚拟环境（即使它未激活）。

这与 `pip` 不同，如果没有虚拟环境被激活，`pip` 会将包安装到全局环境中，并且不会搜索未激活的虚拟环境。

在 uv 中，你可以通过 `--python /path/to/python` 选项提供 Python 可执行文件的路径，或者通过 `--system` 标志安装到非虚拟环境中，该标志会安装到 `PATH` 上找到的第一个 Python 解释器，就像 `pip` 一样。

换句话说，uv 反转了默认行为，需要明确选择加入才能安装到系统 Python 中，这可能导致损坏和其他复杂情况，应仅在有限情况下使用。

更多信息，请参阅 ["使用任意 Python 环境"](./environments.md#using-arbitrary-python-environments)。

## 解析策略

对于一组给定的依赖项说明符，通常没有单一的"正确"包集可以安装。相反，有许多有效的包集可以满足这些说明符。

`pip` 和 uv 都不对 _确切_ 安装的包集做出任何保证；只保证解析将是一致的、确定性的并且符合说明符。因此，在某些情况下，`pip` 和 uv 会产生不同的解析结果；然而，两种解析结果 _应该_ 都是同样有效的。

例如，考虑：

```python title="requirements.in"
starlette
fastapi
```

在撰写本文时，最新的 `starlette` 版本是 `0.37.2`，最新的 `fastapi` 版本是 `0.110.0`。然而，`fastapi==0.110.0` 也依赖于 `starlette`，并引入了一个上限：`starlette>=0.36.3,<0.37.0`。

如果解析器优先考虑包含最新版本的 `starlette`，则需要使用排除 `starlette` 上限的旧版本 `fastapi`。实际上，这需要回退到 `fastapi==0.1.17`：

```python title="requirements.txt"
# This file was autogenerated by uv via the following command:
#    uv pip compile requirements.in
annotated-types==0.6.0
    # via pydantic
anyio==4.3.0
    # via starlette
fastapi==0.1.17
idna==3.6
    # via anyio
pydantic==2.6.3
    # via fastapi
pydantic-core==2.16.3
    # via pydantic
sniffio==1.3.1
    # via anyio
starlette==0.37.2
    # via fastapi
typing-extensions==4.10.0
    # via
    #   pydantic
    #   pydantic-core
```

或者，如果解析器优先考虑包含最新版本的 `fastapi`，则需要使用满足上限的旧版本 `starlette`。实际上，这需要回退到 `starlette==0.36.3`：

```python title="requirements.txt"
# This file was autogenerated by uv via the following command:
#    uv pip compile requirements.in
annotated-types==0.6.0
    # via pydantic
anyio==4.3.0
    # via starlette
fastapi==0.110.0
idna==3.6
    # via anyio
pydantic==2.6.3
    # via fastapi
pydantic-core==2.16.3
    # via pydantic
sniffio==1.3.1
    # via anyio
starlette==0.36.3
    # via fastapi
typing-extensions==4.10.0
    # via
    #   fastapi
    #   pydantic
    #   pydantic-core
```

当 uv 的解析结果与 `pip` 出现不希望的差异时，这通常表明说明符过于宽松，用户应该考虑收紧它们。例如，在 `starlette` 和 `fastapi` 的情况下，用户可以要求 `fastapi>=0.110.0`。

## `pip check`

目前，`uv pip check` 将显示以下诊断信息：

- 包没有 `METADATA` 文件，或者 `METADATA` 文件无法解析。
- 包的 `Requires-Python` 与正在运行的解释器的 Python 版本不匹配。
- 包依赖于一个未安装的包。
- 包依赖于一个已安装但版本不兼容的包。
- 在虚拟环境中安装了多个版本的包。

在某些情况下，`uv pip check` 会显示 `pip check` 不显示的诊断信息，反之亦然。例如，与 `uv pip check` 不同，`pip check` 在环境中安装了多个版本的包时 _不会_ 警告。

## `--user` 和 `user` 安装方案

uv 不支持 `--user` 标志，该标志基于 `user` 安装方案安装包。相反，我们建议使用虚拟环境来隔离包安装。

此外，如果 pip 检测到用户没有目标目录的写入权限（例如在某些系统上安装到系统 Python 时），它会回退到 `user` 安装方案。uv 没有实现任何此类回退。

更多信息，请参见 [#2077](https://github.com/astral-sh/uv/issues/2077)。

## `--only-binary` 强制执行

`--only-binary` 参数用于限制仅安装预构建的二进制发行版。当提供 `--only-binary :all:` 时，pip 和 uv 都将拒绝从 PyPI 和其他注册表构建源发行版。

然而，当依赖项作为直接 URL 提供时（例如，`uv pip install https://...`），pip 并 _不_ 强制执行 `--only-binary`，并且会为所有此类包构建源发行版。

而 uv，则 _确实_ 对直接 URL 依赖项强制执行 `--only-binary`，但有一个例外：给定 `uv pip install https://... --only-binary flask`，如果 uv 无法提前推断出包名，它 _将_ 构建给定 URL 处的源发行版，因为在这种情况下，uv 无法在不构建其元数据的情况下确定该包是否"被允许"。

pip 和 uv 都允许在提供 `--only-binary` 时构建和安装可编辑需求。例如，`uv pip install -e . --only-binary :all:` 是允许的。

## `--no-binary` 强制执行

`--no-binary` 参数用于限制仅安装源发行版。当提供 `--no-binary` 时，uv 将拒绝安装预构建的二进制发行版，但 _会_ 重用本地缓存中已存在的任何二进制发行版。

此外，与 pip 相比，当提供 `--no-binary` 时，uv 的解析器仍会从预构建的二进制发行版中读取元数据。

## `manylinux_compatible` 强制执行

[PEP 600](https://peps.python.org/pep-0600/#package-installers) 描述了一种机制，Python 发行商可以通过在 `_manylinux` 标准库模块上定义 `manylinux_compatible` 函数来选择退出 `manylinux` 兼容性。

uv 尊重 `manylinux_compatible`，但仅针对当前的 glibc 版本进行测试，并全局应用 `manylinux_compatible` 的返回值。

换句话说，如果 `manylinux_compatible` 返回 `True`，uv 将系统视为 `manylinux` 兼容；如果返回 `False`，uv 将系统视为 `manylinux` 不兼容，而不会为每个 glibc 版本调用 `manylinux_compatible`。

这种方法并非规范的完整实现，但与常见的通用 `manylinux_compatible` 实现（如 [`no-manylinux`](https://pypi.org/project/no-manylinux/)）兼容：

```python
from __future__ import annotations
manylinux1_compatible = False
manylinux2010_compatible = False
manylinux2014_compatible = False


def manylinux_compatible(*_, **__):  # PEP 600
    return False
```

## 字节码编译

与 `pip` 不同，uv 默认不在安装期间将 `.py` 文件编译为 `.pyc` 文件（即，uv 不会创建或填充 `__pycache__` 目录）。要在安装期间启用字节码编译，请将 `--compile-bytecode` 标志传递给 `uv pip install` 或 `uv pip sync`，或者将 `UV_COMPILE_BYTECODE` 环境变量设置为 `1`。

跳过字节码编译在某些工作流中可能是不希望的；例如，我们建议在 [Docker 构建](../guides/integration/docker.md) 中启用字节码编译以提高启动时间（以增加构建时间为代价）。

由于字节码编译会抑制 Python 解释器发出的各种警告，在极少数情况下，你可能会在运行使用 uv 安装的 Python 代码时看到 `SyntaxWarning` 或 `DeprecationWarning` 消息，而这些消息在使用 `pip` 时不会出现。这些是有效的警告，但通常被字节码编译过程隐藏，可以通过在 uv 中启用字节码编译来忽略、在上游修复或类似地抑制这些警告。

## 严格性和规范执行

uv 往往比 `pip` 更严格，并且经常拒绝 `pip` 会安装的包。例如，uv 拒绝具有无效 URL 片段的 HTML 索引（参见：[PEP 503](https://peps.python.org/pep-0503/)），而 `pip` 会忽略此类片段。

在某些情况下，uv 为已知存在特定规范合规性问题的流行包实现了宽松的行为。

如果 uv 由于违反规范而拒绝安装 `pip` 会安装的包，最佳做法是首先尝试安装更新版本的包；如果失败，则向包维护者报告该问题。

## `pip` 命令行选项和子命令

uv 不支持 `pip` 的完整命令行选项和子命令集，尽管它支持一个很大的子集。

缺失的选项和子命令根据用户需求和实现的复杂性进行优先级排序，并倾向于在单独的问题中进行跟踪。例如：

- [`--trusted-host`](https://github.com/astral-sh/uv/issues/1339)
- [`--user`](https://github.com/astral-sh/uv/issues/2077)

如果你遇到缺失的选项或子命令，请搜索问题跟踪器以查看是否已报告，如果没有，请考虑打开一个新问题。请随时对任何现有问题进行投票以表达你的兴趣。

## 注册表认证

uv 不支持 `pip` 的 `auto` 或 `import` 选项（用于 `--keyring-provider`）。目前，仅支持 `subprocess` 选项。

与 `pip` 不同，uv 默认不启用密钥环认证。

与 `pip` 不同，uv 不会等到请求返回 HTTP 401 后才搜索认证。uv 会为所有具有可用凭据的主机的请求附加认证信息。

## `egg` 支持

uv 不支持 `pip` 中视为遗留或已弃用的功能。例如，uv 不支持 `.egg` 风格的分发包。

但是，uv 对 (1) `.egg-info` 风格的分发包（偶尔在 Docker 镜像和 Conda 环境中找到）和 (2) 遗留的可编辑 `.egg-link` 风格的分发包提供了部分支持。

具体来说，uv 不支持安装新的 `.egg-info` 或 `.egg-link` 风格的分发包，但会在解析期间尊重任何此类现有分发包，使用 `uv pip list` 和 `uv pip freeze` 列出它们，并使用 `uv pip uninstall` 卸载它们。

## 构建约束

当通过 `--constraint`（或 `UV_CONSTRAINT`）提供约束时，uv 在解析构建依赖项（即构建源发行版）时 _不会_ 应用这些约束。相反，构建约束应通过专用的 `--build-constraint`（或 `UV_BUILD_CONSTRAINT`）设置提供。

而 pip 在通过 `PIP_CONSTRAINT` 指定时会对构建依赖项应用约束，但在命令行上通过 `--constraint` 提供时则不会。

例如，要确保使用 `setuptools 60.0.0` 来构建任何具有 `setuptools` 构建依赖项的包，请使用 `--build-constraint`，而不是 `--constraint`。

## `pip compile` 默认值

`pip compile` 和 `pip-tools` 的默认行为存在一些微小但值得注意的差异。

默认情况下，uv 不会将编译后的需求写入输出文件。相反，uv 要求用户使用 `-o` 或 `--output-file` 选项明确指定输出文件。

默认情况下，uv 在输出编译后的需求时会剥离 extras。换句话说，uv 默认为 `--strip-extras`，而 `pip-compile` 默认为 `--no-strip-extras`。`pip-compile` 计划在下一个主要版本（v8.0.0）中更改此默认值，届时两个工具都将默认使用 `--strip-extras`。要在 uv 中保留 extras，请将 `--no-strip-extras` 标志传递给 `uv pip compile`。

默认情况下，uv 不会将任何索引 URL 写入输出文件，而 `pip-compile` 会输出任何与默认值（PyPI）不匹配的 `--index-url` 或 `--extra-index-url`。要在输出文件中包含索引 URL，请将 `--emit-index-url` 标志传递给 `uv pip compile`。与 `pip-compile` 不同，当传递 `--emit-index-url` 时，uv 将包含所有索引 URL，包括默认索引 URL。

## `requires-python` 上限

在评估依赖项的 `requires-python` 范围时，uv 只考虑下限而完全忽略上限。例如，`>=3.8, <4` 被视为 `>=3.8`。尊重 `requires-python` 的上限通常会导致形式上正确但实际上不正确的解析，因为，例如，解析器会回溯到第一个发布时省略了上限的版本（参见：[`Requires-Python` 上限限制](https://discuss.python.org/t/requires-python-upper-limits/12663)）。

## `requires-python` 说明符

在针对 `requires-python` 说明符评估 Python 版本时，uv 会将候选版本截断为主要、次要和补丁组件，忽略（例如）预发布和后发布标识符。

例如，声明 `requires-python: >=3.13` 的项目将接受 Python 3.13.0b1。虽然 3.13.0b1 并不严格大于 3.13，但当忽略预发布标识符时，它大于 3.13。

虽然这并不严格符合 [PEP 440](https://peps.python.org/pep-0440/)，但它 _确实_ 与
[pip](https://github.com/pypa/pip/blob/24.1.1/src/pip/_internal/resolution/resolvelib/candidates.py#L540) 一致。

## 包优先级

给定一组需求，通常有许多可能的解决方案，解析器必须在它们之间做出选择。uv 的解析器和 pip 的解析器具有不同的包优先级集。虽然两个解析器都使用用户提供的顺序作为其优先级之一，但 pip 具有 uv 没有的额外
[优先级](https://pip.pypa.io/en/stable/topics/more-dependency-resolution/#the-resolver-algorithm)。
因此，uv 比 pip 更容易受到用户顺序变化的影响。

例如，`uv pip install foo bar` 优先考虑 `foo` 的新版本而不是 `bar`，并可能导致与 `uv pip install bar foo` 不同的解析结果。类似地，此行为适用于 `uv pip compile` 输入文件中需求的排序。

## Wheel 文件名和元数据验证

默认情况下，uv 会拒绝那些文件名与文件内的 wheel 元数据不一致的 wheel。例如，一个名为 `foo-1.0.0-py3-none-any.whl` 但其内部元数据显示版本为 `1.0.1` 的 wheel 将被 uv 拒绝，但会被 pip 接受。

要强制 uv 接受此类 wheel，请在环境中设置 `UV_SKIP_WHEEL_FILENAME_CHECK=1`。

## 包名称规范化

默认情况下，uv 会将包名称规范化为其
[符合 PEP 503 的形式](https://packaging.python.org/en/latest/specifications/name-normalization/#name-normalization)，
并在所有输出上下文中使用这些规范化名称。这与 pip 不同，pip 倾向于保留注册表上发布的逐字包名称。

例如，`uv pip list` 显示规范化的包名称（例如，`docstring-parser`），而 `pip list` 显示非规范化的包名称（例如，`docstring_parser`）：

```shell
(venv) $ diff --side-by-side  <(pip list) <(uv pip list)
Package          Version					Package          Version
---------------- -------					---------------- -------
docstring_parser 0.16					      |	docstring-parser 0.16
jaraco.classes   3.4.0					      |	jaraco-classes   3.4.0
more-itertools   10.7.0				    		more-itertools   10.7.0
pip              25.1					    	pip              25.1
PyMuPDFb         1.24.10				      |	pymupdfb         1.24.10
PyPDF2           3.0.1					      |	pypdf2           3.0.1
```