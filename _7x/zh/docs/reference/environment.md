# 环境变量

uv 定义并遵循以下环境变量：

### `UV_BREAK_SYSTEM_PACKAGES`
<small class="added-in">于 `0.1.32` 版本添加</small>

等效于 `--break-system-packages` 命令行参数。如果设置为 `true`，uv 将允许安装与系统已安装包冲突的包。

警告：`UV_BREAK_SYSTEM_PACKAGES=true` 旨在用于持续集成（CI）或容器化环境，应谨慎使用，因为修改系统 Python 可能导致意外行为。

### `UV_BUILD_CONSTRAINT`
<small class="added-in">于 `0.2.34` 版本添加</small>

等效于 `--build-constraints` 命令行参数。如果设置，uv 将使用此文件作为任何源分发构建的约束。使用空格分隔的文件列表。

### `UV_CACHE_DIR`
<small class="added-in">于 `0.0.5` 版本添加</small>

等效于 `--cache-dir` 命令行参数。如果设置，uv 将使用此目录进行缓存，而不是默认的缓存目录。

### `UV_COMPILE_BYTECODE`
<small class="added-in">于 `0.3.3` 版本添加</small>

等效于 `--compile-bytecode` 命令行参数。如果设置，uv 将在安装后将 Python 源文件编译为字节码。

### `UV_COMPILE_BYTECODE_TIMEOUT`
<small class="added-in">于 `0.7.22` 版本添加</small>

字节码编译的超时时间（以秒为单位）。

### `UV_CONCURRENT_BUILDS`
<small class="added-in">于 `0.1.43` 版本添加</small>

设置 uv 在任何给定时间并发构建的源分发的最大数量。

### `UV_CONCURRENT_DOWNLOADS`
<small class="added-in">于 `0.1.43` 版本添加</small>

设置 uv 在任何给定时间执行的并发下载的最大数量。

### `UV_CONCURRENT_INSTALLS`
<small class="added-in">于 `0.1.45` 版本添加</small>

控制安装和解压包时使用的线程数。

### `UV_CONFIG_FILE`
<small class="added-in">于 `0.1.34` 版本添加</small>

等效于 `--config-file` 命令行参数。期望一个指向本地 `uv.toml` 文件的路径，用作配置文件。

### `UV_CONSTRAINT`
<small class="added-in">于 `0.1.36` 版本添加</small>

等效于 `--constraints` 命令行参数。如果设置，uv 将使用此文件作为约束文件。使用空格分隔的文件列表。

### `UV_CREDENTIALS_DIR`
<small class="added-in">于 `0.8.15` 版本添加</small>

使用纯文本后端时，用于存储凭据的目录。

### `UV_CUSTOM_COMPILE_COMMAND`
<small class="added-in">于 `0.1.23` 版本添加</small>

等效于 `--custom-compile-command` 命令行参数。

用于在 `uv pip compile` 生成的 `requirements.txt` 文件的输出头中覆盖 uv。旨在用于从包装脚本内部调用 `uv pip compile` 的情况，以便在输出文件中包含包装脚本的名称。

### `UV_DEFAULT_INDEX`
<small class="added-in">于 `0.4.23` 版本添加</small>

等效于 `--default-index` 命令行参数。如果设置，uv 将在搜索包时使用此 URL 作为默认索引。

### `UV_DEV`
<small class="added-in">于 `0.8.7` 版本添加</small>

等效于 `--dev` 命令行参数。如果设置，uv 将包含开发依赖项。

### `UV_DOWNLOAD_URL`
<small class="added-in">于 `0.8.4` 版本添加</small>

使用独立安装程序下载 uv 的 URL。默认情况下，从 uv 的 GitHub Releases 安装。为向后兼容，也支持别名 `INSTALLER_DOWNLOAD_URL`。

### `UV_ENV_FILE`
<small class="added-in">于 `0.4.30` 版本添加</small>

执行 `uv run` 命令时，用于加载环境变量的 `.env` 文件。

### `UV_EXCLUDE`
<small class="added-in">于 `0.9.8` 版本添加</small>

等效于 `--excludes` 命令行参数。如果设置，uv 将使用此文件作为排除文件。使用空格分隔的文件列表。

### `UV_EXCLUDE_NEWER`
<small class="added-in">于 `0.2.12` 版本添加</small>

等效于 `--exclude-newer` 命令行参数。如果设置，uv 将排除在指定日期之后发布的分发版。

### `UV_EXTRA_INDEX_URL`
<small class="added-in">于 `0.1.3` 版本添加</small>

等效于 `--extra-index-url` 命令行参数。如果设置，uv 将在搜索包时使用此空格分隔的 URL 列表作为额外索引。（已弃用：请改用 `UV_INDEX`。）

### `UV_FIND_LINKS`
<small class="added-in">于 `0.4.19` 版本添加</small>

等效于 `--find-links` 命令行参数。如果设置，uv 将使用此逗号分隔的附加位置列表来搜索包。

### `UV_FORK_STRATEGY`
<small class="added-in">于 `0.5.9` 版本添加</small>

