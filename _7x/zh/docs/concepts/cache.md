# 缓存

## 依赖缓存

uv 使用积极的缓存策略，以避免重新下载（和重新构建）在先前运行中已经访问过的依赖项。

uv 的缓存语义根据依赖项的性质而有所不同：

- **对于注册表依赖项**（例如从 PyPI 下载的），uv 遵循 HTTP 缓存头。
- **对于直接 URL 依赖项**，uv 遵循 HTTP 缓存头，并且还基于 URL 本身进行缓存。
- **对于 Git 依赖项**，uv 基于完全解析的 Git 提交哈希进行缓存。因此，`uv pip compile` 在写入已解析的依赖项集合时，会将 Git 依赖项固定到特定的提交哈希。
- **对于本地依赖项**，uv 基于源归档文件（即本地的 `.whl` 或 `.tar.gz` 文件）的最后修改时间进行缓存。对于目录，uv 基于 `pyproject.toml`、`setup.py` 或 `setup.cfg` 文件的最后修改时间进行缓存。

如果您遇到缓存问题，uv 提供了一些应急方案：

- 要完全清除缓存，请运行 `uv cache clean`。要清除特定包的缓存，请运行 `uv cache clean <package-name>`。例如，`uv cache clean ruff` 将清除 `ruff` 包的缓存。
- 要强制 uv 重新验证所有依赖项的缓存数据，请在任何命令后传递 `--refresh` 参数（例如，`uv sync --refresh` 或 `uv pip install --refresh ...`）。
- 要强制 uv 重新验证特定依赖项的缓存数据，请在任何命令后传递 `--refresh-package` 参数（例如，`uv sync --refresh-package ruff` 或 `uv pip install --refresh-package ruff ...`）。
- 要强制 uv 忽略已安装的现有版本，请在任何安装命令后传递 `--reinstall` 参数（例如，`uv sync --reinstall` 或 `uv pip install --reinstall ...`）。（建议先运行 `uv cache clean <package-name>`，以确保在重新安装之前清除了缓存。）

作为一种特殊情况，uv 将始终重新构建并重新安装任何在命令行上显式传递的本地目录依赖项（例如，`uv pip install .`）。

## 动态元数据

默认情况下，uv _仅_ 在目录根目录中的 `pyproject.toml`、`setup.py` 或 `setup.cfg` 文件发生更改，或者添加或删除了 `src` 目录时，才会重新构建和重新安装本地目录依赖项（例如，可编辑安装）。这是一种启发式方法，在某些情况下，可能导致比预期更少的重新安装。

为了将附加信息纳入给定包的缓存键，您可以在 [`tool.uv.cache-keys`](https://docs.astral.sh/uv/reference/settings/#cache-keys) 下添加缓存键条目，它涵盖了文件路径和 Git 提交哈希。设置 [`tool.uv.cache-keys`](https://docs.astral.sh/uv/reference/settings/#cache-keys) 将替换默认值，因此任何必要的文件（如 `pyproject.toml`）仍应包含在用户定义的缓存键中。

例如，如果一个项目在 `pyproject.toml` 中指定依赖项，但使用 [`setuptools-scm`](https://pypi.org/project/setuptools-scm/) 来管理其版本，因此应该在提交哈希或依赖项更改时重新构建，您可以将以下内容添加到项目的 `pyproject.toml` 中：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "pyproject.toml" }, { git = { commit = true } }]
```

如果您的动态元数据包含了来自 Git 标签集合的信息，您可以扩展缓存键以包含标签：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "pyproject.toml" }, { git = { commit = true, tags = true } }]
```

类似地，如果一个项目从 `requirements.txt` 读取以填充其依赖项，您可以将以下内容添加到项目的 `pyproject.toml` 中：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "pyproject.toml" }, { file = "requirements.txt" }]
```

`file` 键支持 glob 模式，遵循 [`glob`](https://docs.rs/glob/0.3.1/glob/struct.Pattern.html) crate 的语法。例如，要在项目目录或其任何子目录中的 `.toml` 文件被修改时使缓存失效，请使用以下配置：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "**/*.toml" }]
```

!!! note

    使用 glob 模式可能会比较昂贵，因为 uv 可能需要遍历文件系统以确定是否有任何文件发生了更改。
    这反过来可能需要遍历大型或深度嵌套的目录。

