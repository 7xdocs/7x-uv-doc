# 可复现示例

## 为什么可复现示例很重要

最小可复现示例（MRE）对于修复错误至关重要。如果没有一个可以用来复现问题的示例，维护者就无法调试或测试问题是否已修复。如果示例不是最小化的，即包含了许多与问题无关的内容，维护者可能需要花费更多时间来确定问题的根本原因。

## 如何编写可复现示例

编写可复现示例时，目标是提供所有必要的上下文，以便其他人能够复现你的示例。这包括：

- 你使用的平台（例如操作系统和架构）
- 任何相关的系统状态（例如明确设置的环境变量）
- uv 的版本
- 其他相关工具的版本
- 相关文件（`uv.lock`、`pyproject.toml` 等）
- 要运行的命令

为确保你的复现是最小化的，请尽可能移除不必要的依赖、设置和文件。在分享之前，请务必测试你的复现步骤。我们建议包含复现过程中的详细日志；这些日志在你的机器上可能在某些关键方面有所不同。对于非常长的日志，使用 [Gist](https://gist.github.com) 可能会很有帮助。

下面，我们将介绍几种创建和分享可复现示例的特定[策略](#strategies-for-reproducible-examples)。

!!! tip

    Stack Overflow 上有一篇关于创建 MRE 基础知识的很棒指南：[Stack Overflow](https://stackoverflow.com/help/minimal-reproducible-example)。

## 可复现示例的策略

### Docker 镜像

编写 Docker 镜像通常是分享可复现示例的最佳方式，因为它完全自包含。这意味着复现者的系统状态不会影响问题的复现。

!!! note

    仅当问题在 Linux 上可复现时，使用 Docker 镜像才可行。在使用 macOS 时，明智的做法是确保你的镜像在 Linux 上不可复现，但有些错误确实特定于操作系统。虽然使用 Docker 运行 Windows 容器是可行的，但这并不常见。这类错误预计应通过[脚本](#script)的方式报告。

在使用 uv 编写 Docker MRE 时，最好从 [uv 的 Docker 镜像](../../guides/integration/docker.md#available-images) 之一开始。这样做时，请确保固定使用特定版本的 uv。

```Dockerfile
FROM ghcr.io/astral-sh/uv:0.5.24-debian-slim
```

虽然 Docker 镜像与系统隔离，但构建默认会使用你系统的架构。在分享复现步骤时，你可以显式设置平台以确保复现者获得预期的行为。uv 发布了适用于 `linux/amd64`（例如 Intel 或 AMD）和 `linux/arm64`（例如 Apple M 系列或 ARM）的镜像。

```Dockerfile
FROM --platform=linux/amd64 ghcr.io/astral-sh/uv:0.5.24-debian-slim
```

Docker 镜像最适合复现那些可以通过命令构建的问题，例如：

```Dockerfile
FROM --platform=linux/amd64 ghcr.io/astral-sh/uv:0.5.24-debian-slim

RUN uv init /mre
WORKDIR /mre
RUN uv add pydantic
RUN uv sync
RUN uv run -v python -c "import pydantic"
```

但是，你也可以内联地将文件写入镜像：

```Dockerfile
FROM --platform=linux/amd64 ghcr.io/astral-sh/uv:0.5.24-debian-slim

COPY <<EOF /mre/pyproject.toml
[project]
name = "example"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = ["pydantic"]
EOF

WORKDIR /mre
RUN uv lock
```

如果你需要写入多个文件，最好创建并发布一个 [Git 仓库](#git-repository)。你可以结合这些方法，在仓库中包含一个 `Dockerfile`。

在分享 Docker 复现步骤时，包含构建日志会很有帮助。你可以通过禁用缓存和美化输出来查看构建步骤的更多输出：

```console
docker build . --progress plain --no-cache
```

### 脚本

当报告无法在[容器](#docker-image)中复现的平台特定错误时，最佳实践是包含一个显示可用于复现错误的命令的脚本，例如：

```bash
uv init
uv add pydantic
uv sync
uv run -v python -c "import pydantic"
```

如果你的复现需要多个文件，请使用 [Git 仓库](#git-repository) 来分享它们。

除了脚本之外，还应包含失败的*详细*日志（即使用 `-v` 标志）和完整的错误消息。

每当脚本依赖外部状态时，请务必分享这些信息。例如，如果你在 Windows 上编写了脚本，并且它使用了你通过 `choco` 安装的 Python 版本，并在 PowerShell 6.2 上运行，请在报告中包含这些信息。

### Git 仓库

当分享 Git 仓库复现步骤时，请包含一个能复现问题的[脚本](#script)，或者更好的是，包含一个 [Dockerfile](#docker-image)。脚本的第一步应该是克隆仓库并检出特定的提交：

```console
$ git clone https://github.com/<user>/<project>.git
$ cd <project>
$ git checkout <commit>
$ <commands to produce error>
```

你可以通过 [GitHub UI](https://github.com/new) 或 `gh` CLI 快速创建一个新仓库：

```console
$ gh repo create uv-mre-1234 --clone
```

当使用 Git 仓库进行复现时，请记住通过排除不需要复现问题的文件或设置来*最小化*内容。