等效于 `--fork-strategy` 参数。控制在通用解析期间的版本选择策略。

### `UV_FROZEN`
<small class="added-in">于 `0.4.25` 版本添加</small>

等效于 `--frozen` 命令行参数。如果设置，uv 将在不更新 `uv.lock` 文件的情况下运行。

### `UV_GITHUB_TOKEN`
<small class="added-in">于 `0.4.10` 版本添加</small>

等效于 `self update` 的 `--token` 参数。用于身份验证的 GitHub token。

### `UV_GIT_LFS`
<small class="added-in">于 `0.5.19` 版本添加</small>

在从 Git 仓库安装包时，启用获取存储在 Git LFS 中的文件。

### `UV_HTTP_RETRIES`
<small class="added-in">于 `0.7.21` 版本添加</small>

HTTP 请求的重试次数。（默认值：3）

### `UV_HTTP_TIMEOUT`
<small class="added-in">于 `0.1.7` 版本添加</small>

HTTP 请求的超时时间（以秒为单位）。（默认值：30 秒）

### `UV_INDEX`
<small class="added-in">于 `0.4.23` 版本添加</small>

等效于 `--index` 命令行参数。如果设置，uv 将在搜索包时使用此空格分隔的 URL 列表作为额外索引。

### `UV_INDEX_STRATEGY`
<small class="added-in">于 `0.1.29` 版本添加</small>

等效于 `--index-strategy` 命令行参数。

例如，如果设置为 `unsafe-best-match`，uv 将考虑跨所有索引 URL 可用的给定包的所有版本，而不是将其搜索限制在包含该包的第一个索引 URL。

### `UV_INDEX_URL`
<small class="added-in">于 `0.0.5` 版本添加</small>

等效于 `--index-url` 命令行参数。如果设置，uv 将在搜索包时使用此 URL 作为默认索引。（已弃用：请改用 `UV_DEFAULT_INDEX`。）

### `UV_INDEX_{name}_PASSWORD`
<small class="added-in">于 `0.4.23` 版本添加</small>

为命名索引提供 HTTP 基本身份验证密码。

`name` 参数是索引的名称。例如，给定一个名为 `foo` 的索引，环境变量键将为 `UV_INDEX_FOO_PASSWORD`。

### `UV_INDEX_{name}_USERNAME`
<small class="added-in">于 `0.4.23` 版本添加</small>

为命名索引提供 HTTP 基本身份验证用户名。

`name` 参数是索引的名称。例如，给定一个名为 `foo` 的索引，环境变量键将为 `UV_INDEX_FOO_USERNAME`。

### `UV_INIT_BUILD_BACKEND`
<small class="added-in">于 `0.8.2` 版本添加</small>

等效于 `uv init` 的 `--build-backend` 参数。确定创建新项目时使用的默认后端。

### `UV_INSECURE_HOST`
<small class="added-in">于 `0.3.5` 版本添加</small>

等效于 `--allow-insecure-host` 参数。

### `UV_INSECURE_NO_ZIP_VALIDATION`
<small class="added-in">于 `0.8.6` 版本添加</small>

禁用对流式 wheel 和基于 ZIP 的源分发的 ZIP 验证。

警告：禁用 ZIP 验证会绕过完整性检查，并允许 uv 安装潜在的恶意 ZIP 文件，从而可能使您的系统面临安全风险。如果 uv 因验证失败而拒绝 ZIP 文件，则该文件很可能格式错误；请考虑向包维护者提交问题报告。

### `UV_INSTALLER_GHE_BASE_URL`
<small class="added-in">于 `0.5.0` 版本添加</small>

使用独立安装程序和 `self update` 功能下载 uv 的 URL，以替代默认的 GitHub Enterprise URL。

### `UV_INSTALLER_GITHUB_BASE_URL`
<small class="added-in">于 `0.5.0` 版本添加</small>

使用独立安装程序和 `self update` 功能下载 uv 的 URL，以替代默认的 GitHub URL。

### `UV_INSTALL_DIR`
<small class="added-in">于 `0.5.0` 版本添加</small>

使用独立安装程序和 `self update` 功能安装 uv 的目录。默认为 `~/.local/bin`。

### `UV_ISOLATED`
<small class="added-in">于 `0.8.14` 版本添加</small>

等效于 `--isolated` 命令行参数。如果设置，uv 将避免发现 `pyproject.toml` 或 `uv.toml` 文件。

### `UV_KEYRING_PROVIDER`
<small class="added-in">于 `0.1.19` 版本添加</small>

等效于 `--keyring-provider` 命令行参数。如果设置，uv 将使用此值作为密钥环提供程序。

### `UV_LIBC`
<small class="added-in">于 `0.7.22` 版本添加</small>

在 Python 版本请求中填充当前平台时，覆盖在 Linux 系统上由环境确定的 libc。选项包括：`gnu`、`gnueabi`、`gnueabihf`、`musl` 和 `none`。

### `UV_LINK_MODE`
<small class="added-in">于 `0.1.40` 版本添加</small>

等效于 `--link-mode` 命令行参数。如果设置，uv 将使用此值作为链接模式。

