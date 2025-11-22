# `uv auth` CLI

uv 提供了一个高级接口，用于存储和检索来自服务的凭证。

## 登录服务

要添加服务的凭证，请使用 `uv auth login` 命令：

```console
$ uv auth login example.com
```

这将提示输入凭证。

凭证也可以通过 `--username` 和 `--password` 选项提供，或者对于使用 `__token__` 或任意用户名的服务，可以使用 `--token` 选项提供。

!!! note

    我们建议通过 stdin 提供密钥。使用 `-` 表示应从 stdin 读取值，例如，对于 `--password`：

    ```console
    $ echo 'my-password' | uv auth login example.com --password -
    ```

    相同的模式可用于 `--token`。

添加凭证后，uv 将在需要从给定服务获取内容的打包操作中使用它们。目前，仅支持 HTTPS 基本认证。这些凭证尚不会用于 Git 请求。

!!! note

    凭证不会被验证，即，不正确的凭证不会导致失败。

## 登出服务

要移除凭证，请使用 `uv auth logout` 命令：

```console
$ uv auth logout example.com
```

!!! note

    凭证不会在远程服务器上失效，即，它们只会从本地存储中移除，而不会被远程作废。

## 显示服务的凭证

要显示为给定 URL 存储的凭证，请使用 `uv auth token` 命令：

```console
$ uv auth token example.com
```

如果登录时使用了用户名，则也需要提供，例如：

```console
$ uv auth token --username foo example.com
```

## 配置存储后端

凭证将持久化到 uv [凭证存储](./http.md#the-uv-credentials-store)。

默认情况下，凭证被写入一个纯文本文件。可以通过设置 `UV_PREVIEW_FEATURES=native-auth` 来启用加密的、系统原生的存储后端。