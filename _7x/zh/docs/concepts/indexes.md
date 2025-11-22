# 包索引

默认情况下，uv 使用 [Python Package Index (PyPI)](https://pypi.org) 进行依赖解析和包安装。但是，uv 可以通过 `[[tool.uv.index]]` 配置选项（以及类似的命令行选项 `--index`）配置为使用其他包索引，包括私有索引。

## 定义索引

要在解析依赖项时包含额外的索引，请在你的 `pyproject.toml` 中添加一个 `[[tool.uv.index]]` 条目：

```toml
[[tool.uv.index]]
# 索引的可选名称。
name = "pytorch"
# 索引的必需 URL。
url = "https://download.pytorch.org/whl/cpu"
```

索引按照定义的顺序确定优先级，配置文件中列出的第一个索引是在解析依赖项时首先查询的索引，通过命令行提供的索引优先于配置文件中的索引。

默认情况下，uv 包含 Python Package Index (PyPI) 作为"默认"索引，即当在任何其他索引上找不到包时使用的索引。要从索引列表中排除 PyPI，请在另一个索引条目上设置 `default = true`（或使用 `--default-index` 命令行选项）：

```toml
[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cpu"
default = true
```

默认索引始终被视为最低优先级，无论它在索引列表中的位置如何。

索引名称只能包含字母数字字符、短划线、下划点和句点，并且必须是有效的 ASCII。

在命令行上（使用 `--index` 或 `--default-index`）或通过环境变量（`UV_INDEX` 或 `UV_DEFAULT_INDEX`）提供索引时，名称是可选的，但可以使用 `<name>=<url>` 语法包含，如下所示：

```shell
# 在命令行上。
$ uv lock --index pytorch=https://download.pytorch.org/whl/cpu
# 通过环境变量。
$ UV_INDEX=pytorch=https://download.pytorch.org/whl/cpu uv lock
```

## 将包固定到特定索引

可以通过在包的 `tool.uv.sources` 条目中指定索引，将包固定到特定索引。例如，要确保 `torch` *始终*从 `pytorch` 索引安装，请将以下内容添加到你的 `pyproject.toml`：

```toml
[tool.uv.sources]
torch = { index = "pytorch" }

[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cpu"
```

类似地，要根据平台从不同的索引拉取包，你可以提供通过环境标记区分的源列表：

```toml title="pyproject.toml"
[project]
dependencies = ["torch"]

[tool.uv.sources]
torch = [
  { index = "pytorch-cu118", marker = "sys_platform == 'darwin'"},
  { index = "pytorch-cu124", marker = "sys_platform != 'darwin'"},
]

[[tool.uv.index]]
name = "pytorch-cu118"
url = "https://download.pytorch.org/whl/cu118"

[[tool.uv.index]]
name = "pytorch-cu124"
url = "https://download.pytorch.org/whl/cu124"
```

可以将索引标记为 `explicit = true`，以防止从该索引安装包，除非显式固定到该索引。例如，要确保 `torch` 从 `pytorch` 索引安装，但所有其他包都从 PyPI 安装，请将以下内容添加到你的 `pyproject.toml`：

```toml
[tool.uv.sources]
torch = { index = "pytorch" }

[[tool.uv.index]]
name = "pytorch"
url = "https://download.pytorch.org/whl/cpu"
explicit = true
```

通过 `tool.uv.sources` 引用的命名索引必须在项目的 `pyproject.toml` 文件中定义；通过命令行、环境变量或用户级配置提供的索引将不被识别。

如果一个索引同时标记为 `default = true` 和 `explicit = true`，它将被视为显式索引（即只能通过 `tool.uv.sources` 使用），同时也会移除 PyPI 作为默认索引。

## 跨多个索引搜索

默认情况下，uv 会在找到给定包的第一个索引处停止，并将解析限制在该第一个索引上存在的版本（`first-index` 策略）。

例如，如果通过 `[[tool.uv.index]]` 指定了一个内部索引，uv 的行为是：如果一个包存在于该内部索引上，它将*始终*从该内部索引安装，而永远不会从 PyPI 安装。这样做的目的是防止"依赖混淆"攻击，即攻击者在 PyPI 上发布一个与内部包同名的恶意包，从而导致安装恶意包而不是内部包。例如，参见 2022 年 12 月的 [`torchtriton` 攻击](https://pytorch.org/blog/compromised-nightly-dependency/)。

要选择其他索引行为，请使用 `--index-strategy` 命令行选项或 `UV_INDEX_STRATEGY` 环境变量，它支持以下值：

- `first-index`（默认）：在所有索引中搜索每个包，将候选版本限制在包含该包的第一个索引中存在的版本。
- `unsafe-first-match`：在所有索引中搜索每个包，但优先选择具有兼容版本的第一个索引，即使其他索引上有更新的版本可用。
- `unsafe-best-match`：在所有索引中搜索每个包，并从候选版本的组合集中选择最佳版本。

虽然 `unsafe-best-match` 最接近 pip 的行为，但它使用户面临"依赖混淆"攻击的风险。

## 认证

大多数私有包索引需要认证才能访问包，通常通过用户名和密码（或访问令牌）进行。

!!! tip

    有关与特定私有索引提供程序（例如来自 AWS、Azure 或 GCP）进行身份验证的详细信息，请参阅[替代索引指南](../guides/integration/alternative-indexes.md)。

### 直接提供凭据

可以通过环境变量直接提供凭据，或者将它们嵌入到 URL 中。

例如，给定一个名为 `internal-proxy` 的索引，需要用户名（`public`）和密码（`koala`），在你的 `pyproject.toml` 中定义索引（不包含凭据）：

```toml
[[tool.uv.index]]
name = "internal-proxy"
url = "https://example.com/simple"
```

然后，你可以设置 `UV_INDEX_INTERNAL_PROXY_USERNAME` 和 `UV_INDEX_INTERNAL_PROXY_PASSWORD` 环境变量，其中 `INTERNAL_PROXY` 是索引名称的大写版本，非字母数字字符替换为下划线：

```sh
export UV_INDEX_INTERNAL_PROXY_USERNAME=public
export UV_INDEX_INTERNAL_PROXY_PASSWORD=koala
```

通过环境变量提供凭据，可以避免将敏感信息存储在明文的 `pyproject.toml` 文件中。

或者，凭据可以直接嵌入到索引定义中：

```toml
[[tool.uv.index]]
name = "internal"
url = "https://public:koala@pypi-proxy.corp.dev/simple"
```

出于安全目的，凭据*永远不会*存储在 `uv.lock` 文件中；因此，uv 在安装时*必须*能够访问经过身份验证的 URL。

### 使用凭据提供程序

除了直接提供凭据外，uv 还支持从 netrc 和 keyring 发现凭据。有关设置特定凭据提供程序的详细信息，请参阅 [HTTP 认证](./authentication/http.md) 文档。

默认情况下，uv 会在查询提供程序之前尝试未经身份验证的请求。如果请求失败，uv 将搜索凭据。如果找到凭据，将尝试经过身份验证的请求。

!!! note

    如果设置了用户名，uv 将在发出未经身份验证的请求之前搜索凭据。

某些索引（例如 GitLab）会将未经身份验证的请求转发到公共索引，如 PyPI——这意味着 uv 不会搜索凭据。可以使用 `authenticate` 设置按索引更改此行为。例如，要始终搜索凭据：

```toml hl_lines="4"
[[tool.uv.index]]
name = "example"
url = "https://example.com/simple"
authenticate = "always"
```

当 `authenticate` 设置为 `always` 时，uv 将急切地搜索凭据，如果找不到凭据则会报错。

### 跨索引搜索时忽略错误代码

当使用 [first-index 策略](#searching-across-multiple-indexes) 时，如果遇到 HTTP 401 Unauthorized 或 HTTP 403 Forbidden 状态代码，uv 将停止跨索引搜索。一个例外是，在搜索 `pytorch` 索引时，uv 将忽略 403（因为当包不存在时此索引返回 403）。

要配置为索引忽略哪些错误代码，请使用 `ignored-error-codes` 设置。例如，要为私有索引忽略 403（但不忽略 401）：

```toml
[[tool.uv.index]]
name = "private-index"
url = "https://private-index.com/simple"
authenticate = "always"
ignore-error-codes = [403]
```

当遇到 `404 Not Found` 时，uv 将始终继续跨索引搜索。这不能被覆盖。

### 禁用认证

为防止凭据泄露，可以为索引禁用认证：

```toml hl_lines="4"
[[tool.uv.index]]
name = "example"
url = "https://example.com/simple"
authenticate = "never"
```

当 `authenticate` 设置为 `never` 时，uv 将永远不会搜索给定索引的凭据，并且如果直接提供了凭据则会报错。

### 自定义缓存控制头

默认情况下，uv 会遵守索引提供的缓存控制头。例如，PyPI 使用 `max-age=600` 头提供包元数据，从而允许 uv 缓存包元数据 10 分钟；并使用 `max-age=365000000, immutable` 头提供 wheel 和源发行版，从而允许 uv 无限期缓存构件。

要覆盖索引的缓存控制头，请使用 `cache-control` 设置：

```toml
[[tool.uv.index]]
name = "example"
url = "https://example.com/simple"
cache-control = { api = "max-age=600", files = "max-age=365000000, immutable" }
```

`cache-control` 设置接受一个具有两个可选键的对象：

- `api`：控制简单 API 请求（包元数据）的缓存。
- `files`：控制构件下载（wheel 和源发行版）的缓存。

这些键的值是遵循 [HTTP Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) 语法的字符串。例如，要强制 uv 始终重新验证包元数据，请设置 `api = "no-cache"`：

```toml
[[tool.uv.index]]
name = "example"
url = "https://example.com/simple"
cache-control = { api = "no-cache" }
```

此设置最常用于覆盖私有索引的默认缓存控制头，这些索引通常无意中禁用了缓存。我们通常建议遵循 PyPI 的缓存头方法，即设置 `api = "max-age=600"` 和 `files = "max-age=365000000, immutable"`。

## "扁平"索引

默认情况下，`[[tool.uv.index]]` 条目被假定为实现 [PEP 503](https://peps.python.org/pep-0503/) 简单仓库 API 的 PyPI 风格注册表。但是，uv 也支持"扁平"索引，这些是包含 wheel 和源发行版平面列表的本地目录或 HTML 页面。在 pip 中，此类索引使用 `--find-links` 选项指定。

要在你的 `pyproject.toml` 中定义扁平索引，请使用 `format = "flat"` 选项：

```toml
[[tool.uv.index]]
name = "example"
url = "/path/to/directory"
format = "flat"
```

扁平索引支持与简单仓库 API 索引相同的功能集（例如，`explicit = true`）；你也可以使用 `tool.uv.sources` 将包固定到扁平索引。

## `--index-url` 和 `--extra-index-url`

除了 `[[tool.uv.index]]` 配置选项外，为了兼容性，uv 还支持 pip 风格的 `--index-url` 和 `--extra-index-url` 命令行选项，其中 `--index-url` 定义默认索引，`--extra-index-url` 定义额外的索引。

这些选项可以与 `[[tool.uv.index]]` 配置选项结合使用，并遵循相同的优先级规则：

- 默认索引始终被视为最低优先级，无论是通过旧的 `--index-url` 参数、推荐的 `--default-index` 参数，还是带有 `default = true` 的 `[[tool.uv.index]]` 条目定义的。
- 索引按照定义的顺序进行查询，无论是通过旧的 `--extra-index-url` 参数、推荐的 `--index` 参数，还是 `[[tool.uv.index]]` 条目。

实际上，`--index-url` 和 `--extra-index-url` 可以被视为未命名的 `[[tool.uv.index]]` 条目，前者启用了 `default = true`。在这种情况下，`--index-url` 映射到 `--default-index`，而 `--extra-index-url` 映射到 `--index`。