### `UV_LOCKED`
<small class="added-in">于 `0.4.25` 版本添加</small>

等效于 `--locked` 命令行参数。如果设置，uv 将断言 `uv.lock` 文件保持不变。

### `UV_LOG_CONTEXT`
<small class="added-in">于 `0.6.4` 版本添加</small>

向日志消息添加额外的上下文和结构。

如果日志记录未启用（例如，通过 `RUST_LOG` 或 `-v`），则此变量无效。

### `UV_MANAGED_PYTHON`
<small class="added-in">于 `0.6.8` 版本添加</small>

要求使用 uv 管理的 Python 版本。

### `UV_NATIVE_TLS`
<small class="added-in">于 `0.1.19` 版本添加</small>

等效于 `--native-tls` 命令行参数。如果设置为 `true`，uv 将使用系统的信任存储而不是捆绑的 `webpki-roots` crate。

### `UV_NO_BINARY`
<small class="added-in">于 `0.5.30` 版本添加</small>

等效于 `--no-binary` 命令行参数。如果设置，uv 将从源代码安装所有包。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。

### `UV_NO_BINARY_PACKAGE`
<small class="added-in">于 `0.5.30` 版本添加</small>

等效于 `--no-binary-package` 命令行参数。如果设置，uv 将不会对给定的空格分隔包列表使用预构建的 wheel。

### `UV_NO_BUILD`
<small class="added-in">于 `0.1.40` 版本添加</small>

等效于 `--no-build` 命令行参数。如果设置，uv 将不会构建源分发版。

### `UV_NO_BUILD_ISOLATION`
<small class="added-in">于 `0.1.40` 版本添加</small>

等效于 `--no-build-isolation` 命令行参数。如果设置，uv 将在构建源分发版时跳过隔离。

### `UV_NO_BUILD_PACKAGE`
<small class="added-in">于 `0.6.5` 版本添加</small>

等效于 `--no-build-package` 命令行参数。如果设置，uv 将不会为给定的空格分隔包列表构建源分发版。

### `UV_NO_CACHE`
<small class="added-in">于 `0.1.2` 版本添加</small>

等效于 `--no-cache` 命令行参数。如果设置，uv 将不会对任何操作使用缓存。

### `UV_NO_CONFIG`
<small class="added-in">于 `0.2.30` 版本添加</small>

等效于 `--no-config` 命令行参数。如果设置，uv 将不会从当前目录、父目录或用户配置目录读取任何配置文件。

### `UV_NO_DEFAULT_GROUPS`
<small class="added-in">于 `0.9.9` 版本添加</small>

等效于 `--no-default-groups` 命令行参数。如果设置，uv 将不会选择在 `tool.uv.default-groups` 中定义的默认依赖组。

### `UV_NO_DEV`
<small class="added-in">于 `0.8.7` 版本添加</small>

等效于 `--no-dev` 命令行参数。如果设置，uv 将排除开发依赖项。

### `UV_NO_EDITABLE`
<small class="added-in">于 `0.6.15` 版本添加</small>

等效于 `--no-editable` 命令行参数。如果设置，uv 将以非可编辑方式安装或导出任何可编辑依赖项，包括项目和任何工作区成员。

### `UV_NO_ENV_FILE`
<small class="added-in">于 `0.4.30` 版本添加</small>

在执行 `uv run` 命令时忽略 `.env` 文件。

### `UV_NO_GITHUB_FAST_PATH`
<small class="added-in">于 `0.7.13` 版本添加</small>

禁用允许 uv 在某些情况下跳过 `git fetch` 的 GitHub 特定请求。

### `UV_NO_GROUP`
<small class="added-in">于 `0.9.8` 版本添加</small>

等效于 `--no-group` 命令行参数。如果设置，uv 将禁用指定的空格分隔依赖组列表。

### `UV_NO_HF_TOKEN`
<small class="added-in">于 `0.8.1` 版本添加</small>

禁用 Hugging Face 身份验证，即使设置了 `HF_TOKEN`。

### `UV_NO_INSTALLER_METADATA`
<small class="added-in">于 `0.5.7` 版本添加</small>

跳过将 `uv` 安装程序元数据文件（例如，`INSTALLER`、`REQUESTED` 和 `direct_url.json`）写入 site-packages 的 `.dist-info` 目录。

### `UV_NO_MANAGED_PYTHON`
<small class="added-in">于 `0.6.8` 版本添加</small>

禁用使用 uv 管理的 Python 版本。

### `UV_NO_MODIFY_PATH`
<small class="added-in">于 `0.8.4` 版本添加</small>

在使用独立安装程序和 `self update` 功能安装 uv 时，避免修改 `PATH` 环境变量。为向后兼容，也支持别名 `INSTALLER_NO_MODIFY_PATH`。

### `UV_NO_PROGRESS`
<small class="added-in">于 `0.2.28` 版本添加</small>

等效于 `--no-progress` 命令行参数。禁用所有进度输出。例如，旋转器和进度条。

### `UV_NO_SOURCES`
<small class="added-in">于 `0.9.8` 版本添加</small>

