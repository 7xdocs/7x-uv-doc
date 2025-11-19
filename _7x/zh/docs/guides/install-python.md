---
title: 安装和管理 Python
description:
  使用 uv 安装 Python 的指南，包括请求特定版本、自动安装、查看已安装版本等。
---

# 安装 Python

如果系统上已安装 Python，uv 将在无需配置的情况下[检测并使用](#使用现有的-python-版本)。然而，uv 也可以安装和管理 Python 版本。uv 会在需要时[自动安装](#自动-python-下载)缺失的 Python 版本 —— 您无需预先安装 Python 即可开始使用。

## 开始使用

要安装最新的 Python 版本：

```console
$ uv python install
```

!!! note

    Python 不发布官方的可分发二进制文件。因此，uv 使用来自 Astral [`python-build-standalone`](https://github.com/astral-sh/python-build-standalone) 项目的发行版。更多详细信息请参阅 [Python 发行版](../concepts/python-versions.md#managed-python-distributions) 文档。

Python 安装完成后，`uv` 命令将自动使用它。uv 还会将安装的版本添加到您的 `PATH` 中：

```console
$ python3.13
```

默认情况下，uv 仅安装一个带*版本号*的可执行文件。要安装 `python` 和 `python3` 可执行文件，请包含实验性的 `--default` 选项：

```console
$ uv python install --default
```

!!! tip

    更多详细信息请参阅关于 [安装 Python 可执行文件](../concepts/python-versions.md#installing-python-executables) 的文档。

## 安装特定版本

要安装特定的 Python 版本：

```console
$ uv python install 3.12
```

要安装多个 Python 版本：

```console
$ uv python install 3.11 3.12
```

要安装替代的 Python 实现，例如 PyPy：

```console
$ uv python install pypy@3.10
```

更多详细信息请参阅 [`python install`](../concepts/python-versions.md#installing-a-python-version) 文档。

## 重新安装 Python

要重新安装 uv 托管的 Python 版本，请使用 `--reinstall`，例如：

```console
$ uv python install --reinstall
```

这将重新安装所有先前安装的 Python 版本。Python 发行版在不断改进，因此即使 Python 版本未更改，重新安装也可能解决某些错误。

## 查看 Python 安装

要查看可用和已安装的 Python 版本：

```console
$ uv python list
```

更多详细信息请参阅 [`python list`](../concepts/python-versions.md#viewing-available-python-versions) 文档。

## 自动 Python 下载

使用 uv 无需显式安装 Python。默认情况下，uv 会在需要时自动下载 Python 版本。例如，如果未安装 Python 3.12，以下命令将下载它：

```console
$ uvx python@3.12 -c "print('hello world')"
```

即使没有请求特定的 Python 版本，uv 也会按需下载最新版本。例如，如果系统上没有 Python 版本，以下命令将在创建新虚拟环境之前安装 Python：

```console
$ uv venv
```

!!! tip

    如果您希望更好地控制 Python 的下载时机，可以[轻松禁用](../concepts/python-versions.md#disabling-automatic-python-downloads)自动 Python 下载功能。

<!-- TODO(zanieb): 在添加 Python shim 管理功能后恢复此部分内容
请注意，当发生自动 Python 安装时，`python` 命令不会被添加到 shell 中。使用 `uv python install-shim` 来确保安装 `python` shim。
-->

## 使用现有的 Python 版本

如果系统上存在现有的 Python 安装，uv 将会使用它们。此行为无需任何配置：如果系统 Python 满足命令调用的要求，uv 将使用它。详情请参阅 [Python 发现](../concepts/python-versions.md#discovery-of-python-versions) 文档。

要强制 uv 使用系统 Python，请提供 `--no-managed-python` 标志。更多详细信息请参阅 [Python 版本偏好](../concepts/python-versions.md#requiring-or-disabling-managed-python-versions) 文档。

## 升级 Python 版本

!!! important

    升级 Python 补丁版本的功能处于*预览*阶段。这意味着该行为是实验性的，可能会发生变化。

要将 Python 版本升级到最新的受支持补丁版本：

```console
$ uv python upgrade 3.12
```

要升级所有 uv 托管的 Python 版本：

```console
$ uv python upgrade
```

更多详细信息请参阅 [`python upgrade`](../concepts/python-versions.md#upgrading-python-versions) 文档。

## 后续步骤

要了解更多关于 `uv python` 的信息，请参阅 [Python 版本概念](../concepts/python-versions.md) 页面和 [命令参考](../reference/cli.md#uv-python)。

或者，继续阅读以了解如何使用 uv [运行脚本](./scripts.md) 和调用 Python。
