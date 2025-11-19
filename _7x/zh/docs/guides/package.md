---
title: 构建和发布包
description: 使用 uv 将 Python 包构建并发布到包索引（如 PyPI）的指南。
---

# 构建和发布包

uv 支持通过 `uv build` 将 Python 包构建为源码分发包和二进制分发包，并使用 `uv publish` 将它们上传到注册中心。

## 为打包准备你的项目

在尝试发布你的项目之前，你需要确保它已经准备好进行分发包打包。

如果你的项目在 `pyproject.toml` 中没有包含 `[build-system]` 定义，uv 默认不会构建它。这意味着你的项目可能尚未准备好进行分发。请阅读[项目概念](../concepts/projects/config.md#build-systems)文档中关于声明构建系统影响的更多信息。

!!! note

    如果你有内部包不希望被发布，可以将它们标记为私有：

    ```toml
    [project]
    classifiers = ["Private :: Do Not Upload"]
    ```

    此设置会使 PyPI 拒绝发布你上传的包。它不会影响其他注册中心的安全或隐私设置。

    我们还建议仅生成[按项目的 PyPI API 令牌](https://pypi.org/help/#apitoken)：如果没有与项目匹配的 PyPI 令牌，就不会意外发布。

## 构建你的包

使用 `uv build` 构建你的包：

```console
$ uv build
```

默认情况下，`uv build` 将构建当前目录中的项目，并将构建产物放置在 `dist/` 子目录中。

或者，`uv build <SRC>` 将构建指定目录中的包，而 `uv build --package <PACKAGE>` 将在当前工作区内构建指定的包。

!!! info

    默认情况下，`uv build` 在从 `pyproject.toml` 的 `build-system.requires` 部分解析构建依赖时，会遵循 `tool.uv.sources`。在发布包时，我们建议运行 `uv build --no-sources` 以确保在禁用 `tool.uv.sources` 的情况下（例如在使用其他构建工具如 [`pypa/build`](https://github.com/pypa/build) 时），包也能正确构建。

## 更新版本号

`uv version` 命令提供了在发布包之前更新包版本的便捷方法。
[请参阅项目文档以了解如何读取包的版本](./projects.md#managing-version)。

要更新到精确版本，请将其作为位置参数提供：

```console
$ uv version 1.0.0
hello-world 0.7.0 => 1.0.0
```

要在不实际更新 `pyproject.toml` 的情况下预览更改，请使用 `--dry-run` 标志：

```console
$ uv version 2.0.0 --dry-run
hello-world 1.0.0 => 2.0.0
$ uv version
hello-world 1.0.0
```

要按语义增加包的版本，请使用 `--bump` 选项：

```console
$ uv version --bump minor
hello-world 1.2.3 => 1.3.0
```

`--bump` 选项支持以下常见的版本组件：`major`、`minor`、`patch`、`stable`、`alpha`、`beta`、`rc`、`post` 和 `dev`。当多次提供时，这些组件将按从最大（`major`）到最小（`dev`）的顺序应用。

你可以选择使用 `--bump <component>=<value>` 提供数值来显式设置结果组件：

```console
$ uv version --bump patch --bump dev=66463664
hello-world 0.0.1 => 0.0.2.dev66463664
```

要从稳定版本切换到预发布版本，除了预发布组件外，还需提升 major、minor 或 patch 组件之一：

```console
$ uv version --bump patch --bump beta
hello-world 1.3.0 => 1.3.1b1
$ uv version --bump major --bump alpha
hello-world 1.3.0 => 2.0.0a1
```

当从一个预发布版本切换到新的预发布版本时，只需提升相关的预发布组件：

```console
$ uv version --bump beta
hello-world 1.3.0b1 => 1.3.0b2
```

当从预发布版本切换到稳定版本时，可以使用 `stable` 选项来清除预发布组件：

```console
$ uv version --bump stable
hello-world 1.3.1b2 => 1.3.1
```

!!! info

    默认情况下，当 `uv version` 修改项目时，它会执行锁定和同步操作。要防止锁定和同步，请使用 `--frozen`；或者，仅防止同步，请使用 `--no-sync`。

## 发布你的包

!!! note

    关于从 GitHub Actions 发布到 PyPI 的完整指南，请参阅 [GitHub 指南](integration/github.md#publishing-to-pypi)

使用 `uv publish` 发布你的包：

```console
$ uv publish
```

使用 `--token` 或 `UV_PUBLISH_TOKEN` 设置 PyPI 令牌，或者使用 `--username` 或 `UV_PUBLISH_USERNAME` 设置用户名，并使用 `--password` 或 `UV_PUBLISH_PASSWORD` 设置密码。对于从 GitHub Actions 或其他可信发布者发布到 PyPI，你不需要设置任何凭据。相反，[请向 PyPI 项目添加一个可信发布者](https://docs.pypi.org/trusted-publishers/adding-a-publisher/)。

!!! note

    PyPI 不再支持使用用户名和密码发布，你需要生成一个令牌。使用令牌相当于设置 `--username __token__` 并将令牌用作密码。

如果你通过 `[[tool.uv.index]]` 使用自定义索引，请添加 `publish-url` 并使用 `uv publish --index <name>`。例如：

```toml
[[tool.uv.index]]
name = "testpypi"
url = "https://test.pypi.org/simple/"
publish-url = "https://test.pypi.org/legacy/"
explicit = true
```

!!! note

    当使用 `uv publish --index <name>` 时，必须存在 `pyproject.toml` 文件，即你需要在发布 CI 作业中包含检出步骤。

尽管 `uv publish` 会重试失败的上传，但有时发布可能会在中间失败，部分文件已上传而部分文件仍然缺失。对于 PyPI，你可以重试完全相同的命令，已存在的相同文件将被忽略。对于其他注册中心，请使用 `--check-url <index url>` 并指定包所属的索引 URL（不是发布 URL）。当使用 `--index` 时，索引 URL 被用作检查 URL。uv 将跳过上传与注册中心中文件相同的文件，并且它也会处理竞态条件的并行上传。请注意，现有文件需要与之前上传到注册中心的文件完全匹配，这可以避免意外发布相同版本但内容不同的源码分发包和 wheel 包。

## 安装你的包

使用 `uv run` 测试包是否可以安装和导入：

```console
$ uv run --with <PACKAGE> --no-project -- python -c "import <PACKAGE>"
```

`--no-project` 标志用于避免从本地项目目录安装包。

!!! tip

    如果你最近安装了该包，可能需要包含 `--refresh-package <PACKAGE>` 选项以避免使用包的缓存版本。

## 后续步骤

要了解更多关于发布包的信息，请查看 [PyPA 指南](https://packaging.python.org/en/latest/guides/section-build-and-publish/)中关于构建和发布的部分。

或者，继续阅读关于[将 uv 与其他软件集成](./integration/index.md)的指南。