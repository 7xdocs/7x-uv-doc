# 获取帮助

## 帮助菜单

可以使用 `--help` 标志来查看命令的帮助菜单，例如，对于 `uv` 命令：

```console
$ uv --help
```

要查看特定命令的帮助菜单，例如，对于 `uv init` 命令：

```console
$ uv init --help
```

当使用 `--help` 标志时，uv 会显示一个简明的帮助菜单。要查看命令的详细帮助菜单，请使用 `uv help`：

```console
$ uv help
```

要查看特定命令的详细帮助菜单，例如，对于 `uv init` 命令：

```console
$ uv help init
```

当使用详细帮助菜单时，uv 会尝试使用 `less` 或 `more` 来对输出进行"分页"，这样内容就不会一次性全部显示。要退出分页器，请按 `q` 键。

## 显示详细输出

`-v` 标志可用于显示命令的详细输出，例如，对于 `uv sync` 命令：

```console
$ uv sync -v
```

`-v` 标志可以重复使用以增加详细程度，例如：

```console
$ uv sync -vv
```

通常，详细输出会包含关于 uv 为何以某种方式行事的额外信息。

## 查看版本

在寻求帮助时，确定您正在使用的 uv 版本非常重要——有时问题在更新的版本中已经得到解决。

要检查已安装的版本：

```console
$ uv self version
```

以下命令同样有效：

```console
$ uv --version      # 输出与 `uv self version` 相同
$ uv -V             # 不包含构建提交和日期信息
```

!!! note

    在 uv 0.7.0 版本之前，使用的是 `uv version` 而不是 `uv self version`。

## 问题排查

参考文档中包含了一个针对常见问题的[问题排查指南](../reference/troubleshooting/index.md)。

## 在 GitHub 上提交问题

GitHub 上的[问题跟踪器](https://github.com/astral-sh/uv/issues)是报告错误和请求功能的好地方。请确保先搜索类似的问题，因为其他人遇到相同问题的情况很常见。

## 在 Discord 上交流

Astral 有一个 [Discord 服务器](https://discord.com/invite/astral-sh)，这是提问、了解更多关于 uv 的信息以及与其他社区成员互动的好地方。