等效于 `--no-sources` 命令行参数。如果设置，uv 在解析依赖项时将忽略 `[tool.uv.sources]` 注解。

### `UV_NO_SYNC`
<small class="added-in">于 `0.4.18` 版本添加</small>

等效于 `--no-sync` 命令行参数。如果设置，uv 将跳过更新环境。

### `UV_NO_VERIFY_HASHES`
<small class="added-in">于 `0.5.3` 版本添加</small>

等效于 `--no-verify-hashes` 参数。禁用对 `requirements.txt` 文件的哈希验证。

### `UV_NO_WRAP`
<small class="added-in">于 `0.0.5` 版本添加</small>

用于禁用诊断信息的自动换行。

### `UV_OFFLINE`
<small class="added-in">于 `0.5.9` 版本添加</small>

等效于 `--offline` 命令行参数。如果设置，uv 将禁用网络访问。

### `UV_OVERRIDE`
<small class="added-in">于 `0.2.22` 版本添加</small>

等效于 `--overrides` 命令行参数。如果设置，uv 将使用此文件作为覆盖文件。使用空格分隔的文件列表。

### `UV_PRERELEASE`
<small class="added-in">于 `0.1.16` 版本添加</small>

等效于 `--prerelease` 命令行参数。例如，如果设置为 `allow`，uv 将允许所有依赖项使用预发布版本。

### `UV_PREVIEW`
<small class="added-in">于 `0.1.37` 版本添加</small>

等效于 `--preview` 参数。启用预览模式。

### `UV_PREVIEW_FEATURES`
<small class="added-in">于 `0.8.4` 版本添加</small>

等效于 `--preview-features` 参数。启用特定的预览功能。

### `UV_PROJECT`
<small class="added-in">于 `0.4.4` 版本添加</small>

等效于 `--project` 命令行参数。

### `UV_PROJECT_ENVIRONMENT`
<small class="added-in">于 `0.4.4` 版本添加</small>

指定用于项目虚拟环境的目录路径。

