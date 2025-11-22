# TLS 证书

默认情况下，uv 从捆绑的 `webpki-roots` crate 加载证书。`webpki-roots` 是一组来自 Mozilla 的可靠信任根，将其包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上，读取系统信任存储会产生显著的延迟）。

## 系统证书

在某些情况下，您可能希望使用平台原生的证书存储，特别是当您依赖系统证书存储中包含的企业信任根（例如，用于强制代理）时。要指示 uv 使用系统的信任存储，请使用 `--native-tls` 命令行标志运行 uv，或者将 `UV_NATIVE_TLS` 环境变量设置为 `true`。

## 自定义证书

如果需要直接指定证书的路径（例如，在 CI 环境中），请将 `SSL_CERT_FILE` 环境变量设置为证书包的路径，以指示 uv 使用该文件而不是系统的信任存储。

如果需要客户端证书认证（mTLS），请将 `SSL_CLIENT_CERT` 环境变量设置为包含证书及后续私钥的 PEM 格式文件的路径。

## 不安全的主机

如果您使用的设置中需要信任自签名证书或者以其他方式禁用证书验证，您可以通过 `allow-insecure-host` 配置选项指示 uv 允许与特定主机建立不安全的连接。例如，将以下内容添加到 `pyproject.toml` 将允许与 `example.com` 建立不安全连接：

```toml
[tool.uv]
allow-insecure-host = ["example.com"]
```

`allow-insecure-host` 期望接收一个主机名（例如，`localhost`）或主机名-端口对（例如，`localhost:8080`），并且仅适用于 HTTPS 连接，因为 HTTP 连接本质上就是不安全的。

请谨慎使用 `allow-insecure-host`，并且仅在可信环境中使用，因为它会由于缺乏证书验证而使您面临安全风险。