类似地，如果一个项目依赖于一个环境变量，您可以将以下内容添加到项目的 `pyproject.toml` 中，以便在环境变量更改时使缓存失效：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "pyproject.toml" }, { env = "MY_ENV_VAR" }]
```

最后，要在创建或删除特定目录（如 `src`）时使项目缓存失效，请将以下内容添加到项目的 `pyproject.toml` 中：

```toml title="pyproject.toml"
[tool.uv]
cache-keys = [{ file = "pyproject.toml" }, { dir = "src" }]
```

请注意，`dir` 键仅跟踪目录本身的更改，而不跟踪目录内的任意更改。

作为一种应急方案，如果一个项目使用了 `tool.uv.cache-keys` 未涵盖的 `dynamic` 元数据，您可以通过将项目添加到 `tool.uv.reinstall-package` 列表来指示 uv _总是_ 重新构建和重新安装它：

```toml title="pyproject.toml"
[tool.uv]
reinstall-package = ["my-package"]
```

这将强制 uv 在每次运行时重新构建和重新安装 `my-package`，无论包的 `pyproject.toml`、`setup.py` 或 `setup.cfg` 文件是否已更改。

## 缓存安全性

可以安全地同时运行多个 uv 命令，即使是针对同一个虚拟环境。uv 的缓存被设计为线程安全且仅支持追加操作，因此对多个并发读取器和写入器具有鲁棒性。uv 在安装时对目标虚拟环境应用基于文件的锁，以避免跨进程的并发修改。

请注意，在其他 uv 命令运行时修改 uv 缓存（例如，`uv cache clean`）是_不_安全的，并且_永远不_安全直接修改缓存（例如，通过删除文件或目录）。

## 清理缓存

uv 提供了几种不同的机制来从缓存中删除条目：

- `uv cache clean` 从缓存目录中删除_所有_缓存条目，完全清空它。
- `uv cache clean ruff` 删除 `ruff` 包的所有缓存条目，对于使单个或有限数量包的缓存失效很有用。
- `uv cache prune` 删除所有_未使用_的缓存条目。例如，缓存目录可能包含在先前 uv 版本中创建的、不再需要且可以安全删除的条目。定期运行 `uv cache prune` 是安全的，可以保持缓存目录的清洁。

## 持续集成中的缓存

在持续集成环境（如 GitHub Actions 或 GitLab CI）中缓存包安装产物以加速后续运行是很常见的。

默认情况下，uv 会缓存它从源代码构建的 wheel 以及它直接下载的预构建 wheel，以实现高性能的包安装。

然而，在持续集成环境中，持久化预构建 wheel 可能并不理想。对于 uv 来说，事实证明，_省略_预构建 wheel 的缓存（改为在每次运行时从注册表重新下载它们）通常更快。另一方面，缓存从源代码构建的 wheel 往往是值得的，因为 wheel 构建过程可能很昂贵，特别是对于扩展模块。

为了支持这种缓存策略，uv 提供了 `uv cache prune --ci` 命令，该命令从缓存中删除所有预构建的 wheel 和已解压的源码分发，但保留任何从源代码构建的 wheel。我们建议在持续集成作业结束时运行 `uv cache prune --ci` 以确保最大的缓存效率。有关示例，请参阅 [GitHub 集成指南](../guides/integration/github.md#caching)。

## 缓存目录

uv 按以下顺序确定缓存目录：

1. 临时缓存目录，如果请求了 `--no-cache`。
2. 通过 `--cache-dir`、`UV_CACHE_DIR` 或 [`tool.uv.cache-dir`](../reference/settings.md#cache-dir) 指定的特定缓存目录。
3. 系统合适的缓存目录，例如，在 Unix 上为 `$XDG_CACHE_HOME/uv` 或 `$HOME/.cache/uv`，在 Windows 上为 `%LOCALAPPDATA%\uv\cache`。

!!! note

    uv _总是_需要一个缓存目录。当请求 `--no-cache` 时，uv 仍将使用临时缓存在该单个调用内共享数据。

    在大多数情况下，应该使用 `--refresh` 而不是 `--no-cache` — 因为它将更新后续操作的缓存，但不会从缓存中读取。

为了性能，缓存目录位于与 uv 正在操作的 Python 环境相同的文件系统上非常重要。否则，uv 将无法从缓存链接文件到环境中，而是需要回退到缓慢的复制操作。

## 缓存版本控制

uv 缓存由多个存储桶组成（例如，用于 wheel 的存储桶、用于源码分发的存储桶、用于 Git 仓库的存储桶等等）。每个存储桶都进行了版本控制，这样，如果一个版本包含对缓存格式的破坏性更改，uv 将不会尝试读取或写入不兼容的缓存存储桶。

例如，uv 0.4.13 包含对核心元数据存储桶的破坏性更改。因此，存储桶版本从 v12 增加到 v13。在缓存版本内，保证更改既向前兼容又向后兼容。

由于缓存格式的更改伴随着缓存版本的更改，多个版本的 uv 可以安全地读取和写入同一个缓存目录。但是，如果在给定的两个 uv 版本之间缓存版本发生了变化，那么这些版本可能无法共享相同的基础缓存条目。

例如，对 uv 0.4.12 和 uv 0.4.13 使用单个共享缓存是安全的，尽管由于缓存版本的更改，缓存本身在核心元数据存储桶中可能包含重复的条目。