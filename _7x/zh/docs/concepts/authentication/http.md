# HTTP 凭据

uv 支持在查询包注册表时通过 HTTP 进行身份验证。

身份验证可以来自以下来源，按优先级从高到低排列：

- URL，例如：`https://<user>:<password>@<hostname>/...`
- [netrc](#netrc-文件) 配置文件
- uv 凭据存储
- [密钥环提供程序](#密钥环提供程序)（默认关闭）

在以下上下文中指定的主机可以使用身份验证：

- `[index]`
- `index-url`
- `extra-index-url`
- `find-links`
- `package @ https://...`

## netrc 文件

[`.netrc`](https://everything.curl.dev/usingcurl/netrc) 文件是一种长期存在的纯文本格式，用于在系统上存储凭据。

从 `.netrc` 文件读取凭据的功能始终启用。如果定义了 `NETRC` 环境变量，将从其指定的文件路径加载，否则回退到 `~/.netrc`。

## uv 凭据存储

uv 可以使用 [`uv auth` 命令](./cli.md) 从存储中读取和写入凭据。

凭据存储在 uv 状态目录下的一个纯文本文件中，例如，在 Unix 系统上为 `~/.local/share/uv/credentials/credentials.toml`。此文件目前不建议手动编辑。

!!! note

    一个安全的、系统原生的存储机制正处于 [预览](../preview.md) 阶段 — 它仍然是实验性的，正在积极开发中。未来，这将成为默认的存储机制。

    启用后，uv 将使用您操作系统原生的秘密存储机制。在 macOS 上，它使用钥匙串服务。在 Windows 上，它使用 Windows 凭据管理器。在 Linux 上，它使用基于 DBus 的 Secret Service API。

    目前，uv 仅在其已添加到秘密存储中的凭据中搜索原生存储 — 它不会检索由其他应用程序保存的凭据。

    设置 `UV_PREVIEW_FEATURES=native-auth` 以使用此存储机制。

## 密钥环提供程序

密钥环提供程序是一个来自 `pip` 的概念，允许从符合流行的 [keyring](https://github.com/jaraco/keyring) Python 包接口的接口检索凭据。

"subprocess" 密钥环提供程序通过调用 `keyring` 命令来获取凭据。uv 目前不支持其他类型的密钥环提供程序。

设置 `--keyring-provider subprocess`、`UV_KEYRING_PROVIDER=subprocess` 或 `tool.uv.keyring-provider = "subprocess"` 来使用该提供程序。

## 凭据的持久性

如果为单个索引 URL 或网络位置（方案、主机和端口）找到身份验证信息，它将在该命令的持续时间内被缓存，并用于对该索引或网络位置的其他查询。身份验证信息不会在 uv 的不同调用之间缓存。

当使用 `uv add` 时，uv _不会_ 将索引凭据持久化到 `pyproject.toml` 或 `uv.lock` 中。这些文件通常包含在版本控制和分发中，因此将凭据包含在其中通常是不安全的。然而，uv _会_ 持久化直接 URL 的凭据，例如 `package @ https://username:password:example.com/foo.whl`，因为目前没有其他方法可以提供这些凭据。

如果在 `uv add` 期间将凭据附加到索引 URL，uv 在后续操作中可能无法从需要身份验证的索引获取依赖项。有关索引的持久身份验证的详细信息，请参阅 [索引身份验证文档](../indexes.md#authentication)。

## 了解更多

有关验证索引 URL 的详细信息，请参阅 [索引身份验证文档](../indexes.md#authentication)。

有关与 `pip` 差异的详细信息，请参阅 [`pip` 兼容性指南](../../pip/compatibility.md#registry-authentication)。