有关更多详细信息，请参阅[项目文档](../concepts/projects/config.md#project-environment-path)。

### `UV_PUBLISH_CHECK_URL`
<small class="added-in">于 `0.4.30` 版本添加</small>

如果文件已存在于索引上，则不上传。该值是索引的 URL。

### `UV_PUBLISH_INDEX`
<small class="added-in">于 `0.5.8` 版本添加</small>

等效于 `uv publish` 中的 `--index` 命令行参数。如果设置，uv 将使用配置中具有此名称的索引进行发布。

### `UV_PUBLISH_PASSWORD`
<small class="added-in">于 `0.4.16` 版本添加</small>

等效于 `uv publish` 中的 `--password` 命令行参数。如果设置，uv 将使用此密码进行发布。

### `UV_PUBLISH_TOKEN`
<small class="added-in">ed in `0.4.16` 版本添加</small>

等效于 `uv publish` 中的 `--token` 命令行参数。如果设置，uv 将使用此 token（使用用户名 `__token__`）进行发布。

### `UV_PUBLISH_URL`
<small class="added-in">于 `0.4.16` 版本添加</small>

等效于 `--publish-url` 命令行参数。与 `uv publish` 一起使用的索引上传端点的 URL。

### `UV_PUBLISH_USERNAME`
<small class="added-in">于 `0.4.16` 版本添加</small>

等效于 `uv publish` 中的 `--username` 命令行参数。如果设置，uv 将使用此用户名进行发布。

### `UV_PYPY_INSTALL_MIRROR`
<small class="added-in">于 `0.2.35` 版本添加</small>

托管的 PyPy 安装从 [python.org](https://downloads.python.org/) 下载。

可以将此变量设置为镜像 URL 以使用不同的 PyPy 安装源。提供的 URL 将替换例如 `https://downloads.python.org/pypy/pypy3.8-v7.3.7-osx64.tar.bz2` 中的 `https://downloads.python.org/pypy`。通过使用 `file://` URL 方案，可以从本地目录读取分发版。

### `UV_PYTHON`
<small class="added-in">于 `0.1.40` 版本添加</small>

等效于 `--python` 命令行参数。如果设置为路径，uv 将在所有操作中使用此 Python 解释器。

### `UV_PYTHON_BIN_DIR`
<small class="added-in">于 `0.4.29` 版本添加</small>

指定放置指向已安装的托管 Python 可执行文件链接的目录。

### `UV_PYTHON_CACHE_DIR`
<small class="added-in">于 `0.7.0` 版本添加</small>

指定在安装之前用于缓存托管 Python 安装存档的目录。

### `UV_PYTHON_CPYTHON_BUILD`
<small class="added-in">于 `0.8.14` 版本添加</small>

将托管的 CPython 版本固定到特定的构建版本。

对于 CPython，这应该是构建日期（例如，"20250814"）。

### `UV_PYTHON_DOWNLOADS`
<small class="added-in">于 `0.3.2` 版本添加</small>

等效于 [`python-downloads`](../reference/settings.md#python-downloads) 设置，并且在禁用时等效于 `--no-python-downloads` 选项。控制 uv 是否应允许 Python 下载。

### `UV_PYTHON_DOWNLOADS_JSON_URL`
<small class="added-in">于 `0.6.13` 版本添加</small>

托管 Python 安装信息被硬编码在 `uv` 二进制文件中。

可以将此变量设置为指向 JSON 格式的 Python 安装列表的本地路径或 URL，以覆盖硬编码的列表。

这允许自定义下载 URL 或使用比此 `uv` 构建中硬编码的版本稍旧或稍新的 Python 版本。

### `UV_PYTHON_GRAALPY_BUILD`
<small class="added-in">于 `0.8.14` 版本添加</small>

将托管的 GraalPy 版本固定到特定的构建版本。

对于 GraalPy，这应该是 GraalPy 版本（例如，"24.2.2"）。

### `UV_PYTHON_INSTALL_BIN`
<small class="added-in">于 `0.8.0` 版本添加</small>

是否将 Python 可执行文件安装到 `UV_PYTHON_BIN_DIR` 目录中。

### `UV_PYTHON_INSTALL_DIR`
<small class="added-in">于 `0.2.22` 版本添加</small>

指定用于存储托管 Python 安装的目录。

### `UV_PYTHON_INSTALL_MIRROR`
<small class="added-in">于 `0.2.35` 版本添加</small>

托管 Python 安装从 Astral 的 [`python-build-standalone`](https://github.com/astral-sh/python-build-standalone) 项目下载。

可以将此变量设置为镜像 URL 以使用不同的 Python 安装源。提供的 URL 将替换例如 `https://github.com/astral-sh/python-build-standalone/releases/download/20240713/cpython-3.12.4%2B20240713-aarch64-apple-darwin-install_only.tar.gz` 中的 `https://github.com/astral-sh/python-build-standalone/releases/download`。通过使用 `file://` URL 方案，可以从本地目录读取分发版。

### `UV_PYTHON_INSTALL_REGISTRY`
<small class="added-in">于 `0.8.0` 版本添加</small>

是否将 Python 可执行文件安装到 Windows 注册表中。

### `UV_PYTHON_PREFERENCE`
<small class="added-in">于 `0.3.2` 版本添加</small>

控制 uv 应优先使用系统 Python 版本还是托管 Python 版本。

### `UV_PYTHON_PYODIDE_BUILD`
<small class="added-in">于 `0.8.14` 版本添加</small>

将托管的 Pyodide 版本固定到特定的构建版本。

对于 Pyodide，这应该是 Pyodide 版本（例如，"0.28.1"）。

### `UV_PYTHON_PYPY_BUILD`
<small class="added-in">于 `0.8.14` 版本添加</small>

将托管的 PyPy 版本固定到特定的构建版本。

对于 PyPy，这应该是 PyPy 版本（例如，"7.3.20"）。

### `UV_REQUEST_TIMEOUT`
<small class="added-in">于 `0.1.6` 版本添加</small>

HTTP 请求的超时时间（以秒为单位）。等效于 `UV_HTTP_TIMEOUT`。

### `UV_REQUIRE_HASHES`
<small class="added-in">于 `0.1.34` 版本添加</small>

等效于 `--require-hashes` 命令行参数。如果设置为 `true`，uv 将要求所有依赖项在需求文件中指定了哈希值。

### `UV_RESOLUTION`
<small class="added-in">于 `0.1.27` 版本添加</small>

等效于 `--resolution` 命令行参数。例如，如果设置为 `lowest-direct`，uv 将安装所有直接依赖项的最低兼容版本。

### `UV_S3_ENDPOINT_URL`
<small class="added-in">于 `0.8.21` 版本添加</small>

被视为 S3 兼容存储端点的 URL。发往此端点的请求将使用 AWS Signature Version 4 基于 `AWS_ACCESS_KEY_ID`、`AWS_SECRET_ACCESS_KEY`、`AWS_PROFILE` 和 `AWS_CONFIG_FILE` 环境变量进行签名。

### `UV_SKIP_WHEEL_FILENAME_CHECK`
<small class="added-in">于 `0.8.23` 版本添加</small>

避免在安装 wheel 时验证 wheel 文件名是否与其内容匹配。这不推荐，因为文件名不一致的 wheel 应被视为无效，并由相关包维护者进行更正；但是，在极少数情况下，此选项可用于解决无效的构件问题。

### `UV_STACK_SIZE`
<small class="added-in">于 `0.0.5` 版本添加</small>

用于设置 uv 使用的堆栈大小。

值以字节为单位，如果 `UV_STACK_SIZE` 和 `RUST_MIN_STACK` 均未设置，uv 使用 4MB (4194304) 的堆栈。`UV_STACK_SIZE` 优先于 `RUST_MIN_STACK`。

与正常的 `RUST_MIN_STACK` 语义不同，这会影响主线程堆栈大小，因为我们实际上生成自己的 main2 线程来解决 Windows 真实主线程只有 1MB 的问题。该线程的大小为 `max(UV_STACK_SIZE, 1MB)`。

### `UV_SYSTEM_PYTHON`
<small class="added-in">于 `0.1.18` 版本添加</small>

等效于 `--system` 命令行参数。如果设置为 `true`，uv 将使用在系统 `PATH` 中找到的第一个 Python 解释器。

警告：`UV_SYSTEM_PYTHON=true` 旨在用于持续集成（CI）或容器化环境，应谨慎使用，因为修改系统 Python 可能导致意外行为。

### `UV_TEST_NO_HTTP_RETRY_DELAY`
<small class="added-in">于 `0.7.21` 版本添加</small>

用于在测试中禁用 HTTP 重试的延迟。

### `UV_TOOL_BIN_DIR`
<small class="added-in">于 `0.3.0` 版本添加</small>

指定用于安装工具可执行文件的 "bin" 目录。

### `UV_TOOL_DIR`
<small class="added-in">于 `0.2.16` 版本添加</small>

指定 uv 存储托管工具的目录。

### `UV_TORCH_BACKEND`
<small class="added-in">于 `0.6.9` 版本添加</small>

等效于 `--torch-backend` 命令行参数（例如，`cpu`、`cu126` 或 `auto`）。

### `UV_UNMANAGED_INSTALL`
<small class="added-in">于 `0.5.0` 版本添加</small>

在 CI 等临时环境中使用，用于将 uv 安装到特定路径，同时防止安装程序修改 shell 配置文件或环境变量。

### `UV_UPLOAD_HTTP_TIMEOUT`
<small class="added-in">于 `0.9.1` 版本添加</small>

仅用于上传 HTTP 请求的超时时间（以秒为单位）。（默认值：900 秒）

### `UV_VENV_CLEAR`
<small class="added-in">于 `0.8.0` 版本添加</small>

等效于 `--clear` 命令行参数。如果设置，uv 将删除目标路径上任何现有的文件或目录。

### `UV_VENV_SEED`
<small class="added-in">于 `0.5.21` 版本添加</small>

将由 `uv venv` 创建的虚拟环境中安装种子包（一个或多个：`pip`、`setuptools` 和 `wheel`）。

注意：`setuptools` 和 `wheel` 不包含在 Python 3.12+ 环境中。

### `UV_WORKING_DIRECTORY`
<small class="added-in">于 `0.9.1` 版本添加</small>

等效于 `--directory` 命令行参数。



## 外部定义的变量

uv 还读取以下外部定义的环境变量：

### `ALL_PROXY`
<small class="added-in">于 `0.1.38` 版本添加</small>

所有网络请求的通用代理。

### `ANDROID_API_LEVEL`
<small class="added-in">于 `0.8.16` 版本添加</small>

与 `--python-platform aarch64-linux-android` 及相关变体一起使用，用于设置 Android API 级别。（即，最低支持的 Android API 级别）。

默认为 `24`。

### `APPDATA`
<small class="added-in">于 `0.1.42` 版本添加</small>

Windows 系统上用户级配置目录的路径。

### `AWS_ACCESS_KEY_ID`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 访问密钥 ID。

### `AWS_CONFIG_FILE`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 配置文件。

### `AWS_DEFAULT_REGION`
<small class="added-in">于 `0.8.21` 版本添加</small>

如果未设置 `AWS_REGION`，则签署 S3 请求时使用的默认 AWS 区域。

### `AWS_PROFILE`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 配置文件。

### `AWS_REGION`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 区域。

### `AWS_SECRET_ACCESS_KEY`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 秘密访问密钥。

### `AWS_SESSION_TOKEN`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 会话令牌。

### `AWS_SHARED_CREDENTIALS_FILE`
<small class="added-in">于 `0.8.21` 版本添加</small>

签署 S3 请求时使用的 AWS 共享凭据文件。

### `BASH_VERSION`
<small class="added-in">于 `0.1.28` 版本添加</small>

用于检测 Bash shell 的使用。

### `CLICOLOR_FORCE`
<small class="added-in">于 `0.1.32` 版本添加</small>

用于通过 `anstyle` 控制颜色。

### `COLUMNS`
<small class="added-in">于 `0.6.2` 版本添加</small>

覆盖用于换行的终端宽度。此变量不由 uv 直接读取。

这是一个准标准变量，例如在 `ncurses(3x)` 中有所描述。

### `CONDA_DEFAULT_ENV`
<small class="added-in">于 `0.5.0` 版本添加</small>

用于确定活动 Conda 环境的名称。

### `CONDA_PREFIX`
<small class="added-in">于 `0.0.5` 版本添加</small>

用于检测活动 Conda 环境的路径。

### `DEPENDABOT`
<small class="added-in">于 `next release` 版本添加</small>

用于确定我们是否在 Dependabot 中运行。

### `FISH_VERSION`
<small class="added-in">于 `0.1.28` 版本添加</small>

用于检测 Fish shell 的使用。

### `FORCE_COLOR`
<small class="added-in">于 `0.2.7` 版本添加</small>

无论终端是否支持，都强制彩色输出。

参见 [force-color.org](https://force-color.org)。

### `GITHUB_ACTIONS`
<small class="added-in">于 `0.4.16` 版本添加</small>

指示当前进程正在 GitHub Actions 中运行。

当设置为 `true` 时，`uv publish` 可能会尝试可信发布流程。

### `GITLAB_CI`
<small class="added-in">于 `0.8.18` 版本添加</small>

指示当前进程正在 GitLab CI 中运行。

当设置为 `true` 时，`uv publish` 可能会尝试可信发布流程。

### `HF_TOKEN`
<small class="added-in">于 `0.8.1` 版本添加</small>

Hugging Face 请求的身份验证令牌。设置后，uv 在向 `https://huggingface.co/` 及其任何子域发出请求时将使用此令牌。

### `HOME`
<small class="added-in">于 `0.0.5` 版本添加</small>

标准的 `HOME` 环境变量。

### `HTTPS_PROXY`
<small class="added-in">于 `0.1.38` 版本添加</small>

HTTPS 请求的代理。

### `HTTP_PROXY`
<small class="added-in">于 `0.1.38` 版本添加</small>

HTTP 请求的代理。

### `HTTP_TIMEOUT`
<small class="added-in">于 `0.1.7` 版本添加</small>

HTTP 请求的超时时间（以秒为单位）。等效于 `UV_HTTP_TIMEOUT`。

### `IPHONEOS_DEPLOYMENT_TARGET`
<small class="added-in">于 `0.8.16` 版本添加</small>

与 `--python-platform arm64-apple-ios` 及相关变体一起使用，用于设置部署目标（即，最低支持的 iOS 版本）。

默认为 `13.0`。

### `JPY_SESSION_NAME`
<small class="added-in">于 `0.2.6` 版本添加</small>

用于检测是否在 Jupyter notebook 内部运行。

### `KSH_VERSION`
<small class="added-in">于 `0.2.33` 版本添加</small>

用于检测 Ksh shell 的使用。

### `LOCALAPPDATA`
<small class="added-in">于 `0.3.3` 版本添加</small>

用于查找 Microsoft Store Python 安装。

### `MACOSX_DEPLOYMENT_TARGET`
<small class="added-in">于 `0.1.42` 版本添加</small>

与 `--python-platform macos` 及相关变体一起使用，用于设置部署目标（即，最低支持的 macOS 版本）。

默认为 `13.0`，这是撰写本文时最新的非 EOL macOS 版本。

### `NETRC`
<small class="added-in">于 `0.1.16` 版本添加</small>

用于设置 .netrc 文件的位置。

### `NO_COLOR`
<small class="added-in">于 `0.2.7` 版本添加</small>

禁用彩色输出（优先于 `FORCE_COLOR`）。

参见 [no-color.org](https://no-color.org)。

### `NO_PROXY`
<small class="added-in">于 `0.1.38` 版本添加</small>

应绕过代理的主机名（例如，`example.com`）和/或模式（例如，`192.168.1.0/24`）的逗号分隔列表。

### `NU_VERSION`
<small class="added-in">于 `0.1.16` 版本添加</small>

用于检测 `NuShell` 的使用。

### `PAGER`
<small class="added-in">于 `0.4.18` 版本添加</small>

标准的 `PAGER` posix 环境变量。由 `uv` 用于配置适当的分页器。

### `PATH`
<small class="added-in">于 `0.0.5` 版本添加</small>

标准的 `PATH` 环境变量。

### `PROMPT`
<small class="added-in">于 `0.1.16` 版本添加</small>

用于检测 Windows 命令提示符（与 PowerShell 相对）的使用。

### `PWD`
<small class="added-in">于 `0.0.5` 版本添加</small>

标准的 `PWD` posix 环境变量。

### `PYC_INVALIDATION_MODE`
<small class="added-in">于 `0.1.7` 版本添加</small>

与 `--compile` 一起运行时使用的验证模式。

参见 [`PycInvalidationMode`](https://docs.python.org/3/library/py_compile.html#py_compile.PycInvalidationMode)。

### `PYTHONPATH`
<small class="added-in">于 `0.1.22` 版本添加</small>

将目录添加到 Python 模块搜索路径（例如，`PYTHONPATH=/path/to/modules`）。

### `PYX_API_KEY`
<small class="added-in">于 `0.8.15` 版本添加</small>

pyx API 密钥（例如，`sk-pyx-...`）。

### `PYX_API_URL`
<small class="added-in">于 `0.8.15` 版本添加</small>

pyx Simple API 服务器的 URL。

### `PYX_AUTH_TOKEN`
<small class="added-in">于 `0.8.15` 版本添加</small>

pyx 身份验证令牌（例如，`eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...`），由 `uv auth token` 输出。

### `PYX_CDN_DOMAIN`
<small class="added-in">于 `0.8.15` 版本添加</small>

pyx CDN 的域名。

### `PYX_CREDENTIALS_DIR`
<small class="added-in">于 `0.8.15` 版本添加</small>

指定 uv 存储 pyx 凭据的目录。

### `RUST_BACKTRACE`
<small class="added-in">于 `0.7.22` 版本添加</small>

如果设置，可用于在发生 panic 时显示更多堆栈跟踪详细信息。uv 在 Windows 上尤其使用它来在平台异常期间显示更多详细信息。

例如：

* `RUST_BACKTRACE=1` 将打印简短的回溯。
* `RUST_BACKTRACE=full` 将打印完整的回溯。

有关更多信息，请参阅 [Rust 回溯文档](https://doc.rust-lang.org/std/backtrace/index.html)。

### `RUST_LOG`
<small class="added-in">于 `0.0.5` 版本添加</small>

如果设置，uv 将使用此值作为其 `--verbose` 输出的日志级别。接受与 `tracing_subscriber` crate 兼容的任何过滤器。

例如：

* `RUST_LOG=uv=debug` 等效于在命令行中添加 `--verbose`。
* `RUST_LOG=trace` 将启用跟踪级别的日志记录。

有关更多信息，请参阅 [tracing 文档](https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#example-syntax)。

### `RUST_MIN_STACK`
<small class="added-in">于 `0.5.19` 版本添加</small>

用于设置 uv 使用的堆栈大小。

值以字节为单位，如果 `UV_STACK_SIZE` 和 `RUST_MIN_STACK` 均未设置，uv 使用 4MB (4194304) 的堆栈。`UV_STACK_SIZE` 优先于 `RUST_MIN_STACK`。

建议设置 `UV_STACK_SIZE`，因为 `RUST_MIN_STACK` 也会影响子进程，例如使用 Rust 代码的构建后端。

与正常的 `RUST_MIN_STACK` 语义不同，这会影响主线程堆栈大小，因为我们实际上生成自己的 main2 线程来解决 Windows 真实主线程只有 1MB 的问题。该线程的大小为 `max(RUST_MIN_STACK, 1MB)`。

### `SHELL`
<small class="added-in">于 `0.1.16` 版本添加</small>

标准的 `SHELL` posix 环境变量。

### `SSL_CERT_DIR`
<small class="added-in">于 `0.9.10` 版本添加</small>

用于 SSL 连接的证书包的自定义路径。
支持使用平台特定分隔符（Unix 上为 `:`，Windows 上为 `;`）分隔的多个条目。

设置时优先于 `UV_NATIVE_TLS`。

### `SSL_CERT_FILE`
<small class="added-in">于 `0.1.14` 版本添加</small>

用于 SSL 连接的自定义证书包文件路径。

设置时优先于 `UV_NATIVE_TLS`。

### `SSL_CLIENT_CERT`
<small class="added-in">于 `0.2.11` 版本添加</small>

如果设置，uv 将使用此文件进行 mTLS 身份验证。这应该是一个包含 PEM 格式证书和私钥的单个文件。

### `SYSTEMDRIVE`
<small class="added-in">于 `0.4.26` 版本添加</small>

Windows 系统上系统级配置目录的路径。

### `TRACING_DURATIONS_FILE`
<small class="added-in">于 `0.0.5` 版本添加</small>

用于通过 `tracing-durations-export` 功能创建跟踪持续时间文件。

### `USERPROFILE`
<small class="added-in">于 `0.0.5` 版本添加</small>

Windows 系统上用户配置文件根目录的路径。

### `UV`
<small class="added-in">于 `0.6.0` 版本添加</small>

用于调用 uv 的二进制文件的路径。

这会传播到 uv 生成的所有子进程。

如果可执行文件是通过符号链接调用的，某些平台将返回符号链接的路径，而其他平台将返回符号链接目标的路径。

有关安全注意事项，请参阅 <https://doc.rust-lang.org/std/env/fn.current_exe.html#security>。

### `VIRTUAL_ENV`
<small class="added-in">于 `0.0.5` 版本添加</small>

用于检测已激活的虚拟环境。

### `VIRTUAL_ENV_DISABLE_PROMPT`
<small class="added-in">于 `0.0.5` 版本添加</small>

如果在激活虚拟环境之前将其设置为 `1`，则不会将虚拟环境名称前置到终端提示符。

### `XDG_BIN_HOME`
<small class="added-in">于 `0.2.16` 版本添加</small>

安装可执行文件的目录路径。

### `XDG_CACHE_HOME`
<small class="added-in">于 `0.1.17` 版本添加</small>

Unix 系统上缓存目录的路径。

### `XDG_CONFIG_DIRS`
<small class="added-in">于 `0.4.26` 版本添加</small>

Unix 系统上系统级配置目录的路径。

### `XDG_CONFIG_HOME`
<small class="added-in">于 `0.1.34` 版本添加</small>

Unix 系统上用户级配置目录的路径。

### `XDG_DATA_HOME`
<small class="added-in">于 `0.2.16` 版本添加</small>

用于存储托管 Python 安装和工具的目录路径。

### `ZDOTDIR`
<small class="added-in">于 `0.2.25` 版本添加</small>

用于在使用 Zsh 时确定使用哪个 `.zshenv`。

### `ZSH_VERSION`
<small class="added-in">于 `0.1.28` 版本添加</small>

用于检测 Zsh shell 的使用。

### `_CONDA_ROOT`
<small class="added-in">于 `0.8.18` 版本添加</small>

用于确定 Conda 的根安装路径。