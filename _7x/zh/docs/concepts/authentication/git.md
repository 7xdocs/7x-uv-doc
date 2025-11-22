# Git 凭证

uv 允许使用 SSH 或 HTTP 认证从私有 Git 仓库安装包。

## SSH 认证

要使用 SSH 密钥进行认证，请使用 `ssh://` 协议：

- `git+ssh://git@<hostname>/...` (例如，`git+ssh://git@github.com/astral-sh/uv`)
- `git+ssh://git@<host>/...` (例如，`git+ssh://git@github.com-key-2/astral-sh/uv`)

SSH 认证需要使用用户名 `git`。

有关如何配置 SSH 的更多详细信息，请参阅 [GitHub SSH 文档](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)。

### HTTP 认证

要通过 HTTP 基本认证使用密码或令牌进行认证：

- `git+https://<user>:<token>@<hostname>/...` (例如， `git+https://git:github_pat_asdf@github.com/astral-sh/uv`)
- `git+https://<token>@<hostname>/...` (例如， `git+https://github_pat_asdf@github.com/astral-sh/uv`)
- `git+https://<user>@<hostname>/...` (例如， `git+https://git@github.com/astral-sh/uv`)

!!! note

    使用 GitHub 个人访问令牌时，用户名是任意的。GitHub 不允许在 URL 中使用您的账户名和密码，但其他托管服务商可能允许。

如果 URL 中没有凭证但需要进行身份验证，则会查询 [Git 凭证助手](#git-凭证助手)。

## 凭证的持久化

使用 `uv add` 时，uv _不会_ 将 Git 凭证持久化到 `pyproject.toml` 或 `uv.lock` 文件中。这些文件通常包含在版本控制和分发中，因此在其中包含凭证通常是不安全的。

如果您配置了 Git 凭证助手，您的凭证可能会被自动持久化，从而使得后续获取依赖项能够成功。但是，如果您没有 Git 凭证助手，或者项目在没有预置凭证的机器上使用，uv 将无法获取依赖项。

您*可以*通过向 `uv add` 传递 `--raw` 选项来强制 uv 持久化 Git 凭证。但是，我们强烈建议改为设置 [凭证助手](#git-凭证助手)。

## Git 凭证助手

Git 凭证助手用于存储和检索 Git 凭证。请参阅 [Git 文档](https://git-scm.com/doc/credential-helpers) 以了解更多。

如果您使用 GitHub，设置凭证助手的最简单方法是 [安装 `gh` CLI](https://github.com/cli/cli#installation) 并使用：

```console
$ gh auth login
```

更多详细信息，请参阅 [`gh auth login`](https://cli.github.com/manual/gh_auth_login) 文档。

!!! note

    在交互式使用 `gh auth login` 时，凭证助手会自动配置。但是当使用 `gh auth login --with-token` 时（如在 uv 的 [GitHub Actions 指南](../../guides/integration/github.md#private-repos) 中），之后需要运行 [`gh auth setup-git`](https://cli.github.com/manual/gh_auth_setup-git) 命令来配置凭证助手。