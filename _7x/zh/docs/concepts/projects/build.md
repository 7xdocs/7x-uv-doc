# 构建分发包

为了将您的项目分发给其他人（例如，上传到像 PyPI 这样的索引），您需要将其构建为可分发的格式。

Python 项目通常同时以源码分发包（sdists）和二进制分发包（wheels）的形式分发。前者通常是一个包含项目源代码以及一些额外元数据的 `.tar.gz` 或 `.zip` 文件，而后者是一个包含预构建构件的 `.whl` 文件，可以直接安装。

!!! important

    当使用 `uv build` 时，uv 充当一个[构建前端](https://peps.python.org/pep-0517/#terminology-and-goals)，它仅决定使用的 Python 版本并调用构建后端。构建的细节，例如包含的文件和分发包的文件名，由构建后端决定，如 [`[build-system]`](./config.md#build-systems) 中所定义。关于构建配置的信息可以在相应工具的文档中找到。

## 使用 `uv build`

`uv build` 可用于为您的项目构建源码分发包和二进制分发包。
默认情况下，`uv build` 将构建当前目录中的项目，并将构建产物放置在 `dist/` 子目录中：

```console
$ uv build
$ ls dist/
example-0.1.0-py3-none-any.whl
example-0.1.0.tar.gz
```

您可以通过向 `uv build` 提供路径来在不同目录中构建项目，例如 `uv build path/to/project`。

`uv build` 将首先构建一个源码分发包，然后从该源码分发包构建一个二进制分发包（wheel）。

您可以使用 `uv build --sdist` 限制 `uv build` 仅构建源码分发包，使用 `uv build --wheel` 仅构建二进制分发包，或者使用 `uv build --sdist --wheel` 从源码构建这两种分发包。

## 构建约束

`uv build` 接受 `--build-constraint` 参数，该参数可用于在构建过程中约束任何构建要求的版本。当与 `--require-hashes` 结合使用时，uv 将强制执行用于构建项目的要求与特定的已知哈希值匹配，以确保可重现性。

例如，给定以下 `constraints.txt`：

```text
setuptools==68.2.2 --hash=sha256:b454a35605876da60632df1a60f736524eb73cc47bbc9f3f1ef1b644de74fd2a
```

运行以下命令将使用指定版本的 `setuptools` 构建项目，并验证下载的 `setuptools` 分发包是否与指定的哈希值匹配：

```console
$ uv build --build-constraint constraints.txt --require-hashes
```