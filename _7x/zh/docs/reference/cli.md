# CLI 参考

## uv

一个极快的 Python 包管理器。

<h3 class="cli-reference">用法</h3>

```
uv [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-auth"><code>uv auth</code></a></dt><dd><p>管理认证</p></dd>
<dt><a href="#uv-run"><code>uv run</code></a></dt><dd><p>运行命令或脚本</p></dd>
<dt><a href="#uv-init"><code>uv init</code></a></dt><dd><p>创建新项目</p></dd>
<dt><a href="#uv-add"><code>uv add</code></a></dt><dd><p>向项目添加依赖</p></dd>
<dt><a href="#uv-remove"><code>uv remove</code></a></dt><dd><p>从项目移除依赖</p></dd>
<dt><a href="#uv-version"><code>uv version</code></a></dt><dd><p>读取或更新项目版本</p></dd>
<dt><a href="#uv-sync"><code>uv sync</code></a></dt><dd><p>更新项目环境</p></dd>
<dt><a href="#uv-lock"><code>uv lock</code></a></dt><dd><p>更新项目锁文件</p></dd>
<dt><a href="#uv-export"><code>uv export</code></a></dt><dd><p>将项目锁文件导出为替代格式</p></dd>
<dt><a href="#uv-tree"><code>uv tree</code></a></dt><dd><p>显示项目依赖树</p></dd>
<dt><a href="#uv-format"><code>uv format</code></a></dt><dd><p>格式化项目中的 Python 代码</p></dd>
<dt><a href="#uv-tool"><code>uv tool</code></a></dt><dd><p>运行和安装 Python 包提供的命令</p></dd>
<dt><a href="#uv-python"><code>uv python</code></a></dt><dd><p>管理 Python 版本和安装</p></dd>
<dt><a href="#uv-pip"><code>uv pip</code></a></dt><dd><p>使用 pip 兼容接口管理 Python 包</p></dd>
<dt><a href="#uv-venv"><code>uv venv</code></a></dt><dd><p>创建虚拟环境</p></dd>
<dt><a href="#uv-build"><code>uv build</code></a></dt><dd><p>将 Python 包构建为源码发行版和 wheel</p></dd>
<dt><a href="#uv-publish"><code>uv publish</code></a></dt><dd><p>上传发行版到索引</p></dd>
<dt><a href="#uv-cache"><code>uv cache</code></a></dt><dd><p>管理 uv 的缓存</p></dd>
<dt><a href="#uv-self"><code>uv self</code></a></dt><dd><p>管理 uv 可执行文件</p></dd>
<dt><a href="#uv-help"><code>uv help</code></a></dt><dd><p>显示命令的文档</p></dd>
</dl>

## uv auth

管理认证

<h3 class="cli-reference">用法</h3>

```
uv auth [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-auth-login"><code>uv auth login</code></a></dt><dd><p>登录服务</p></dd>
<dt><a href="#uv-auth-logout"><code>uv auth logout</code></a></dt><dd><p>登出服务</p></dd>
<dt><a href="#uv-auth-token"><code>uv auth token</code></a></dt><dd><p>显示服务的认证令牌</p></dd>
<dt><a href="#uv-auth-dir"><code>uv auth dir</code></a></dt><dd><p>显示 uv 凭据目录的路径</p></dd>
</dl>

### uv auth login

登录服务

<h3 class="cli-reference">用法</h3>

```
uv auth login [OPTIONS] <SERVICE>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-auth-login--service"><a href="#uv-auth-login--service"<code>SERVICE</code></a></dt><dd><p>要登录的服务的域名或 URL</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-auth-login--allow-insecure-host"><a href="#uv-auth-login--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-auth-login--cache-dir"><a href="#uv-auth-login--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-auth-login--color"><a href="#uv-auth-login--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-auth-login--config-file"><a href="#uv-auth-login--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-auth-login--directory"><a href="#uv-auth-login--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-auth-login--help"><a href="#uv-auth-login--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-auth-login--keyring-provider"><a href="#uv-auth-login--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>用于存储凭据的密钥环提供程序。</p>
<p>对于 <code>login</code>，仅支持 <code>--keyring-provider native</code>，它通过 uv 内置的集成使用系统密钥环。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用密钥环进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-auth-login--managed-python"><a href="#uv-auth-login--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-login--native-tls"><a href="#uv-auth-login--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-auth-login--no-cache"><a href="#uv-auth-login--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-auth-login--no-config"><a href="#uv-auth-login--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-auth-login--no-managed-python"><a href="#uv-auth-login--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-login--no-progress"><a href="#uv-auth-login--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-auth-login--no-python-downloads"><a href="#uv-auth-login--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-auth-login--offline"><a href="#uv-auth-login--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-auth-login--password"><a href="#uv-auth-login--password"><code>--password</code></a> <i>password</i></dt><dd><p>用于服务的密码。</p>
<p>使用 <code>-</code> 从 stdin 读取密码。</p>
</dd><dt id="uv-auth-login--project"><a href="#uv-auth-login--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-auth-login--quiet"><a href="#uv-auth-login--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-auth-login--token"><a href="#uv-auth-login--token"><code>--token</code></a>, <code>-t</code> <i>token</i></dt><dd><p>用于服务的令牌。</p>
<p>用户名将设置为 <code>__token__</code>。</p>
<p>使用 <code>-</code> 从 stdin 读取令牌。</p>
</dd><dt id="uv-auth-login--username"><a href="#uv-auth-login--username"><code>--username</code></a>, <code>-u</code> <i>username</i></dt><dd><p>用于服务的用户名</p>
</dd><dt id="uv-auth-login--verbose"><a href="#uv-auth-login--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv auth logout

登出服务

<h3 class="cli-reference">用法</h3>

```
uv auth logout [OPTIONS] <SERVICE>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-auth-logout--service"><a href="#uv-auth-logout--service"<code>SERVICE</code></a></dt><dd><p>要登出的服务的域名或 URL</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-auth-logout--allow-insecure-host"><a href="#uv-auth-logout--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--cache-dir"><a href="#uv-auth-logout--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--color"><a href="#uv-auth-logout--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-auth-logout--config-file"><a href="#uv-auth-logout--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--directory"><a href="#uv-auth-logout--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--help"><a href="#uv-auth-logout--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-auth-logout--keyring-provider"><a href="#uv-auth-logout--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>用于存储凭据的密钥环提供程序。</p>
<p>对于 <code>logout</code>，仅支持 <code>--keyring-provider native</code>，它通过 uv 内置的集成使用系统密钥环。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用密钥环进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-auth-logout--managed-python"><a href="#uv-auth-logout--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--native-tls"><a href="#uv-auth-logout--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--no-cache"><a href="#uv-auth-logout--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--no-config"><a href="#uv-auth-logout--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--no-managed-python"><a href="#uv-auth-logout--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--no-progress"><a href="#uv-auth-logout--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--no-python-downloads"><a href="#uv-auth-logout--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-auth-logout--offline"><a href="#uv-auth-logout--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--project"><a href="#uv-auth-logout--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-auth-logout--quiet"><a href="#uv-auth-logout--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-auth-logout--username"><a href="#uv-auth-logout--username"><code>--username</code></a>, <code>-u</code> <i>username</i></dt><dd><p>要登出的用户名</p>
</dd><dt id="uv-auth-logout--verbose"><a href="#uv-auth-logout--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv auth token

显示服务的认证令牌

<h3 class="cli-reference">用法</h3>

```
uv auth token [OPTIONS] <SERVICE>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-auth-token--service"><a href="#uv-auth-token--service"<code>SERVICE</code></a></dt><dd><p>要查找的服务的域名或 URL</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-auth-token--allow-insecure-host"><a href="#uv-auth-token--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-auth-token--cache-dir"><a href="#uv-auth-token--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-auth-token--color"><a href="#uv-auth-token--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-auth-token--config-file"><a href="#uv-auth-token--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-auth-token--directory"><a href="#uv-auth-token--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-auth-token--help"><a href="#uv-auth-token--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-auth-token--keyring-provider"><a href="#uv-auth-token--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>用于读取凭据的密钥环提供程序</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用密钥环进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-auth-token--managed-python"><a href="#uv-auth-token--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-token--native-tls"><a href="#uv-auth-token--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-auth-token--no-cache"><a href="#uv-auth-token--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-auth-token--no-config"><a href="#uv-auth-token--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-auth-token--no-managed-python"><a href="#uv-auth-token--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-token--no-progress"><a href="#uv-auth-token--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-auth-token--no-python-downloads"><a href="#uv-auth-token--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-auth-token--offline"><a href="#uv-auth-token--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-auth-token--project"><a href="#uv-auth-token--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-auth-token--quiet"><a href="#uv-auth-token--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-auth-token--username"><a href="#uv-auth-token--username"><code>--username</code></a>, <code>-u</code> <i>username</i></dt><dd><p>要查找的用户名</p>
</dd><dt id="uv-auth-token--verbose"><a href="#uv-auth-token--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv auth dir

显示 uv 凭据目录的路径。

默认情况下，凭据存储在 Unix 上的 uv 数据目录 `$XDG_DATA_HOME/uv/credentials` 或 `$HOME/.local/share/uv/credentials` 以及 Windows 上的 `%APPDATA%\uv\data\credentials` 中。

凭据目录可以通过 `$UV_CREDENTIALS_DIR` 覆盖。

仅当使用纯文本后端（而不是使用系统密钥环的本机后端）时，凭据才存储在此目录中。

<h3 class="cli-reference">用法</h3>

```
uv auth dir [OPTIONS] [SERVICE]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-auth-dir--service"><a href="#uv-auth-dir--service"<code>SERVICE</code></a></dt><dd><p>要查找的服务的域名或 URL</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-auth-dir--allow-insecure-host"><a href="#uv-auth-dir--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--cache-dir"><a href="#uv-auth-dir--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--color"><a href="#uv-auth-dir--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-auth-dir--config-file"><a href="#uv-auth-dir--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--directory"><a href="#uv-auth-dir--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--help"><a href="#uv-auth-dir--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-auth-dir--managed-python"><a href="#uv-auth-dir--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--native-tls"><a href="#uv-auth-dir--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--no-cache"><a href="#uv-auth-dir--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--no-config"><a href="#uv-auth-dir--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--no-managed-python"><a href="#uv-auth-dir--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--no-progress"><a href="#uv-auth-dir--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--no-python-downloads"><a href="#uv-auth-dir--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-auth-dir--offline"><a href="#uv-auth-dir--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--project"><a href="#uv-auth-dir--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-auth-dir--quiet"><a href="#uv-auth-dir--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-auth-dir--verbose"><a href="#uv-auth-dir--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv run

运行命令或脚本。

确保命令在 Python 环境中运行。

当与以 `.py` 结尾的文件或 HTTP(S) URL 一起使用时，该文件将被视为脚本并使用 Python 解释器运行，即 `uv run file.py` 等效于 `uv run python file.py`。对于 URL，脚本会在执行前临时下载。如果脚本包含内联依赖元数据，它将被安装到一个隔离的临时环境中。当与 `-` 一起使用时，输入将从 stdin 读取，并被视为 Python 脚本。

在项目中使用时，将在调用命令之前创建和更新项目环境。

在项目外部使用时，如果在当前目录或父目录中可以找到虚拟环境，则命令将在该环境中运行。否则，命令将在发现的解释器的环境中运行。

命令（或脚本）之后的参数不会被解释为 uv 的参数。所有 uv 的选项必须在命令之前提供，例如 `uv run --verbose foo`。可以使用 `--` 来分隔命令和 uv 选项以增加清晰度，例如 `uv run --python 3.12 -- python`。

<h3 class="cli-reference">用法</h3>

```
uv run [OPTIONS] [COMMAND]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-run--active"><a href="#uv-run--active"><code>--active</code></a></dt><dd><p>优先使用活动的虚拟环境而不是项目的虚拟环境。</p>
<p>如果项目虚拟环境处于活动状态或没有虚拟环境处于活动状态，则此选项无效。</p>
</dd><dt id="uv-run--all-extras"><a href="#uv-run--all-extras"><code>--all-extras</code></a></dt><dd><p>包含所有可选依赖。</p>
<p>可选依赖通过 <code>pyproject.toml</code> 中的 <code>project.optional-dependencies</code> 定义。</p>
<p>此选项仅在项目中运行时可用。</p>
</dd><dt id="uv-run--all-groups"><a href="#uv-run--all-groups"><code>--all-groups</code></a></dt><dd><p>包含所有依赖组的依赖。</p>
<p><code>--no-group</code> 可用于排除特定组。</p>
</dd><dt id="uv-run--all-packages"><a href="#uv-run--all-packages"><code>--all-packages</code></a></dt><dd><p>安装所有工作区成员后运行命令。</p>
<p>工作区的环境（<code>.venv</code>）被更新以包含所有工作区成员。</p>
<p>通过 <code>--extra</code>、<code>--group</code> 或相关选项指定的任何附加项或组将应用于所有工作区成员。</p>
</dd><dt id="uv-run--allow-insecure-host"><a href="#uv-run--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-run--cache-dir"><a href="#uv-run--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-run--color"><a href="#uv-run--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-run--compile-bytecode"><a href="#uv-run--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在第一次导入模块时延迟执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以保持一致性。与 pip 一样，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-run--config-file"><a href="#uv-run--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-run--config-setting"><a href="#uv-run--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-run--config-settings-package"><a href="#uv-run--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-run--default-index"><a href="#uv-run--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的仓库（简单仓库 API）或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-run--directory"><a href="#uv-run--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-run--env-file"><a href="#uv-run--env-file"><code>--env-file</code></a> <i>env-file</i></dt><dd><p>从 <code>.env</code> 文件加载环境变量。</p>
<p>可以多次提供，后续文件将覆盖先前文件中定义的值。</p>
<p>也可以通过 <code>UV_ENV_FILE</code> 环境变量设置。</p></dd><dt id="uv-run--exact"><a href="#uv-run--exact"><code>--exact</code></a></dt><dd><p>执行精确同步，移除多余的包。</p>
<p>启用后，uv 将从环境中移除任何多余的包。默认情况下，<code>uv run</code> 将做出满足要求所需的最小更改。</p>
</dd><dt id="uv-run--exclude-newer"><a href="#uv-run--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-run--exclude-newer-package"><a href="#uv-run--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-run--extra"><a href="#uv-run--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>包含来自指定附加名称的可选依赖。</p>
<p>可以多次提供。</p>
<p>可选依赖通过 <code>pyproject.toml</code> 中的 <code>project.optional-dependencies</code> 定义。</p>
<p>此选项仅在项目中运行时可用。</p>
</dd><dt id="uv-run--extra-index-url"><a href="#uv-run--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的仓库（简单仓库 API）或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-run--find-links"><a href="#uv-run--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的包之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源码发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-run--fork-strategy"><a href="#uv-run--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>：优化为每个包选择最少数量的版本。如果旧版本与更广泛支持的 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>：优化为每个支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-run--frozen"><a href="#uv-run--frozen"><code>--frozen</code></a></dt><dd><p>运行而不更新 <code>uv.lock</code> 文件。</p>
<p>不检查锁文件是否是最新的，而是使用锁文件中的版本作为真实来源。如果锁文件丢失，uv 将退出并报错。如果 <code>pyproject.toml</code> 包含尚未包含在锁文件中的依赖项更改，则它们将不会出现在环境中。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-run--group"><a href="#uv-run--group"><code>--group</code></a> <i>group</i></dt><dd><p>包含来自指定依赖组的依赖。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-run--gui-script"><a href="#uv-run--gui-script"><code>--gui-script</code></a></dt><dd><p>将给定路径作为 Python GUI 脚本运行。</p>
<p>使用 <code>--gui-script</code> 将尝试将路径解析为 PEP 723 脚本并使用 <code>pythonw.exe</code> 运行它，无论其扩展名如何。仅在 Windows 上可用。</p>
</dd><dt id="uv-run--help"><a href="#uv-run--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-run--index"><a href="#uv-run--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的仓库（简单仓库 API）或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>索引名称不支持作为值。相对路径必须使用 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-run--index-strategy"><a href="#uv-run--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了“依赖混淆”攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名，优先选择找到的“最佳”版本。如果一个包版本在多个索引中，仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-run--index-url"><a href="#uv-run--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的仓库（简单仓库 API）或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-run--isolated"><a href="#uv-run--isolated"><code>--isolated</code></a></dt><dd><p>在隔离的虚拟环境中运行命令。</p>
<p>通常，出于性能考虑会重用项目环境。此选项强制为项目使用新环境，在依赖项和需求声明之间强制执行严格的隔离。</p>
<p>项目仍使用可编辑安装。</p>
<p>当与 <code>--with</code> 或 <code>--with-requirements</code> 一起使用时，额外的依赖项仍将在第二个环境中分层。</p>
<p>也可以通过 <code>UV_ISOLATED</code> 环境变量设置。</p></dd><dt id="uv-run--keyring-provider"><a href="#uv-run--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试对索引 URL 使用 <code>keyring</code> 进行身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用密钥环进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-run--link-mode"><a href="#uv-run--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过移除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-run--locked"><a href="#uv-run--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求锁文件是最新的。如果锁文件丢失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-run--managed-python"><a href="#uv-run--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-run--module"><a href="#uv-run--module"><code>--module</code></a>, <code>-m</code></dt><dd><p>运行 Python 模块。</p>
<p>等效于 <code>python -m &lt;module&gt;</code>。</p>
</dd><dt id="uv-run--native-tls"><a href="#uv-run--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-run--no-binary"><a href="#uv-run--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-run--no-binary-package"><a href="#uv-run--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-run--no-build"><a href="#uv-run--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源码发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源码发行版的缓存 wheel，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-run--no-build-isolation"><a href="#uv-run--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源码发行版时禁用隔离。</p>
<p>假定 PEP 518 指定的构建依赖已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-run--no-build-isolation-package"><a href="#uv-run--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源码发行版时禁用隔离。</p>
<p>假定包的 PEP 518 指定的构建依赖已安装。</p>
</dd><dt id="uv-run--no-build-package"><a href="#uv-run--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源码发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-run--no-cache"><a href="#uv-run--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-run--no-config"><a href="#uv-run--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-run--no-default-groups"><a href="#uv-run--no-default-groups"><code>--no-default-groups</code></a></dt><dd><p>忽略默认依赖组。</p>
<p>uv 默认包含 <code>tool.uv.default-groups</code> 中定义的组。这会禁用该选项，但是，仍然可以使用 <code>--group</code> 包含特定组。</p>
<p>也可以通过 <code>UV_NO_DEFAULT_GROUPS</code> 环境变量设置。</p></dd><dt id="uv-run--no-dev"><a href="#uv-run--no-dev"><code>--no-dev</code></a></dt><dd><p>禁用开发依赖组。</p>
<p>此选项是 <code>--no-group dev</code> 的别名。请参阅 <code>--no-default-groups</code> 以改为禁用所有默认组。</p>
<p>此选项仅在项目中运行时可用。</p>
<p>也可以通过 <code>UV_NO_DEV</code> 环境变量设置。</p></dd><dt id="uv-run--no-editable"><a href="#uv-run--no-editable"><code>--no-editable</code></a></dt><dd><p>将任何可编辑依赖项（包括项目和任何工作区成员）安装为非可编辑</p>
<p>也可以通过 <code>UV_NO_EDITABLE</code> 环境变量设置。</p></dd><dt id="uv-run--no-env-file"><a href="#uv-run--no-env-file"><code>--no-env-file</code></a></dt><dd><p>避免从 <code>.env</code> 文件读取环境变量</p>
<p>也可以通过 <code>UV_NO_ENV_FILE</code> 环境变量设置。</p></dd><dt id="uv-run--no-extra"><a href="#uv-run--no-extra"><code>--no-extra</code></a> <i>no-extra</i></dt><dd><p>如果提供了 <code>--all-extras</code>，则排除指定的可选依赖。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-run--no-group"><a href="#uv-run--no-group"><code>--no-group</code></a> <i>no-group</i></dt><dd><p>禁用指定的依赖组。</p>
<p>此选项始终优先于默认组、<code>--all-groups</code> 和 <code>--group</code>。</p>
<p>可以多次提供。</p>
<p>也可以通过 <code>UV_NO_GROUP</code> 环境变量设置。</p></dd><dt id="uv-run--no-index"><a href="#uv-run--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖和通过 <code>--find-links</code> 提供的依赖</p>
</dd><dt id="uv-run--no-managed-python"><a href="#uv-run--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-run--no-progress"><a href="#uv-run--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-run--no-project"><a href="#uv-run--no-project"><code>--no-project</code></a>, <code>--no_workspace</code></dt><dd><p>避免发现项目或工作区。</p>
<p>不在当前目录和父目录中搜索项目，而是在由 <code>--with</code> 需求填充的隔离临时环境中运行。</p>
<p>如果虚拟环境处于活动状态或在当前目录或父目录中找到，它将像没有项目或工作区一样被使用。</p>
</dd><dt id="uv-run--no-python-downloads"><a href="#uv-run--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-run--no-sources"><a href="#uv-run--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-run--no-sync"><a href="#uv-run--no-sync"><code>--no-sync</code></a></dt><dd><p>避免同步虚拟环境。</p>
<p>意味着 <code>--frozen</code>，因为项目依赖将被忽略（即锁文件不会被更新，因为无论如何环境都不会被同步）。</p>
<p>也可以通过 <code>UV_NO_SYNC</code> 环境变量设置。</p></dd><dt id="uv-run--offline"><a href="#uv-run--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-run--only-dev"><a href="#uv-run--only-dev"><code>--only-dev</code></a></dt><dd><p>仅包含开发依赖组。</p>
<p>项目及其依赖将被省略。</p>
<p>此选项是 <code>--only-group dev</code> 的别名。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-run--only-group"><a href="#uv-run--only-group"><code>--only-group</code></a> <i>only-group</i></dt><dd><p>仅包含来自指定依赖组的依赖。</p>
<p>项目及其依赖将被省略。</p>
<p>可以多次提供。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-run--package"><a href="#uv-run--package"><code>--package</code></a> <i>package</i></dt><dd><p>在工作区中的特定包中运行命令。</p>
<p>如果工作区成员不存在，uv 将退出并报错。</p>
</dd><dt id="uv-run--prerelease"><a href="#uv-run--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>：不允许所有预发布版本</li>
<li><code>allow</code>：允许所有预发布版本</li>
<li><code>if-necessary</code>：如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>：对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>：如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-run--project"><a href="#uv-run--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-run--python"><a href="#uv-run--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于运行环境的 Python 解释器。</p>
<p>如果解释器请求由发现的环境满足，则将使用该环境。</p>
<p>请参阅 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-run--python-platform"><a href="#uv-run--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装需求的平台。</p>
<p>表示为“目标三元组”，一个描述目标平台 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标为 macOS (Darwin) 时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与<em>目标</em>平台兼容的 wheel；因此，安装的发行版可能与<em>当前</em>平台不兼容。相反，从源码构建的任何发行版可能与<em>目标</em>平台不兼容，因为它们将为<em>当前</em>平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>：<code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>：<code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>：<code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>：64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>：ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>：32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>：x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>：基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>：x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>：ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>：ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>：<code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>：RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>：<code>x86_64</code> 目标，用于 <code>manylinux2014</code> 平台。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_17</code> 平台</li>
<li><code>x86_64-manylinux_2_28</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_28</code> 平台</li>
<li><code>x86_64-manylinux_2_31</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_31</code> 平台</li>
<li><code>x86_64-manylinux_2_32</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_32</code> 平台</li>
<li><code>x86_64-manylinux_2_33</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_33</code> 平台</li>
<li><code>x86_64-manylinux_2_34</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_34</code> 平台</li>
<li><code>x86_64-manylinux_2_35</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_35</code> 平台</li>
<li><code>x86_64-manylinux_2_36</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_36</code> 平台</li>
<li><code>x86_64-manylinux_2_37</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_37</code> 平台</li>
<li><code>x86_64-manylinux_2_38</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_38</code> 平台</li>
<li><code>x86_64-manylinux_2_39</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_39</code> 平台</li>
<li><code>x86_64-manylinux_2_40</code>：<code>x86_64</code> 目标，用于 <code>manylinux_2_40</code> 平台</li>
<li><code>aarch64-manylinux2014</code>：ARM64 目标，用于 <code>manylinux2014</code> 平台。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>：ARM64 目标，用于 <code>manylinux_2_17</code> 平台</li>
<li><code>aarch64-manylinux_2_28</code>：ARM64 目标，用于 <code>manylinux_2_28</code> 平台</li>
<li><code>aarch64-manylinux_2_31</code>：ARM64 目标，用于 <code>manylinux_2_31</code> 平台</li>
<li><code>aarch64-manylinux_2_32</code>：ARM64 目标，用于 <code>manylinux_2_32</code> 平台</li>
<li><code>aarch64-manylinux_2_33</code>：ARM64 目标，用于 <code>manylinux_2_33</code> 平台</li>
<li><code>aarch64-manylinux_2_34</code>：ARM64 目标，用于 <code>manylinux_2_34</code> 平台</li>
<li><code>aarch64-manylinux_2_35</code>：ARM64 目标，用于 <code>manylinux_2_35</code> 平台</li>
<li><code>aarch64-manylinux_2_36</code>：ARM64 目标，用于 <code>manylinux_2_36</code> 平台</li>
<li><code>aarch64-manylinux_2_37</code>：ARM64 目标，用于 <code>manylinux_2_37</code> 平台</li>
<li><code>aarch64-manylinux_2_38</code>：ARM64 目标，用于 <code>manylinux_2_38</code> 平台</li>
<li><code>aarch64-manylinux_2_39</code>：ARM64 目标，用于 <code>manylinux_2_39</code> 平台</li>
<li><code>aarch64-manylinux_2_40</code>：ARM64 目标，用于 <code>manylinux_2_40</code> 平台</li>
<li><code>aarch64-linux-android</code>：ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>：<code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>：使用 Pyodide 2024 平台的 wasm32 目标。旨在与 Python 3.12 一起使用</li>
<li><code>arm64-apple-ios</code>：iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>：iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>：iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-run--quiet"><a href="#uv-run--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-run--refresh"><a href="#uv-run--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-run--refresh-package"><a href="#uv-run--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-run--reinstall"><a href="#uv-run--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-run--reinstall-package"><a href="#uv-run--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-run--resolution"><a href="#uv-run--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>为给定包需求在不同兼容版本之间选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>：解析每个包的最高兼容版本</li>
<li><code>lowest</code>：解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>：解析任何直接依赖的最低兼容版本，以及任何传递依赖的最高兼容版本</li>
</ul></dd><dt id="uv-run--script"><a href="#uv-run--script"><code>--script</code></a>, <code>-s</code></dt><dd><p>将给定路径作为 Python 脚本运行。</p>
<p>使用 <code>--script</code> 将尝试将路径解析为 PEP 723 脚本，无论其扩展名如何。</p>
</dd><dt id="uv-run--upgrade"><a href="#uv-run--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-run--upgrade-package"><a href="#uv-run--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-run--verbose"><a href="#uv-run--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-run--with"><a href="#uv-run--with"><code>--with</code></a>, <code>-w</code> <i>with</i></dt><dd><p>运行并安装给定的包。</p>
<p>在项目中使用时，这些依赖将分层在项目环境之上，位于一个单独的临时环境中。这些依赖允许与项目指定的依赖冲突。</p>
</dd><dt id="uv-run--with-editable"><a href="#uv-run--with-editable"><code>--with-editable</code></a> <i>with-editable</i></dt><dd><p>以可编辑模式运行并安装给定的包。</p>
<p>在项目中使用时，这些依赖将分层在项目环境之上，位于一个单独的临时环境中。这些依赖允许与项目指定的依赖冲突。</p>
</dd><dt id="uv-run--with-requirements"><a href="#uv-run--with-requirements"><code>--with-requirements</code></a> <i>with-requirements</i></dt><dd><p>运行并安装给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、带有内联元数据的 <code>.py</code> 文件和 <code>pylock.toml</code>。</p>
<p>与 <code>--with</code> 相同的环境语义适用。</p>
<p>不允许使用 <code>pyproject.toml</code>、<code>setup.py</code> 或 <code>setup.cfg</code> 文件。</p>
</dd></dl>

## uv init

创建新项目。

遵循 `pyproject.toml` 规范。

如果目标位置已存在 `pyproject.toml`，uv 将退出并报错。

如果在目标路径的任何父目录中找到 `pyproject.toml`，则项目将作为父级的工作区成员添加。

某些项目状态在需要时才会创建，例如项目虚拟环境（`.venv`）和锁文件（`uv.lock`）在第一次同步时延迟创建。

<h3 class="cli-reference">用法</h3>

```
uv init [OPTIONS] [PATH]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-init--path"><a href="#uv-init--path"<code>PATH</code></a></dt><dd><p>用于项目/脚本的路径。</p>
<p>初始化应用程序或库时默认为当前工作目录；初始化脚本时需要。接受相对路径和绝对路径。</p>
<p>如果在目标路径的任何父目录中找到 <code>pyproject.toml</code>，则项目将作为父级的工作区成员添加，除非提供了 <code>--no-workspace</code>。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-init--allow-insecure-host"><a href="#uv-init--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-init--app"><a href="#uv-init--app"><code>--app</code></a>, <code>--application</code></dt><dd><p>为应用程序创建项目。</p>
<p>如果未请求 <code>--lib</code>，这是默认行为。</p>
<p>此类项目适用于 Web 服务器、脚本和命令行界面。</p>
<p>默认情况下，应用程序不打算作为 Python 包构建和分发。可以使用 <code>--package</code> 选项创建可分发的应用程序，例如，如果您想通过 PyPI 分发命令行界面。</p>
</dd><dt id="uv-init--author-from"><a href="#uv-init--author-from"><code>--author-from</code></a> <i>author-from</i></dt><dd><p>填写 <code>pyproject.toml</code> 中的 <code>authors</code> 字段。</p>
<p>默认情况下，uv 将尝试从某些来源（例如 Git）推断作者信息（<code>auto</code>）。使用 <code>--author-from git</code> 仅从 Git 配置推断。使用 <code>--author-from none</code> 避免推断作者信息。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：自动从某些来源（例如 Git）获取作者信息</li>
<li><code>git</code>：仅从 Git 配置获取作者信息</li>
<li><code>none</code>：不推断作者信息</li>
</ul></dd><dt id="uv-init--bare"><a href="#uv-init--bare"><code>--bare</code></a></dt><dd><p>仅创建 <code>pyproject.toml</code>。</p>
<p>禁用创建额外文件，如 <code>README.md</code>、<code>src/</code> 树、<code>.python-version</code> 文件等。</p>
</dd><dt id="uv-init--build-backend"><a href="#uv-init--build-backend"><code>--build-backend</code></a> <i>build-backend</i></dt><dd><p>为项目初始化选择的构建后端。</p>
<p>隐含设置 <code>--package</code>。</p>
<p>也可以通过 <code>UV_INIT_BUILD_BACKEND</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>uv</code>：使用 uv 作为项目构建后端</li>
<li><code>hatch</code>：使用 <a href="https://pypi.org/project/hatchling">hatchling</a> 作为项目构建后端</li>
<li><code>flit</code>：使用 <a href="https://pypi.org/project/flit-core">flit-core</a> 作为项目构建后端</li>
<li><code>pdm</code>：使用 <a href="https://pypi.org/project/pdm-backend">pdm-backend</a> 作为项目构建后端</li>
<li><code>poetry</code>：使用 <a href="https://pypi.org/project/poetry-core">poetry-core</a> 作为项目构建后端</li>
<li><code>setuptools</code>：使用 <a href="https://pypi.org/project/setuptools">setuptools</a> 作为项目构建后端</li>
<li><code>maturin</code>：使用 <a href="https://pypi.org/project/maturin">maturin</a> 作为项目构建后端</li>
<li><code>scikit</code>：使用 <a href="https://pypi.org/project/scikit-build-core">scikit-build-core</a> 作为项目构建后端</li>
</ul></dd><dt id="uv-init--cache-dir"><a href="#uv-init--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-init--color"><a href="#uv-init--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-init--config-file"><a href="#uv-init--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-init--description"><a href="#uv-init--description"><code>--description</code></a> <i>description</i></dt><dd><p>设置项目描述</p>
</dd><dt id="uv-init--directory"><a href="#uv-init--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-init--help"><a href="#uv-init--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-init--lib"><a href="#uv-init--lib"><code>--lib</code></a>, <code>--library</code></dt><dd><p>为库创建项目。</p>
<p>库是打算作为 Python 包构建和分发的项目。</p>
</dd><dt id="uv-init--managed-python"><a href="#uv-init--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-init--name"><a href="#uv-init--name"><code>--name</code></a> <i>name</i></dt><dd><p>项目的名称。</p>
<p>默认为目录的名称。</p>
</dd><dt id="uv-init--native-tls"><a href="#uv-init--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-init--no-cache"><a href="#uv-init--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-init--no-config"><a href="#uv-init--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-init--no-description"><a href="#uv-init--no-description"><code>--no-description</code></a></dt><dd><p>禁用项目的描述</p>
</dd><dt id="uv-init--no-managed-python"><a href="#uv-init--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-init--no-package"><a href="#uv-init--no-package"><code>--no-package</code></a></dt><dd><p>不设置项目作为 Python 包构建。</p>
<p>不包括项目的 <code>[build-system]</code>。</p>
<p>这是使用 <code>--app</code> 时的默认行为。</p>
</dd><dt id="uv-init--no-pin-python"><a href="#uv-init--no-pin-python"><code>--no-pin-python</code></a></dt><dd><p>不为项目创建 <code>.python-version</code> 文件。</p>
<p>默认情况下，uv 将创建一个 <code>.python-version</code> 文件，其中包含发现的 Python 解释器的次要版本，这将导致后续的 uv 命令使用该版本。</p>
</dd><dt id="uv-init--no-progress"><a href="#uv-init--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-init--no-python-downloads"><a href="#uv-init--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-init--no-readme"><a href="#uv-init--no-readme"><code>--no-readme</code></a></dt><dd><p>不创建 <code>README.md</code> 文件</p>
</dd><dt id="uv-init--no-workspace"><a href="#uv-init--no-workspace"><code>--no-workspace</code></a>, <code>--no-project</code></dt><dd><p>避免发现工作区并创建独立项目。</p>
<p>默认情况下，uv 在当前目录或任何父目录中搜索工作区。</p>
</dd><dt id="uv-init--offline"><a href="#uv-init--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-init--package"><a href="#uv-init--package"><code>--package</code></a></dt><dd><p>设置项目作为 Python 包构建。</p>
<p>为项目定义 <code>[build-system]</code>。</p>
<p>这是使用 <code>--lib</code> 或 <code>--build-backend</code> 时的默认行为。</p>
<p>当使用 <code>--app</code> 时，这将包括一个 <code>[project.scripts]</code> 入口点并使用 <code>src/</code> 项目结构。</p>
</dd><dt id="uv-init--project"><a href="#uv-init--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-init--python"><a href="#uv-init--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于确定最低支持 Python 版本的 Python 解释器。</p>
<p>请参阅 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-init--quiet"><a href="#uv-init--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-init--script"><a href="#uv-init--script"><code>--script</code></a></dt><dd><p>创建脚本。</p>
<p>脚本是一个独立文件，其中嵌入了枚举其依赖项以及任何 Python 版本要求的元数据，如 PEP 723 规范中所定义。</p>
<p>PEP 723 脚本可以直接使用 <code>uv run</code> 执行。</p>
<p>默认情况下，添加对系统 Python 版本的要求；使用 <code>--python</code> 指定替代的 Python 版本要求。</p>
</dd><dt id="uv-init--vcs"><a href="#uv-init--vcs"><code>--vcs</code></a> <i>vcs</i></dt><dd><p>为项目初始化版本控制系统。</p>
<p>默认情况下，uv 将初始化一个 Git 仓库（<code>git</code>）。使用 <code>--vcs none</code> 明确避免初始化版本控制系统。</p>
<p>可能的值：</p>
<ul>
<li><code>git</code>：使用 Git 进行版本控制</li>
<li><code>none</code>：不使用任何版本控制系统</li>
</ul></dd><dt id="uv-init--verbose"><a href="#uv-init--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv add

向项目添加依赖项。

依赖项将被添加到项目的 `pyproject.toml` 文件中。

如果给定的依赖项已存在，它将被更新到新的版本限定符，除非它包含与现有限定符不同的标记，在这种情况下将为该依赖项添加另一个条目。

lockfile 和项目环境将被更新以反映添加的依赖项。要跳过更新 lockfile，请使用 `--frozen`。要跳过更新环境，请使用 `--no-sync`。

如果任何请求的依赖项无法找到，uv 将退出并报错，除非提供了 `--frozen` 标志，在这种情况下 uv 将逐字添加依赖项而不检查它们是否存在或与项目兼容。

uv 将在当前目录或任何父目录中搜索项目。如果找不到项目，uv 将退出并报错。

<h3 class="cli-reference">用法</h3>

```
uv add [OPTIONS] <PACKAGES|--requirements <REQUIREMENTS>>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-add--packages"><a href="#uv-add--packages"<code>PACKAGES</code></a></dt><dd><p>要添加的包，作为 PEP 508 要求（例如，<code>ruff==0.5.0</code>）</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-add--active"><a href="#uv-add--active"><code>--active</code></a></dt><dd><p>优先使用活动的虚拟环境而非项目的虚拟环境。</p>
<p>如果项目虚拟环境已激活或没有虚拟环境处于活动状态，则此选项无效。</p>
</dd><dt id="uv-add--allow-insecure-host"><a href="#uv-add--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如，<code>localhost</code>）、主机-端口对（例如，<code>localhost:8080</code>）或 URL（例如，<code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证并可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-add--bounds"><a href="#uv-add--bounds"><code>--bounds</code></a> <i>bounds</i></dt><dd><p>添加依赖项时使用的版本限定符类型。</p>
<p>向项目添加依赖项时，如果未提供约束或 URL，则会根据包的最新兼容版本添加约束。默认情况下，使用下限约束，例如 <code>&gt;=1.2.3</code>。</p>
<p>当提供 <code>--frozen</code> 时，不执行解析，并且始终添加没有约束的依赖项。</p>
<p>此选项处于预览状态，可能在未来的任何版本中更改。</p>
<p>可能的值：</p>
<ul>
<li><code>lower</code>:  仅下限，例如 <code>&gt;=1.2.3</code></li>
<li><code>major</code>:  允许相同的主版本，类似于 semver 脱字符，例如 <code>&gt;=1.2.3, &lt;2.0.0</code></li>
<li><code>minor</code>:  允许相同的次版本，类似于 semver 波浪号，例如 <code>&gt;=1.2.3, &lt;1.3.0</code></li>
<li><code>exact</code>:  固定确切的版本，例如 <code>==1.2.3</code></li>
</ul></dd><dt id="uv-add--branch"><a href="#uv-add--branch"><code>--branch</code></a> <i>branch</i></dt><dd><p>从 Git 添加依赖项时使用的分支</p>
</dd><dt id="uv-add--cache-dir"><a href="#uv-add--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-add--color"><a href="#uv-add--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-add--compile-bytecode"><a href="#uv-add--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在首次导入模块时惰性执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-add--config-file"><a href="#uv-add--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>要用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-add--config-setting"><a href="#uv-add--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-add--config-settings-package"><a href="#uv-add--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给 PEP 517 构建后端以用于特定包的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-add--constraints"><a href="#uv-add--constraints"><code>--constraints</code></a>, <code>--constraint</code>, <code>-c</code> <i>constraints</i></dt><dd><p>使用给定的需求文件约束版本。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的需求的<em>版本</em>。约束将<em>不会</em>添加到项目的 <code>pyproject.toml</code> 文件中，但在依赖项解析期间将<em>会</em>被遵守。</p>
<p>这相当于 pip 的 <code>--constraint</code> 选项。</p>
<p>也可以通过 <code>UV_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-add--default-index"><a href="#uv-add--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-add--dev"><a href="#uv-add--dev"><code>--dev</code></a></dt><dd><p>将需求添加到开发依赖组。</p>
<p>此选项是 <code>--group dev</code> 的别名。</p>
<p>也可以通过 <code>UV_DEV</code> 环境变量设置。</p></dd><dt id="uv-add--directory"><a href="#uv-add--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-add--editable"><a href="#uv-add--editable"><code>--editable</code></a></dt><dd><p>以可编辑模式添加需求</p>
</dd><dt id="uv-add--exclude-newer"><a href="#uv-add--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-add--exclude-newer-package"><a href="#uv-add--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-add--extra"><a href="#uv-add--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>要为依赖项启用的额外功能。</p>
<p>可以多次提供。</p>
<p>要将此依赖项添加到可选的额外功能中，请参阅 <code>--optional</code>。</p>
</dd><dt id="uv-add--extra-index-url"><a href="#uv-add--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-add--find-links"><a href="#uv-add--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如，<code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-add--fork-strategy"><a href="#uv-add--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-add--frozen"><a href="#uv-add--frozen"><code>--frozen</code></a></dt><dd><p>添加依赖项而不重新锁定项目。</p>
<p>项目环境将不会同步。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-add--group"><a href="#uv-add--group"><code>--group</code></a> <i>group</i></dt><dd><p>将需求添加到指定的依赖组。</p>
<p>这些需求将不会包含在项目的发布元数据中。</p>
</dd><dt id="uv-add--help"><a href="#uv-add--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-add--index"><a href="#uv-add--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-add--index-strategy"><a href="#uv-add--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用返回给定包名称匹配的第一个索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-add--index-url"><a href="#uv-add--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-add--keyring-provider"><a href="#uv-add--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-add--link-mode"><a href="#uv-add--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即，写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-add--locked"><a href="#uv-add--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求 lockfile 是最新的。如果 lockfile 缺失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-add--managed-python"><a href="#uv-add--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-add--marker"><a href="#uv-add--marker"><code>--marker</code></a>, <code>-m</code> <i>marker</i></dt><dd><p>将此标记应用于所有添加的包</p>
</dd><dt id="uv-add--native-tls"><a href="#uv-add--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-add--no-binary"><a href="#uv-add--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-add--no-binary-package"><a href="#uv-add--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-add--no-build"><a href="#uv-add--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-add--no-build-isolation"><a href="#uv-add--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-add--no-build-isolation-package"><a href="#uv-add--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包在 PEP 518 中指定的构建依赖项已安装。</p>
</dd><dt id="uv-add--no-build-package"><a href="#uv-add--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-add--no-cache"><a href="#uv-add--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-add--no-config"><a href="#uv-add--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-add--no-index"><a href="#uv-add--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-add--no-install-local"><a href="#uv-add--no-install-local"><code>--no-install-local</code></a></dt><dd><p>不安装本地路径依赖项</p>
<p>跳过当前项目、工作区成员以及任何其他本地（路径或可编辑）包。仅安装远程/索引依赖项。在 Docker 构建中很有用，可以首先缓存繁重的第三方依赖项并单独分层本地包。</p>
<p>反向选项 <code>--only-install-local</code> 可用于<em>仅</em>安装本地包，排除所有远程依赖项。</p>
</dd><dt id="uv-add--no-install-package"><a href="#uv-add--no-install-package"><code>--no-install-package</code></a> <i>no-install-package</i></dt><dd><p>不安装给定的包。</p>
<p>默认情况下，项目的所有依赖项都安装到环境中。<code>--no-install-package</code> 选项允许排除特定包。请注意，这可能导致环境损坏，应谨慎使用。</p>
<p>反向选项 <code>--only-install-package</code> 可用于<em>仅</em>安装指定的包，排除所有其他包。</p>
</dd><dt id="uv-add--no-install-project"><a href="#uv-add--no-install-project"><code>--no-install-project</code></a></dt><dd><p>不安装当前项目。</p>
<p>默认情况下，当前项目及其所有依赖项都安装到环境中。<code>--no-install-project</code> 选项允许排除项目，但其所有依赖项仍会安装。这在诸如构建 Docker 镜像等情况下特别有用，其中将项目与其依赖项分开安装可以实现最佳层缓存。</p>
<p>反向选项 <code>--only-install-project</code> 可用于<em>仅</em>安装项目本身，排除所有依赖项。</p>
</dd><dt id="uv-add--no-install-workspace"><a href="#uv-add--no-install-workspace"><code>--no-install-workspace</code></a></dt><dd><p>不安装任何工作区成员，包括当前项目。</p>
<p>默认情况下，所有工作区成员及其依赖项都安装到环境中。<code>--no-install-workspace</code> 选项允许排除所有工作区成员，同时保留它们的依赖项。这在诸如构建 Docker 镜像等情况下特别有用，其中将工作区与其依赖项分开安装可以实现最佳层缓存。</p>
<p>反向选项 <code>--only-install-workspace</code> 可用于<em>仅</em>安装工作区成员，排除所有其他依赖项。</p>
</dd><dt id="uv-add--no-managed-python"><a href="#uv-add--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-add--no-progress"><a href="#uv-add--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-add--no-python-downloads"><a href="#uv-add--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-add--no-sources"><a href="#uv-add--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-add--no-sync"><a href="#uv-add--no-sync"><code>--no-sync</code></a></dt><dd><p>避免同步虚拟环境</p>
<p>也可以通过 <code>UV_NO_SYNC</code> 环境变量设置。</p></dd><dt id="uv-add--no-workspace"><a href="#uv-add--no-workspace"><code>--no-workspace</code></a></dt><dd><p>不要将依赖项添加为工作区成员。</p>
<p>默认情况下，当添加一个作为本地路径且在工作区目录内的依赖项时，uv 会将其添加为工作区成员；传递 <code>--no-workspace</code> 以将包添加为直接路径依赖项。</p>
</dd><dt id="uv-add--offline"><a href="#uv-add--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-add--optional"><a href="#uv-add--optional"><code>--optional</code></a> <i>optional</i></dt><dd><p>将需求添加到包的指定额外功能的可选依赖项中。</p>
<p>然后在安装项目时可以使用 <code>--extra</code> 标志激活该组。</p>
<p>要为此需求启用可选的额外功能，请参阅 <code>--extra</code>。</p>
</dd><dt id="uv-add--package"><a href="#uv-add--package"><code>--package</code></a> <i>package</i></dt><dd><p>将依赖项添加到工作区中的特定包</p>
</dd><dt id="uv-add--prerelease"><a href="#uv-add--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的限定符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-add--project"><a href="#uv-add--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-add--python"><a href="#uv-add--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于解析和同步的 Python 解释器。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-add--quiet"><a href="#uv-add--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-add--raw"><a href="#uv-add--raw"><code>--raw</code></a>, <code>--raw-sources</code></dt><dd><p>按原样添加依赖项。</p>
<p>默认情况下，uv 将使用 <code>tool.uv.sources</code> 部分记录 Git、本地、可编辑和直接 URL 需求的源信息。当提供 <code>--raw</code> 时，uv 会将源需求添加到 <code>project.dependencies</code>，而不是 <code>tool.uv.sources</code>。</p>
<p>此外，默认情况下，uv 会为您的依赖项添加边界，例如 <code>foo&gt;=1.0.0</code>。当提供 <code>--raw</code> 时，uv 将添加没有边界的依赖项。</p>
</dd><dt id="uv-add--refresh"><a href="#uv-add--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存的数据</p>
</dd><dt id="uv-add--refresh-package"><a href="#uv-add--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-add--reinstall"><a href="#uv-add--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-add--reinstall-package"><a href="#uv-add--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-add--requirements"><a href="#uv-add--requirements"><code>--requirements</code></a>, <code>--requirement</code>, <code>-r</code> <i>requirements</i></dt><dd><p>添加给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、带有内联元数据的 <code>.py</code> 文件、<code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code>。</p>
</dd><dt id="uv-add--resolution"><a href="#uv-add--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-add--rev"><a href="#uv-add--rev"><code>--rev</code></a> <i>rev</i></dt><dd><p>从 Git 添加依赖项时使用的提交</p>
</dd><dt id="uv-add--script"><a href="#uv-add--script"><code>--script</code></a> <i>script</i></dt><dd><p>将依赖项添加到指定的 Python 脚本，而不是项目。</p>
<p>如果提供，uv 将根据 PEP 723 将依赖项添加到脚本的内联元数据表中。如果不存在这样的内联元数据表，将创建并添加一个新的内联元数据表到脚本。当通过 <code>uv run</code> 执行时，uv 将为脚本创建一个临时环境，并安装所有内联依赖项。</p>
</dd><dt id="uv-add--tag"><a href="#uv-add--tag"><code>--tag</code></a> <i>tag</i></dt><dd><p>从 Git 添加依赖项时使用的标签</p>
</dd><dt id="uv-add--upgrade"><a href="#uv-add--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-add--upgrade-package"><a href="#uv-add--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-add--verbose"><a href="#uv-add--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-add--workspace"><a href="#uv-add--workspace"><code>--workspace</code></a></dt><dd><p>将依赖项添加为工作区成员。</p>
<p>默认情况下，uv 会将工作区目录内的路径依赖项添加为工作区成员。当与路径依赖项一起使用时，包将被添加到根 <code>pyproject.toml</code> 文件的工作区 <code>members</code> 列表中。</p>
</dd></dl>

## uv remove

从项目中移除依赖项。

依赖项将从项目的 `pyproject.toml` 文件中移除。

如果给定依赖项存在多个条目（即，每个条目具有不同的标记），则所有条目都将被移除。

lockfile 和项目环境将被更新以反映移除的依赖项。要跳过更新 lockfile，请使用 `--frozen`。要跳过更新环境，请使用 `--no-sync`。

如果任何请求的依赖项不在项目中，uv 将退出并报错。

如果包已手动安装在环境中（即，使用 `uv pip install`），则不会被 `uv remove` 移除。

uv 将在当前目录或任何父目录中搜索项目。如果找不到项目，uv 将退出并报错。

<h3 class="cli-reference">用法</h3>

```
uv remove [OPTIONS] <PACKAGES>...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-remove--packages"><a href="#uv-remove--packages"<code>PACKAGES</code></a></dt><dd><p>要移除的依赖项的名称（例如，<code>ruff</code>）</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-remove--active"><a href="#uv-remove--active"><code>--active</code></a></dt><dd><p>优先使用活动的虚拟环境而非项目的虚拟环境。</p>
<p>如果项目虚拟环境已激活或没有虚拟环境处于活动状态，则此选项无效。</p>
</dd><dt id="uv-remove--allow-insecure-host"><a href="#uv-remove--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如，<code>localhost</code>）、主机-端口对（例如，<code>localhost:8080</code>）或 URL（例如，<code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证并可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-remove--cache-dir"><a href="#uv-remove--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-remove--color"><a href="#uv-remove--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-remove--compile-bytecode"><a href="#uv-remove--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在首次导入模块时惰性执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-remove--config-file"><a href="#uv-remove--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>要用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-remove--config-setting"><a href="#uv-remove--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-remove--config-settings-package"><a href="#uv-remove--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给 PEP 517 构建后端以用于特定包的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-remove--default-index"><a href="#uv-remove--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-remove--dev"><a href="#uv-remove--dev"><code>--dev</code></a></dt><dd><p>从开发依赖组中移除包。</p>
<p>此选项是 <code>--group dev</code> 的别名。</p>
<p>也可以通过 <code>UV_DEV</code> 环境变量设置。</p></dd><dt id="uv-remove--directory"><a href="#uv-remove--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-remove--exclude-newer"><a href="#uv-remove--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-remove--exclude-newer-package"><a href="#uv-remove--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-remove--extra-index-url"><a href="#uv-remove--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-remove--find-links"><a href="#uv-remove--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如，<code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-remove--fork-strategy"><a href="#uv-remove--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-remove--frozen"><a href="#uv-remove--frozen"><code>--frozen</code></a></dt><dd><p>移除依赖项而不重新锁定项目。</p>
<p>项目环境将不会同步。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-remove--group"><a href="#uv-remove--group"><code>--group</code></a> <i>group</i></dt><dd><p>从指定的依赖组中移除包</p>
</dd><dt id="uv-remove--help"><a href="#uv-remove--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-remove--index"><a href="#uv-remove--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-remove--index-strategy"><a href="#uv-remove--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用返回给定包名称匹配的第一个索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-remove--index-url"><a href="#uv-remove--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-remove--keyring-provider"><a href="#uv-remove--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-remove--link-mode"><a href="#uv-remove--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即，写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-remove--locked"><a href="#uv-remove--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求 lockfile 是最新的。如果 lockfile 缺失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-remove--managed-python"><a href="#uv-remove--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-remove--native-tls"><a href="#uv-remove--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-remove--no-binary"><a href="#uv-remove--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-remove--no-binary-package"><a href="#uv-remove--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-remove--no-build"><a href="#uv-remove--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-remove--no-build-isolation"><a href="#uv-remove--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-remove--no-build-isolation-package"><a href="#uv-remove--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包在 PEP 518 中指定的构建依赖项已安装。</p>
</dd><dt id="uv-remove--no-build-package"><a href="#uv-remove--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-remove--no-cache"><a href="#uv-remove--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-remove--no-config"><a href="#uv-remove--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-remove--no-index"><a href="#uv-remove--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-remove--no-managed-python"><a href="#uv-remove--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-remove--no-progress"><a href="#uv-remove--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-remove--no-python-downloads"><a href="#uv-remove--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-remove--no-sources"><a href="#uv-remove--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-remove--no-sync"><a href="#uv-remove--no-sync"><code>--no-sync</code></a></dt><dd><p>在重新锁定项目后避免同步虚拟环境</p>
<p>也可以通过 <code>UV_NO_SYNC</code> 环境变量设置。</p></dd><dt id="uv-remove--offline"><a href="#uv-remove--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-remove--optional"><a href="#uv-remove--optional"><code>--optional</code></a> <i>optional</i></dt><dd><p>从项目的指定额外功能的可选依赖项中移除包</p>
</dd><dt id="uv-remove--package"><a href="#uv-remove--package"><code>--package</code></a> <i>package</i></dt><dd><p>从工作区中的特定包中移除依赖项</p>
</dd><dt id="uv-remove--prerelease"><a href="#uv-remove--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的限定符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-remove--project"><a href="#uv-remove--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-remove--python"><a href="#uv-remove--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于解析和同步的 Python 解释器。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-remove--quiet"><a href="#uv-remove--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-remove--refresh"><a href="#uv-remove--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存的数据</p>
</dd><dt id="uv-remove--refresh-package"><a href="#uv-remove--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-remove--reinstall"><a href="#uv-remove--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-remove--reinstall-package"><a href="#uv-remove--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-remove--resolution"><a href="#uv-remove--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-remove--script"><a href="#uv-remove--script"><code>--script</code></a> <i>script</i></dt><dd><p>从指定的 Python 脚本中移除依赖项，而不是从项目中移除。</p>
<p>如果提供，uv 将根据 PEP 723 从脚本的内联元数据表中移除依赖项。</p>
</dd><dt id="uv-remove--upgrade"><a href="#uv-remove--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-remove--upgrade-package"><a href="#uv-remove--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-remove--verbose"><a href="#uv-remove--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv version

读取或更新项目的版本

<h3 class="cli-reference">用法</h3>

```
uv version [OPTIONS] [VALUE]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-version--value"><a href="#uv-version--value"<code>VALUE</code></a></dt><dd><p>将项目版本设置为此值</p>
<p>要改用语义版本控制组件更新项目，请使用 <code>--bump</code>。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-version--active"><a href="#uv-version--active"><code>--active</code></a></dt><dd><p>优先使用活动的虚拟环境而非项目的虚拟环境。</p>
<p>如果项目虚拟环境已激活或没有虚拟环境处于活动状态，则此选项无效。</p>
</dd><dt id="uv-version--allow-insecure-host"><a href="#uv-version--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如，<code>localhost</code>）、主机-端口对（例如，<code>localhost:8080</code>）或 URL（例如，<code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证并可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-version--bump"><a href="#uv-version--bump"><code>--bump</code></a> <i>bump[=value]</i></dt><dd><p>使用给定的语义更新项目版本</p>
<p>此标志可以传递多次。</p>
<p>可能的值：</p>
<ul>
<li><code>major</code>:  增加主版本（例如，1.2.3 =&gt; 2.0.0）</li>
<li><code>minor</code>:  增加次版本（例如，1.2.3 =&gt; 1.3.0）</li>
<li><code>patch</code>:  增加修订版本（例如，1.2.3 =&gt; 1.2.4）</li>
<li><code>stable</code>:  从预发布版本移动到稳定版本（例如，1.2.3b4.post5.dev6 =&gt; 1.2.3）</li>
<li><code>alpha</code>:  增加 alpha 版本（例如，1.2.3a4 =&gt; 1.2.3a5）</li>
<li><code>beta</code>:  增加 beta 版本（例如，1.2.3b4 =&gt; 1.2.3b5）</li>
<li><code>rc</code>:  增加 rc 版本（例如，1.2.3rc4 =&gt; 1.2.3rc5）</li>
<li><code>post</code>:  增加 post 版本（例如，1.2.3.post5 =&gt; 1.2.3.post6）</li>
<li><code>dev</code>:  增加 dev 版本（例如，1.2.3a4.dev6 =&gt; 1.2.3.dev7）</li>
</ul></dd><dt id="uv-version--cache-dir"><a href="#uv-version--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-version--color"><a href="#uv-version--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-version--compile-bytecode"><a href="#uv-version--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在首次导入模块时惰性执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-version--config-file"><a href="#uv-version--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>要用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-version--config-setting"><a href="#uv-version--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-version--config-settings-package"><a href="#uv-version--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给 PEP 517 构建后端以用于特定包的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-version--default-index"><a href="#uv-version--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-version--directory"><a href="#uv-version--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-version--dry-run"><a href="#uv-version--dry-run"><code>--dry-run</code></a></dt><dd><p>不将新版本写入 <code>pyproject.toml</code></p>
<p>相反，将显示版本。</p>
</dd><dt id="uv-version--exclude-newer"><a href="#uv-version--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-version--exclude-newer-package"><a href="#uv-version--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-version--extra-index-url"><a href="#uv-version--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-version--find-links"><a href="#uv-version--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如，<code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-version--fork-strategy"><a href="#uv-version--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-version--frozen"><a href="#uv-version--frozen"><code>--frozen</code></a></dt><dd><p>更新版本而不重新锁定项目。</p>
<p>项目环境将不会同步。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-version--help"><a href="#uv-version--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-version--index"><a href="#uv-version--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-version--index-strategy"><a href="#uv-version--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用返回给定包名称匹配的第一个索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-version--index-url"><a href="#uv-version--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-version--keyring-provider"><a href="#uv-version--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-version--link-mode"><a href="#uv-version--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即，写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-version--locked"><a href="#uv-version--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求 lockfile 是最新的。如果 lockfile 缺失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-version--managed-python"><a href="#uv-version--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-version--native-tls"><a href="#uv-version--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-version--no-binary"><a href="#uv-version--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-version--no-binary-package"><a href="#uv-version--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-version--no-build"><a href="#uv-version--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-version--no-build-isolation"><a href="#uv-version--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-version--no-build-isolation-package"><a href="#uv-version--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包在 PEP 518 中指定的构建依赖项已安装。</p>
</dd><dt id="uv-version--no-build-package"><a href="#uv-version--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-version--no-cache"><a href="#uv-version--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-version--no-config"><a href="#uv-version--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-version--no-index"><a href="#uv-version--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-version--no-managed-python"><a href="#uv-version--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-version--no-progress"><a href="#uv-version--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-version--no-python-downloads"><a href="#uv-version--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-version--no-sources"><a href="#uv-version--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-version--no-sync"><a href="#uv-version--no-sync"><code>--no-sync</code></a></dt><dd><p>在重新锁定项目后避免同步虚拟环境</p>
<p>也可以通过 <code>UV_NO_SYNC</code> 环境变量设置。</p></dd><dt id="uv-version--offline"><a href="#uv-version--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-version--output-format"><a href="#uv-version--output-format"><code>--output-format</code></a> <i>output-format</i></dt><dd><p>输出的格式</p>
<p>[默认值：text]</p><p>可能的值：</p>
<ul>
<li><code>text</code>:  将版本显示为纯文本</li>
<li><code>json</code>:  将版本显示为 JSON</li>
</ul></dd><dt id="uv-version--package"><a href="#uv-version--package"><code>--package</code></a> <i>package</i></dt><dd><p>更新工作区中特定包的版本</p>
</dd><dt id="uv-version--prerelease"><a href="#uv-version--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的限定符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-version--project"><a href="#uv-version--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-version--python"><a href="#uv-version--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于解析和同步的 Python 解释器。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-version--quiet"><a href="#uv-version--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-version--refresh"><a href="#uv-version--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存的数据</p>
</dd><dt id="uv-version--refresh-package"><a href="#uv-version--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-version--reinstall"><a href="#uv-version--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-version--reinstall-package"><a href="#uv-version--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-version--resolution"><a href="#uv-version--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-version--short"><a href="#uv-version--short"><code>--short</code></a></dt><dd><p>仅显示版本</p>
<p>默认情况下，uv 将在版本之前显示项目名称。</p>
</dd><dt id="uv-version--upgrade"><a href="#uv-version--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-version--upgrade-package"><a href="#uv-version--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-version--verbose"><a href="#uv-version--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv sync

更新项目的环境。

同步确保所有项目依赖项都已安装并与 lockfile 保持同步。

默认情况下，执行精确同步：uv 会移除未声明为项目依赖项的包。使用 `--inexact` 标志可以保留多余的包。请注意，如果多余的包与项目依赖项冲突，它仍将被移除。此外，如果使用 `--no-build-isolation`，uv 将不会移除多余的包以避免移除可能的构建依赖项。

如果项目虚拟环境（`.venv`）不存在，它将被创建。

除非提供了 `--locked` 或 `--frozen` 标志，否则在同步之前会重新锁定项目。

uv 将在当前目录或任何父目录中搜索项目。如果找不到项目，uv 将退出并报错。

请注意，从 lockfile 安装时，uv 不会为已拉取的包版本提供警告。

<h3 class="cli-reference">用法</h3>

```
uv sync [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-sync--active"><a href="#uv-sync--active"><code>--active</code></a></dt><dd><p>将依赖项同步到活动的虚拟环境。</p>
<p>不是创建或更新项目或脚本的虚拟环境，而是优先使用活动的虚拟环境，如果设置了 <code>VIRTUAL_ENV</code> 环境变量。</p>
</dd><dt id="uv-sync--all-extras"><a href="#uv-sync--all-extras"><code>--all-extras</code></a></dt><dd><p>包含所有可选依赖项。</p>
<p>当两个或多个额外功能在 <code>tool.uv.conflicts</code> 中声明为冲突时，使用此标志将始终导致错误。</p>
<p>请注意，所有可选依赖项始终包含在解析中；此选项仅影响要安装的包的选择。</p>
</dd><dt id="uv-sync--all-groups"><a href="#uv-sync--all-groups"><code>--all-groups</code></a></dt><dd><p>包含所有依赖组中的依赖项。</p>
<p><code>--no-group</code> 可用于排除特定组。</p>
</dd><dt id="uv-sync--all-packages"><a href="#uv-sync--all-packages"><code>--all-packages</code></a></dt><dd><p>同步工作区中的所有包。</p>
<p>工作区的环境（<code>.venv</code>）被更新以包含所有工作区成员。</p>
<p>通过 <code>--extra</code>、<code>--group</code> 或相关选项指定的任何额外功能或组将应用于所有工作区成员。</p>
</dd><dt id="uv-sync--allow-insecure-host"><a href="#uv-sync--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如，<code>localhost</code>）、主机-端口对（例如，<code>localhost:8080</code>）或 URL（例如，<code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证并可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-sync--cache-dir"><a href="#uv-sync--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-sync--check"><a href="#uv-sync--check"><code>--check</code></a></dt><dd><p>检查 Python 环境是否与项目同步。</p>
<p>如果环境不是最新的，uv 将退出并报错。</p>
</dd><dt id="uv-sync--color"><a href="#uv-sync--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-sync--compile-bytecode"><a href="#uv-sync--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在首次导入模块时惰性执行。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-sync--config-file"><a href="#uv-sync--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>要用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-sync--config-setting"><a href="#uv-sync--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-sync--config-settings-package"><a href="#uv-sync--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给 PEP 517 构建后端以用于特定包的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-sync--default-index"><a href="#uv-sync--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-sync--directory"><a href="#uv-sync--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-sync--dry-run"><a href="#uv-sync--dry-run"><code>--dry-run</code></a></dt><dd><p>执行空运行，不写入 lockfile 或修改项目环境。</p>
<p>在空运行模式下，uv 将解析项目的依赖项并报告对 lockfile 和项目环境的更改结果，但不会修改两者。</p>
</dd><dt id="uv-sync--exclude-newer"><a href="#uv-sync--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-sync--exclude-newer-package"><a href="#uv-sync--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如，<code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如，<code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-sync--extra"><a href="#uv-sync--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>包含指定额外功能名称的可选依赖项。</p>
<p>可以多次提供。</p>
<p>当指定了在 <code>tool.uv.conflicts</code> 中出现的多个额外功能或组时，uv 将报告错误。</p>
<p>请注意，所有可选依赖项始终包含在解析中；此选项仅影响要安装的包的选择。</p>
</dd><dt id="uv-sync--extra-index-url"><a href="#uv-sync--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-sync--find-links"><a href="#uv-sync--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如，<code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-sync--fork-strategy"><a href="#uv-sync--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-sync--frozen"><a href="#uv-sync--frozen"><code>--frozen</code></a></dt><dd><p>同步而不更新 <code>uv.lock</code> 文件。</p>
<p>不是检查 lockfile 是否是最新的，而是使用 lockfile 中的版本作为事实来源。如果 lockfile 缺失，uv 将退出并报错。如果 <code>pyproject.toml</code> 包含尚未包含在 lockfile 中的依赖项更改，它们将不会出现在环境中。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-sync--group"><a href="#uv-sync--group"><code>--group</code></a> <i>group</i></dt><dd><p>包含指定依赖组中的依赖项。</p>
<p>当指定了在 <code>tool.uv.conflicts</code> 中出现的多个额外功能或组时，uv 将报告错误。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-sync--help"><a href="#uv-sync--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-sync--index"><a href="#uv-sync--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-sync--index-strategy"><a href="#uv-sync--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用返回给定包名称匹配的第一个索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-sync--index-url"><a href="#uv-sync--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-sync--inexact"><a href="#uv-sync--inexact"><code>--inexact</code></a>, <code>--no-exact</code></dt><dd><p>不移除环境中存在的多余包。</p>
<p>启用后，uv 将进行满足要求所需的最小更改。默认情况下，同步将从环境中移除任何多余的包</p>
</dd><dt id="uv-sync--keyring-provider"><a href="#uv-sync--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-sync--link-mode"><a href="#uv-sync--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即，写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-sync--locked"><a href="#uv-sync--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求 lockfile 是最新的。如果 lockfile 缺失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-sync--managed-python"><a href="#uv-sync--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-sync--native-tls"><a href="#uv-sync--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-sync--no-binary"><a href="#uv-sync--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-sync--no-binary-package"><a href="#uv-sync--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-sync--no-build"><a href="#uv-sync--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-sync--no-build-isolation"><a href="#uv-sync--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-sync--no-build-isolation-package"><a href="#uv-sync--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包在 PEP 518 中指定的构建依赖项已安装。</p>
</dd><dt id="uv-sync--no-build-package"><a href="#uv-sync--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-sync--no-cache"><a href="#uv-sync--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-sync--no-config"><a href="#uv-sync--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-sync--no-default-groups"><a href="#uv-sync--no-default-groups"><code>--no-default-groups</code></a></dt><dd><p>忽略默认依赖组。</p>
<p>uv 默认包含在 <code>tool.uv.default-groups</code> 中定义的组。此选项禁用该选项，但是，仍然可以使用 <code>--group</code> 包含特定组。</p>
<p>也可以通过 <code>UV_NO_DEFAULT_GROUPS</code> 环境变量设置。</p></dd><dt id="uv-sync--no-dev"><a href="#uv-sync--no-dev"><code>--no-dev</code></a></dt><dd><p>禁用开发依赖组。</p>
<p>此选项是 <code>--no-group dev</code> 的别名。请参阅 <code>--no-default-groups</code> 以禁用所有默认组。</p>
<p>也可以通过 <code>UV_NO_DEV</code> 环境变量设置。</p></dd><dt id="uv-sync--no-editable"><a href="#uv-sync--no-editable"><code>--no-editable</code></a></dt><dd><p>以不可编辑模式安装任何可编辑依赖项，包括项目和任何工作区成员</p>
<p>也可以通过 <code>UV_NO_EDITABLE</code> 环境变量设置。</p></dd><dt id="uv-sync--no-extra"><a href="#uv-sync--no-extra"><code>--no-extra</code></a> <i>no-extra</i></dt><dd><p>如果提供了 <code>--all-extras</code>，则排除指定的可选依赖项。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-sync--no-group"><a href="#uv-sync--no-group"><code>--no-group</code></a> <i>no-group</i></dt><dd><p>禁用指定的依赖组。</p>
<p>此选项始终优先于默认组、<code>--all-groups</code> 和 <code>--group</code>。</p>
<p>可以多次提供。</p>
<p>也可以通过 <code>UV_NO_GROUP</code> 环境变量设置。</p></dd><dt id="uv-sync--no-index"><a href="#uv-sync--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-sync--no-install-local"><a href="#uv-sync--no-install-local"><code>--no-install-local</code></a></dt><dd><p>不安装本地路径依赖项</p>
<p>跳过当前项目、工作区成员以及任何其他本地（路径或可编辑）包。仅安装远程/索引依赖项。在 Docker 构建中很有用，可以首先缓存繁重的第三方依赖项并单独分层本地包。</p>
<p>反向选项 <code>--only-install-local</code> 可用于<em>仅</em>安装本地包，排除所有远程依赖项。</p>
</dd><dt id="uv-sync--no-install-package"><a href="#uv-sync--no-install-package"><code>--no-install-package</code></a> <i>no-install-package</i></dt><dd><p>不安装给定的包。</p>
<p>默认情况下，项目的所有依赖项都安装到环境中。<code>--no-install-package</code> 选项允许排除特定包。请注意，这可能导致环境损坏，应谨慎使用。</p>
<p>反向选项 <code>--only-install-package</code> 可用于<em>仅</em>安装指定的包，排除所有其他包。</p>
</dd><dt id="uv-sync--no-install-project"><a href="#uv-sync--no-install-project"><code>--no-install-project</code></a></dt><dd><p>不安装当前项目。</p>
<p>默认情况下，当前项目及其所有依赖项都安装到环境中。<code>--no-install-project</code> 选项允许排除项目，但其所有依赖项仍会安装。这在诸如构建 Docker 镜像等情况下特别有用，其中将项目与其依赖项分开安装可以实现最佳层缓存。</p>
<p>反向选项 <code>--only-install-project</code> 可用于<em>仅</em>安装项目本身，排除所有依赖项。</p>
</dd><dt id="uv-sync--no-install-workspace"><a href="#uv-sync--no-install-workspace"><code>--no-install-workspace</code></a></dt><dd><p>不安装任何工作区成员，包括根项目。</p>
<p>默认情况下，所有工作区成员及其依赖项都安装到环境中。<code>--no-install-workspace</code> 选项允许排除所有工作区成员，同时保留它们的依赖项。这在诸如构建 Docker 镜像等情况下特别有用，其中将工作区与其依赖项分开安装可以实现最佳层缓存。</p>
<p>反向选项 <code>--only-install-workspace</code> 可用于<em>仅</em>安装工作区成员，排除所有其他依赖项。</p>
</dd><dt id="uv-sync--no-managed-python"><a href="#uv-sync--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-sync--no-progress"><a href="#uv-sync--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-sync--no-python-downloads"><a href="#uv-sync--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-sync--no-sources"><a href="#uv-sync--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-sync--offline"><a href="#uv-sync--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-sync--only-dev"><a href="#uv-sync--only-dev"><code>--only-dev</code></a></dt><dd><p>仅包含开发依赖组。</p>
<p>项目及其依赖项将被省略。</p>
<p>此选项是 <code>--only-group dev</code> 的别名。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-sync--only-group"><a href="#uv-sync--only-group"><code>--only-group</code></a> <i>only-group</i></dt><dd><p>仅包含指定依赖组中的依赖项。</p>
<p>项目及其依赖项将被省略。</p>
<p>可以多次提供。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-sync--output-format"><a href="#uv-sync--output-format"><code>--output-format</code></a> <i>output-format</i></dt><dd><p>选择输出格式</p>
<p>[默认值：text]</p><p>可能的值：</p>
<ul>
<li><code>text</code>:  以人类可读的格式显示结果</li>
<li><code>json</code>:  以 JSON 格式显示结果</li>
</ul></dd><dt id="uv-sync--package"><a href="#uv-sync--package"><code>--package</code></a> <i>package</i></dt><dd><p>为工作区中的特定包同步。</p>
<p>工作区的环境（<code>.venv</code>）被更新以反映指定工作区成员包声明的依赖项子集。</p>

<p>如果任何工作区成员不存在，uv 将退出并报错。</p>
</dd><dt id="uv-sync--prerelease"><a href="#uv-sync--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 会接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方要求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中包含显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中包含显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-sync--project"><a href="#uv-sync--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-sync--python"><a href="#uv-sync--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于项目环境的 Python 解释器。</p>
<p>默认情况下，使用第一个满足项目 <code>requires-python</code> 约束的解释器。</p>
<p>如果提供了虚拟环境中的 Python 解释器，包将不会同步到给定环境。该解释器将用于在项目中创建虚拟环境。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-sync--python-platform"><a href="#uv-sync--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装要求的平台。</p>
<p>表示为"目标三元组"，一个描述目标平台的字符串，包括其 CPU、供应商和操作系统名称，例如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标平台为 macOS (Darwin) 时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标平台为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标平台为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与<em>目标</em>平台兼容的 wheel；因此，安装的发行版可能与<em>当前</em>平台不兼容。相反，从源代码构建的任何发行版可能与<em>目标</em>平台不兼容，因为它们将为<em>当前</em>平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>:  <code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>:  <code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>:  <code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>:  64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>:  ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>:  32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>:  x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>:  基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>:  x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>:  ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>:  ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>:  <code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>:  RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>:  用于 <code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>:  用于 <code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>:  用于 <code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>:  用于 <code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>:  用于 <code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>:  用于 <code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>:  用于 <code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>:  用于 <code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>:  用于 <code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>:  用于 <code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>:  用于 <code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>:  用于 <code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>:  用于 <code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>:  用于 <code>manylinux2014</code> 平台的 ARM64 目标。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>:  用于 <code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>:  用于 <code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>:  用于 <code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>:  用于 <code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>:  用于 <code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>:  用于 <code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>:  用于 <code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>:  用于 <code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>:  用于 <code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>:  用于 <code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>:  用于 <code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>:  用于 <code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>:  ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>:  <code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>:  使用 Pyodide 2024 平台的 wasm32 目标。旨在与 Python 3.12 一起使用</li>
<li><code>arm64-apple-ios</code>:  用于 iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>:  用于 iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>:  用于 iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-sync--quiet"><a href="#uv-sync--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-sync--refresh"><a href="#uv-sync--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-sync--refresh-package"><a href="#uv-sync--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-sync--reinstall"><a href="#uv-sync--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。隐含 <code>--refresh</code></p>
</dd><dt id="uv-sync--reinstall-package"><a href="#uv-sync--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-sync--resolution"><a href="#uv-sync--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包要求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-sync--script"><a href="#uv-sync--script"><code>--script</code></a> <i>script</i></dt><dd><p>为 Python 脚本同步环境，而不是当前项目。</p>
<p>如果提供，uv 将根据脚本的内联元数据表同步依赖项，遵循 PEP 723。</p>
</dd><dt id="uv-sync--upgrade"><a href="#uv-sync--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh</code></p>
</dd><dt id="uv-sync--upgrade-package"><a href="#uv-sync--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-sync--verbose"><a href="#uv-sync--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv lock

更新项目的锁文件。

如果项目锁文件（`uv.lock`）不存在，将会创建它。如果锁文件存在，其内容将用作解析的首选项。

如果项目的依赖项没有更改，除非提供了 `--upgrade` 标志，否则锁定将无效。

<h3 class="cli-reference">用法</h3>

```
uv lock [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-lock--allow-insecure-host"><a href="#uv-lock--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-lock--cache-dir"><a href="#uv-lock--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-lock--check"><a href="#uv-lock--check"><code>--check</code></a></dt><dd><p>检查锁文件是否为最新。</p>
<p>断言解析后 <code>uv.lock</code> 将保持不变。如果锁文件丢失或需要更新，uv 将退出并报错。</p>
<p>等效于 <code>--locked</code>。</p>
</dd><dt id="uv-lock--check-exists"><a href="#uv-lock--check-exists"><code>--check-exists</code></a>, <code>--frozen</code></dt><dd><p>断言 <code>uv.lock</code> 存在而不检查它是否为最新。</p>
<p>等效于 <code>--frozen</code>。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-lock--color"><a href="#uv-lock--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-lock--config-file"><a href="#uv-lock--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-lock--config-setting"><a href="#uv-lock--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-lock--config-settings-package"><a href="#uv-lock--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-lock--default-index"><a href="#uv-lock--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-lock--directory"><a href="#uv-lock--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-lock--dry-run"><a href="#uv-lock--dry-run"><code>--dry-run</code></a></dt><dd><p>执行空运行，不写入锁文件。</p>
<p>在空运行模式下，uv 将解析项目的依赖项并报告结果更改，但不会将锁文件写入磁盘。</p>
</dd><dt id="uv-lock--exclude-newer"><a href="#uv-lock--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-lock--exclude-newer-package"><a href="#uv-lock--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-lock--extra-index-url"><a href="#uv-lock--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）除了 <code>--index-url</code> 之外要使用的额外包索引 URL。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-lock--find-links"><a href="#uv-lock--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了注册表索引中找到的候选发行版之外，还要搜索的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-lock--fork-strategy"><a href="#uv-lock--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少的版本数量。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-lock--help"><a href="#uv-lock--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-lock--index"><a href="#uv-lock--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-lock--index-strategy"><a href="#uv-lock--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移至下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果包版本在多个索引中，仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-lock--index-url"><a href="#uv-lock--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-lock--keyring-provider"><a href="#uv-lock--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-lock--link-mode"><a href="#uv-lock--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅在构建源发行版时使用。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-lock--managed-python"><a href="#uv-lock--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-lock--native-tls"><a href="#uv-lock--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-lock--no-binary"><a href="#uv-lock--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-lock--no-binary-package"><a href="#uv-lock--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-lock--no-build"><a href="#uv-lock--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源发行版的缓存 wheel，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-lock--no-build-isolation"><a href="#uv-lock--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-lock--no-build-isolation-package"><a href="#uv-lock--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-lock--no-build-package"><a href="#uv-lock--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-lock--no-cache"><a href="#uv-lock--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-lock--no-config"><a href="#uv-lock--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-lock--no-index"><a href="#uv-lock--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-lock--no-managed-python"><a href="#uv-lock--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-lock--no-progress"><a href="#uv-lock--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-lock--no-python-downloads"><a href="#uv-lock--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-lock--no-sources"><a href="#uv-lock--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-lock--offline"><a href="#uv-lock--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用时，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-lock--prerelease"><a href="#uv-lock--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 会接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方要求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中包含显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中包含显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-lock--project"><a href="#uv-lock--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-lock--python"><a href="#uv-lock--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>解析期间使用的 Python 解释器。</p>
<p>当没有 wheel 时，需要 Python 解释器来构建源发行版以确定包元数据。</p>
<p>如果未设置 <code>requires-python</code>，解释器也用作最小 Python 版本的备用值。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-lock--quiet"><a href="#uv-lock--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-lock--refresh"><a href="#uv-lock--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-lock--refresh-package"><a href="#uv-lock--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-lock--resolution"><a href="#uv-lock--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包要求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-lock--script"><a href="#uv-lock--script"><code>--script</code></a> <i>script</i></dt><dd><p>锁定指定的 Python 脚本，而不是当前项目。</p>
<p>如果提供，uv 将脚本（基于其内联元数据表，遵循 PEP 723）锁定到脚本本身旁边的 <code>.lock</code> 文件。</p>
</dd><dt id="uv-lock--upgrade"><a href="#uv-lock--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh</code></p>
</dd><dt id="uv-lock--upgrade-package"><a href="#uv-lock--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-lock--verbose"><a href="#uv-lock--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv export

将项目的锁文件导出为替代格式。

目前支持 `requirements.txt` 和 `pylock.toml`（PEP 751）格式。

除非提供 `--locked` 或 `--frozen` 标志，否则项目会在导出前重新锁定。

uv 将在当前目录或任何父目录中搜索项目。如果找不到项目，uv 将退出并报错。

如果在工作区中操作，默认情况下将导出根目录；但是，可以使用 `--package` 选项选择特定成员。

<h3 class="cli-reference">用法</h3>

```
uv export [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-export--all-extras"><a href="#uv-export--all-extras"><code>--all-extras</code></a></dt><dd><p>包含所有可选依赖项</p>
</dd><dt id="uv-export--all-groups"><a href="#uv-export--all-groups"><code>--all-groups</code></a></dt><dd><p>包含来自所有依赖组别的依赖项。</p>
<p><code>--no-group</code> 可用于排除特定组别。</p>
</dd><dt id="uv-export--all-packages"><a href="#uv-export--all-packages"><code>--all-packages</code></a></dt><dd><p>导出整个工作区。</p>
<p>所有工作区成员的依赖项将包含在导出的需求文件中。</p>
<p>通过 <code>--extra</code>、<code>--group</code> 或相关选项指定的任何额外项或组别将应用于所有工作区成员。</p>
</dd><dt id="uv-export--allow-insecure-host"><a href="#uv-export--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-export--cache-dir"><a href="#uv-export--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-export--color"><a href="#uv-export--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-export--config-file"><a href="#uv-export--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-export--config-setting"><a href="#uv-export--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-export--config-settings-package"><a href="#uv-export--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-export--default-index"><a href="#uv-export--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-export--directory"><a href="#uv-export--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>请参阅 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-export--exclude-newer"><a href="#uv-export--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-export--exclude-newer-package"><a href="#uv-export--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-export--extra"><a href="#uv-export--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>包含来自指定额外名称的可选依赖项。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-export--extra-index-url"><a href="#uv-export--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）除了 <code>--index-url</code> 之外要使用的额外包索引 URL。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-export--find-links"><a href="#uv-export--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了注册表索引中找到的候选发行版之外，还要搜索的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-export--fork-strategy"><a href="#uv-export--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少的版本数量。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-export--format"><a href="#uv-export--format"><code>--format</code></a> <i>format</i></dt><dd><p><code>uv.lock</code> 应导出到的格式。</p>
<p>支持 <code>requirements.txt</code> 和 <code>pylock.toml</code>（PEP 751）输出格式。</p>
<p>如果提供了输出文件，uv 将从输出文件的文件扩展名推断输出格式。否则，默认为 <code>requirements.txt</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>requirements.txt</code>:  以 <code>requirements.txt</code> 格式导出</li>
<li><code>pylock.toml</code>:  以 <code>pylock.toml</code> 格式导出</li>
</ul></dd><dt id="uv-export--frozen"><a href="#uv-export--frozen"><code>--frozen</code></a></dt><dd><p>在导出前不更新 <code>uv.lock</code>。</p>
<p>如果 <code>uv.lock</code> 不存在，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-export--group"><a href="#uv-export--group"><code>--group</code></a> <i>group</i></dt><dd><p>包含来自指定依赖组别的依赖项。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-export--help"><a href="#uv-export--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-export--index"><a href="#uv-export--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>不支持索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-export--index-strategy"><a href="#uv-export--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移至下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果包版本在多个索引中，仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-export--index-url"><a href="#uv-export--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或按相同格式布局的本地目录。</p>
<p>通过此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-export--keyring-provider"><a href="#uv-export--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-export--link-mode"><a href="#uv-export--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅在构建源发行版时使用。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-export--locked"><a href="#uv-export--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求锁文件是最新的。如果锁文件丢失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-export--managed-python"><a href="#uv-export--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-export--native-tls"><a href="#uv-export--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-export--no-annotate"><a href="#uv-export--no-annotate"><code>--no-annotate</code></a></dt><dd><p>排除指示每个包来源的注释</p>
</dd><dt id="uv-export--no-binary"><a href="#uv-export--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-export--no-binary-package"><a href="#uv-export--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-export--no-build"><a href="#uv-export--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源发行版的缓存 wheel，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-export--no-build-isolation"><a href="#uv-export--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-export--no-build-isolation-package"><a href="#uv-export--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-export--no-build-package"><a href="#uv-export--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-export--no-cache"><a href="#uv-export--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-export--no-config"><a href="#uv-export--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-export--no-default-groups"><a href="#uv-export--no-default-groups"><code>--no-default-groups</code></a></dt><dd><p>忽略默认依赖组别。</p>
<p>uv 默认包含 <code>tool.uv.default-groups</code> 中定义的组别。这会禁用该选项，但是，仍然可以使用 <code>--group</code> 包含特定组别。</p>
<p>也可以通过 <code>UV_NO_DEFAULT_GROUPS</code> 环境变量设置。</p></dd><dt id="uv-export--no-dev"><a href="#uv-export--no-dev"><code>--no-dev</code></a></dt><dd><p>禁用开发依赖组别。</p>
<p>此选项是 <code>--no-group dev</code> 的别名。请参阅 <code>--no-default-groups</code> 以禁用所有默认组别。</p>
<p>也可以通过 <code>UV_NO_DEV</code> 环境变量设置。</p></dd><dt id="uv-export--no-editable"><a href="#uv-export--no-editable"><code>--no-editable</code></a></dt><dd><p>将任何可编辑依赖项（包括项目和任何工作区成员）导出为不可编辑</p>
<p>也可以通过 <code>UV_NO_EDITABLE</code> 环境变量设置。</p></dd><dt id="uv-export--no-emit-local"><a href="#uv-export--no-emit-local"><code>--no-emit-local</code></a>, <code>--no-install-local</code></dt><dd><p>不要在导出的需求中包含本地路径依赖项。</p>
<p>从导出中省略当前项目、工作区成员和任何其他本地（路径或可编辑）包。仅写入远程/索引依赖项。对于希望首先导出和缓存第三方依赖项的 Docker 和 CI 流程很有用。</p>
<p>反向的 <code>--only-emit-local</code> 可用于仅发出本地包，排除所有远程依赖项。</p>
</dd><dt id="uv-export--no-emit-package"><a href="#uv-export--no-emit-package"><code>--no-emit-package</code></a>, <code>--no-install-package</code> <i>no-emit-package</i></dt><dd><p>不发出给定的包。</p>
<p>默认情况下，所有项目的依赖项都包含在导出的需求文件中。<code>--no-emit-package</code> 选项允许排除特定包。</p>
<p>反向的 <code>--only-emit-package</code> 可用于仅发出指定的包，排除所有其他包。</p>
</dd><dt id="uv-export--no-emit-project"><a href="#uv-export--no-emit-project"><code>--no-emit-project</code></a>, <code>--no-install-project</code></dt><dd><p>不发出当前项目。</p>
<p>默认情况下，当前项目及其所有依赖项包含在导出的需求文件中。<code>--no-emit-project</code> 选项允许排除项目，但保留其所有依赖项。</p>
<p>反向的 <code>--only-emit-project</code> 可用于仅发出项目本身，排除所有依赖项。</p>
</dd><dt id="uv-export--no-emit-workspace"><a href="#uv-export--no-emit-workspace"><code>--no-emit-workspace</code></a>, <code>--no-install-workspace</code></dt><dd><p>不发出任何工作区成员，包括根项目。</p>
<p>默认情况下，所有工作区成员及其依赖项都包含在导出的需求文件中，包括它们的所有依赖项。<code>--no-emit-workspace</code> 选项允许排除所有工作区成员，同时保留它们的依赖项。</p>
<p>反向的 <code>--only-emit-workspace</code> 可用于仅发出工作区成员，排除所有其他依赖项。</p>
</dd><dt id="uv-export--no-extra"><a href="#uv-export--no-extra"><code>--no-extra</code></a> <i>no-extra</i></dt><dd><p>如果提供了 <code>--all-extras</code>，则排除指定的可选依赖项。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-export--no-group"><a href="#uv-export--no-group"><code>--no-group</code></a> <i>no-group</i></dt><dd><p>禁用指定的依赖组别。</p>
<p>此选项始终优先于默认组别、<code>--all-groups</code> 和 <code>--group</code>。</p>
<p>可以多次提供。</p>
<p>也可以通过 <code>UV_NO_GROUP</code> 环境变量设置。</p></dd><dt id="uv-export--no-hashes"><a href="#uv-export--no-hashes"><code>--no-hashes</code></a></dt><dd><p>在生成的输出中省略哈希值</p>
</dd><dt id="uv-export--no-header"><a href="#uv-export--no-header"><code>--no-header</code></a></dt><dd><p>排除生成输出文件顶部的注释头</p>
</dd><dt id="uv-export--no-index"><a href="#uv-export--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-export--no-managed-python"><a href="#uv-export--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-export--no-progress"><a href="#uv-export--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-export--no-python-downloads"><a href="#uv-export--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-export--no-sources"><a href="#uv-export--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-export--offline"><a href="#uv-export--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用时，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-export--only-dev"><a href="#uv-export--only-dev"><code>--only-dev</code></a></dt><dd><p>仅包含开发依赖组别。</p>
<p>项目及其依赖项将被省略。</p>
<p>此选项是 <code>--only-group dev</code> 的别名。隐含 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-export--only-group"><a href="#uv-export--only-group"><code>--only-group</code></a> <i>only-group</i></dt><dd><p>仅包含来自指定依赖组别的依赖项。</p>
<p>项目及其依赖项将被省略。</p>
<p>可以多次提供。隐含 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-export--output-file"><a href="#uv-export--output-file"><code>--output-file</code></a>, <code>-o</code> <i>output-file</i></dt><dd><p>将导出的需求写入给定文件</p>
</dd><dt id="uv-export--package"><a href="#uv-export--package"><code>--package</code></a> <i>package</i></dt><dd><p>导出工作区中特定包的依赖项。</p>
<p>如果任何工作区成员不存在，uv 将退出并报错。</p>
</dd><dt id="uv-export--prerelease"><a href="#uv-export--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 会接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方要求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中包含显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中包含显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-export--project"><a href="#uv-export--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-export--prune"><a href="#uv-export--prune"><code>--prune</code></a> <i>package</i></dt><dd><p>从依赖树中修剪给定的包。</p>
<p>修剪的包将从导出的需求文件中排除，修剪包移除后不再需要的任何依赖项也将被排除。</p>
</dd><dt id="uv-export--python"><a href="#uv-export--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>解析期间使用的 Python 解释器。</p>
<p>当没有 wheel 时，需要 Python 解释器来构建源发行版以确定包元数据。</p>
<p>如果未设置 <code>requires-python</code>，解释器也用作最小 Python 版本的备用值。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-export--quiet"><a href="#uv-export--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-export--refresh"><a href="#uv-export--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-export--refresh-package"><a href="#uv-export--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-export--resolution"><a href="#uv-export--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包要求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-export--script"><a href="#uv-export--script"><code>--script</code></a> <i>script</i></dt><dd><p>导出指定 PEP 723 Python 脚本的依赖项，而不是当前项目。</p>
<p>如果提供，uv 将根据其内联元数据表解析依赖项，遵循 PEP 723。</p>
</dd><dt id="uv-export--upgrade"><a href="#uv-export--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh</code></p>
</dd><dt id="uv-export--upgrade-package"><a href="#uv-export--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-export--verbose"><a href="#uv-export--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv tree

显示项目的依赖树

<h3 class="cli-reference">用法</h3>

```
uv tree [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tree--all-groups"><a href="#uv-tree--all-groups"><code>--all-groups</code></a></dt><dd><p>包含所有依赖组的依赖项。</p>
<p>可以使用 <code>--no-group</code> 来排除特定组。</p>
</dd><dt id="uv-tree--allow-insecure-host"><a href="#uv-tree--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tree--cache-dir"><a href="#uv-tree--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tree--color"><a href="#uv-tree--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-tree--config-file"><a href="#uv-tree--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tree--config-setting"><a href="#uv-tree--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-tree--config-settings-package"><a href="#uv-tree--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-tree--default-index"><a href="#uv-tree--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tree--depth"><a href="#uv-tree--depth"><code>--depth</code></a>, <code>-d</code> <i>depth</i></dt><dd><p>依赖树的最大显示深度</p>
<p>[默认值：255]</p></dd><dt id="uv-tree--directory"><a href="#uv-tree--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基准进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tree--exclude-newer"><a href="#uv-tree--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-tree--exclude-newer-package"><a href="#uv-tree--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-tree--extra-index-url"><a href="#uv-tree--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tree--find-links"><a href="#uv-tree--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-tree--fork-strategy"><a href="#uv-tree--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>：优化为每个包选择最少数量的版本。如果旧版本与更广泛支持的 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>：优化为每个支持的 Python 版本选择每个包的最新支持版本</li>
</ul></dd><dt id="uv-tree--frozen"><a href="#uv-tree--frozen"><code>--frozen</code></a></dt><dd><p>显示需求而不锁定项目。</p>
<p>如果锁定文件缺失，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_FROZEN</code> 环境变量设置。</p></dd><dt id="uv-tree--group"><a href="#uv-tree--group"><code>--group</code></a> <i>group</i></dt><dd><p>包含指定依赖组的依赖项。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-tree--help"><a href="#uv-tree--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-tree--index"><a href="#uv-tree--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tree--index-strategy"><a href="#uv-tree--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名匹配结果的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-tree--index-url"><a href="#uv-tree--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tree--invert"><a href="#uv-tree--invert"><code>--invert</code></a>, <code>--reverse</code></dt><dd><p>显示给定包的反向依赖项。此标志将反转树并显示依赖于给定包的包</p>
</dd><dt id="uv-tree--keyring-provider"><a href="#uv-tree--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-tree--link-mode"><a href="#uv-tree--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅在构建源发行版时使用。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-tree--locked"><a href="#uv-tree--locked"><code>--locked</code></a></dt><dd><p>断言 <code>uv.lock</code> 将保持不变。</p>
<p>要求锁定文件是最新的。如果锁定文件缺失或需要更新，uv 将退出并报错。</p>
<p>也可以通过 <code>UV_LOCKED</code> 环境变量设置。</p></dd><dt id="uv-tree--managed-python"><a href="#uv-tree--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tree--native-tls"><a href="#uv-tree--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本机证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本机证书存储，特别是如果您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tree--no-binary"><a href="#uv-tree--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-tree--no-binary-package"><a href="#uv-tree--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tree--no-build"><a href="#uv-tree--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-tree--no-build-isolation"><a href="#uv-tree--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-tree--no-build-isolation-package"><a href="#uv-tree--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包的 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-tree--no-build-package"><a href="#uv-tree--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tree--no-cache"><a href="#uv-tree--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tree--no-config"><a href="#uv-tree--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tree--no-dedupe"><a href="#uv-tree--no-dedupe"><code>--no-dedupe</code></a></dt><dd><p>不对重复的依赖项进行去重。通常，当一个包已经显示其依赖项时，后续出现不会重新显示其依赖项，并包含一个 (*) 表示它已经显示过。此标志将导致这些重复项被重复显示</p>
</dd><dt id="uv-tree--no-default-groups"><a href="#uv-tree--no-default-groups"><code>--no-default-groups</code></a></dt><dd><p>忽略默认依赖组。</p>
<p>uv 默认包含在 <code>tool.uv.default-groups</code> 中定义的组。此选项禁用该行为，但是，仍然可以使用 <code>--group</code> 包含特定组。</p>
<p>也可以通过 <code>UV_NO_DEFAULT_GROUPS</code> 环境变量设置。</p></dd><dt id="uv-tree--no-dev"><a href="#uv-tree--no-dev"><code>--no-dev</code></a></dt><dd><p>禁用开发依赖组。</p>
<p>此选项是 <code>--no-group dev</code> 的别名。请参阅 <code>--no-default-groups</code> 以禁用所有默认组。</p>
<p>也可以通过 <code>UV_NO_DEV</code> 环境变量设置。</p></dd><dt id="uv-tree--no-group"><a href="#uv-tree--no-group"><code>--no-group</code></a> <i>no-group</i></dt><dd><p>禁用指定的依赖组。</p>
<p>此选项始终优先于默认组、<code>--all-groups</code> 和 <code>--group</code>。</p>
<p>可以多次提供。</p>
<p>也可以通过 <code>UV_NO_GROUP</code> 环境变量设置。</p></dd><dt id="uv-tree--no-index"><a href="#uv-tree--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-tree--no-managed-python"><a href="#uv-tree--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tree--no-progress"><a href="#uv-tree--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tree--no-python-downloads"><a href="#uv-tree--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tree--no-sources"><a href="#uv-tree--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-tree--offline"><a href="#uv-tree--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tree--only-dev"><a href="#uv-tree--only-dev"><code>--only-dev</code></a></dt><dd><p>仅包含开发依赖组。</p>
<p>项目及其依赖项将被省略。</p>
<p>此选项是 <code>--only-group dev</code> 的别名。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-tree--only-group"><a href="#uv-tree--only-group"><code>--only-group</code></a> <i>only-group</i></dt><dd><p>仅包含指定依赖组的依赖项。</p>
<p>项目及其依赖项将被省略。</p>
<p>可以多次提供。意味着 <code>--no-default-groups</code>。</p>
</dd><dt id="uv-tree--outdated"><a href="#uv-tree--outdated"><code>--outdated</code></a></dt><dd><p>显示树中每个包的最新可用版本</p>
</dd><dt id="uv-tree--package"><a href="#uv-tree--package"><code>--package</code></a> <i>package</i></dt><dd><p>仅显示指定的包</p>
</dd><dt id="uv-tree--prerelease"><a href="#uv-tree--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>：不允许所有预发布版本</li>
<li><code>allow</code>：允许所有预发布版本</li>
<li><code>if-necessary</code>：如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>：允许在其版本要求中具有显式预发布标记的第一方包的预发布版本</li>
<li><code>if-necessary-or-explicit</code>：如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-tree--project"><a href="#uv-tree--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tree--prune"><a href="#uv-tree--prune"><code>--prune</code></a> <i>prune</i></dt><dd><p>从依赖树的显示中修剪给定的包</p>
</dd><dt id="uv-tree--python"><a href="#uv-tree--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于锁定和过滤的 Python 解释器。</p>
<p>默认情况下，树被过滤以匹配 Python 解释器报告的平台。使用 <code>--universal</code> 显示所有平台的树，或使用 <code>--python-version</code> 或 <code>--python-platform</code> 来覆盖标记的子集。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tree--python-platform"><a href="#uv-tree--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>过滤树时使用的平台。</p>
<p>例如，传递 <code>--platform windows</code> 以显示在 Windows 上安装时将包含的依赖项。</p>
<p>表示为"目标三元组"，一个描述目标平台的 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>：<code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>：<code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>：<code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>：64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>：ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>：32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>：x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>：基于 ARM 的 macOS 目标，如 Apple Silicon 设备上所见</li>
<li><code>x86_64-apple-darwin</code>：x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>：ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>：ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>：<code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>：RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>：<code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>：<code>manylinux2014</code> 平台的 ARM64 目标。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>：ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>：<code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>：使用 Pyodide 2024 平台的 wasm32 目标。用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>：iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>：iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>：iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-tree--python-version"><a href="#uv-tree--python-version"><code>--python-version</code></a> <i>python-version</i></dt><dd><p>过滤树时使用的 Python 版本。</p>
<p>例如，传递 <code>--python-version 3.10</code> 以显示在 Python 3.10 上安装时将包含的依赖项。</p>
<p>默认为发现的 Python 解释器的版本。</p>
</dd><dt id="uv-tree--quiet"><a href="#uv-tree--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tree--resolution"><a href="#uv-tree--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>：解析每个包的最高兼容版本</li>
<li><code>lowest</code>：解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>：解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-tree--script"><a href="#uv-tree--script"><code>--script</code></a> <i>script</i></dt><dd><p>显示指定的 PEP 723 Python 脚本的依赖树，而不是当前项目的依赖树。</p>
<p>如果提供，uv 将根据其内联元数据表解析依赖项，遵循 PEP 723。</p>
</dd><dt id="uv-tree--show-sizes"><a href="#uv-tree--show-sizes"><code>--show-sizes</code></a></dt><dd><p>显示树中包的压缩 wheel 大小</p>
</dd><dt id="uv-tree--universal"><a href="#uv-tree--universal"><code>--universal</code></a></dt><dd><p>显示与平台无关的依赖树。</p>
<p>显示所有 Python 版本和平台的已解析包版本，而不是过滤到与当前环境相关的版本。</p>
<p>每个包可能显示多个版本。</p>
</dd><dt id="uv-tree--upgrade"><a href="#uv-tree--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-tree--upgrade-package"><a href="#uv-tree--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包的升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-tree--verbose"><a href="#uv-tree--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv format

格式化项目中的 Python 代码。

使用 Ruff 格式化程序格式化 Python 代码。默认情况下，项目中的所有 Python 文件都会被格式化。此命令的行为与在项目根目录中运行 `ruff format` 相同。

要检查文件是否已格式化而不修改它们，请使用 `--check`。要查看格式化更改的差异，请使用 `--diff`。

其他参数可以在 `--` 之后传递给 Ruff。

<h3 class="cli-reference">用法</h3>

```
uv format [OPTIONS] [-- <EXTRA_ARGS>...]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-format--extra_args"><a href="#uv-format--extra_args"<code>EXTRA_ARGS</code></a></dt><dd><p>要传递给 Ruff 的附加参数。</p>
<p>例如，使用 <code>uv format -- --line-length 100</code> 设置行长度，或使用 <code>uv format -- src/module/foo.py</code> 格式化特定文件。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-format--allow-insecure-host"><a href="#uv-format--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-format--cache-dir"><a href="#uv-format--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-format--check"><a href="#uv-format--check"><code>--check</code></a></dt><dd><p>检查文件是否已格式化而不应用更改</p>
</dd><dt id="uv-format--color"><a href="#uv-format--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-format--config-file"><a href="#uv-format--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-format--diff"><a href="#uv-format--diff"><code>--diff</code></a></dt><dd><p>显示格式化更改的差异而不应用它们。</p>
<p>意味着 <code>--check</code>。</p>
</dd><dt id="uv-format--directory"><a href="#uv-format--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基准进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-format--help"><a href="#uv-format--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-format--managed-python"><a href="#uv-format--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-format--native-tls"><a href="#uv-format--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本机证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本机证书存储，特别是如果您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-format--no-cache"><a href="#uv-format--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-format--no-config"><a href="#uv-format--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-format--no-managed-python"><a href="#uv-format--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-format--no-progress"><a href="#uv-format--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-format--no-project"><a href="#uv-format--no-project"><code>--no-project</code></a></dt><dd><p>避免发现项目或工作区。</p>
<p>不是在当前项目的上下文中运行格式化程序，而是在当前目录的上下文中运行它。当当前目录不是项目时，这很有用。</p>
</dd><dt id="uv-format--no-python-downloads"><a href="#uv-format--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-format--offline"><a href="#uv-format--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-format--project"><a href="#uv-format--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-format--quiet"><a href="#uv-format--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-format--verbose"><a href="#uv-format--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-format--version"><a href="#uv-format--version"><code>--version</code></a> <i>version</i></dt><dd><p>用于格式化的 Ruff 版本。</p>
<p>默认情况下，将使用 uv 固定的 Ruff 版本。</p>
</dd></dl>

## uv tool

运行和安装 Python 包提供的命令

<h3 class="cli-reference">用法</h3>

```
uv tool [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-tool-run"><code>uv tool run</code></a></dt><dd><p>运行 Python 包提供的命令</p></dd>
<dt><a href="#uv-tool-install"><code>uv tool install</code></a></dt><dd><p>安装 Python 包提供的命令</p></dd>
<dt><a href="#uv-tool-upgrade"><code>uv tool upgrade</code></a></dt><dd><p>升级已安装的工具</p></dd>
<dt><a href="#uv-tool-list"><code>uv tool list</code></a></dt><dd><p>列出已安装的工具</p></dd>
<dt><a href="#uv-tool-uninstall"><code>uv tool uninstall</code></a></dt><dd><p>卸载工具</p></dd>
<dt><a href="#uv-tool-update-shell"><code>uv tool update-shell</code></a></dt><dd><p>确保工具可执行目录在 <code>PATH</code> 上</p></dd>
<dt><a href="#uv-tool-dir"><code>uv tool dir</code></a></dt><dd><p>显示 uv 工具目录的路径</p></dd>
</dl>

### uv tool run

运行 Python 包提供的命令。

默认情况下，要安装的包假定与命令名称匹配。

命令名称可以包含精确版本，格式为 `<package>@<version>`，例如 `uv tool run ruff@0.3.0`。如果需要更复杂的版本规范，或者命令由不同的包提供，请使用 `--from`。

`uvx` 可用于调用 Python，例如使用 `uvx python` 或 `uvx python@<version>`。将在隔离的虚拟环境中启动 Python 解释器。

如果工具之前已安装，即通过 `uv tool install` 安装，则将使用已安装的版本，除非请求了版本或使用了 `--isolated` 标志。

`uvx` 是 `uv tool run` 的便捷别名，它们的行为是相同的。

如果未提供命令，则显示已安装的工具。

包被安装到 uv 缓存目录中的临时虚拟环境中。

<h3 class="cli-reference">用法</h3>

```
uv tool run [OPTIONS] [COMMAND]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-run--allow-insecure-host"><a href="#uv-tool-run--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-run--build-constraints"><a href="#uv-tool-run--build-constraints"><code>--build-constraints</code></a>, <code>--build-constraint</code>, <code>-b</code> <i>build-constraints</i></dt><dd><p>在构建源发行版时，使用给定的需求文件约束构建依赖项。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的需求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>也可以通过 <code>UV_BUILD_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-tool-run--cache-dir"><a href="#uv-tool-run--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-run--color"><a href="#uv-tool-run--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-tool-run--compile-bytecode"><a href="#uv-tool-run--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；而是在首次导入模块时延迟执行编译。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 一样，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--config-file"><a href="#uv-tool-run--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--config-setting"><a href="#uv-tool-run--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-run--config-settings-package"><a href="#uv-tool-run--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-run--constraints"><a href="#uv-tool-run--constraints"><code>--constraints</code></a>, <code>--constraint</code>, <code>-c</code> <i>constraints</i></dt><dd><p>使用给定的需求文件约束版本。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的需求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>这等效于 pip 的 <code>--constraint</code> 选项。</p>
<p>也可以通过 <code>UV_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-tool-run--default-index"><a href="#uv-tool-run--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-run--directory"><a href="#uv-tool-run--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基准进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-run--env-file"><a href="#uv-tool-run--env-file"><code>--env-file</code></a> <i>env-file</i></dt><dd><p>从 <code>.env</code> 文件加载环境变量。</p>
<p>可以多次提供，后续文件中定义的值将覆盖先前文件中的值。</p>
<p>也可以通过 <code>UV_ENV_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--exclude-newer"><a href="#uv-tool-run--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-tool-run--exclude-newer-package"><a href="#uv-tool-run--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-tool-run--extra-index-url"><a href="#uv-tool-run--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-run--find-links"><a href="#uv-tool-run--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-tool-run--fork-strategy"><a href="#uv-tool-run--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>：优化为每个包选择最少数量的版本。如果旧版本与更广泛支持的 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>：优化为每个支持的 Python 版本选择每个包的最新支持版本</li>
</ul></dd><dt id="uv-tool-run--from"><a href="#uv-tool-run--from"><code>--from</code></a> <i>from</i></dt><dd><p>使用给定的包来提供命令。</p>
<p>默认情况下，包名假定与命令名匹配。</p>
</dd><dt id="uv-tool-run--help"><a href="#uv-tool-run--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-tool-run--index"><a href="#uv-tool-run--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-run--index-strategy"><a href="#uv-tool-run--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名匹配结果的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-tool-run--index-url"><a href="#uv-tool-run--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-run--isolated"><a href="#uv-tool-run--isolated"><code>--isolated</code></a></dt><dd><p>在隔离的虚拟环境中运行工具，忽略任何已安装的工具</p>
<p>也可以通过 <code>UV_ISOLATED</code> 环境变量设置。</p></dd><dt id="uv-tool-run--keyring-provider"><a href="#uv-tool-run--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-tool-run--link-mode"><a href="#uv-tool-run--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-tool-run--managed-python"><a href="#uv-tool-run--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-run--native-tls"><a href="#uv-tool-run--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本机证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本机证书存储，特别是如果您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-binary"><a href="#uv-tool-run--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-binary-package"><a href="#uv-tool-run--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-build"><a href="#uv-tool-run--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-build-isolation"><a href="#uv-tool-run--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-build-isolation-package"><a href="#uv-tool-run--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包的 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-tool-run--no-build-package"><a href="#uv-tool-run--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-cache"><a href="#uv-tool-run--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-config"><a href="#uv-tool-run--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-env-file"><a href="#uv-tool-run--no-env-file"><code>--no-env-file</code></a></dt><dd><p>避免从 <code>.env</code> 文件读取环境变量</p>
<p>也可以通过 <code>UV_NO_ENV_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-index"><a href="#uv-tool-run--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-tool-run--no-managed-python"><a href="#uv-tool-run--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-progress"><a href="#uv-tool-run--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-run--no-python-downloads"><a href="#uv-tool-run--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-run--no-sources"><a href="#uv-tool-run--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-tool-run--offline"><a href="#uv-tool-run--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--overrides"><a href="#uv-tool-run--overrides"><code>--overrides</code></a>, <code>--override</code> <i>overrides</i></dt><dd><p>使用给定的需求文件覆盖版本。</p>
<p>覆盖文件是类似 <code>requirements.txt</code> 的文件，强制安装特定版本的需求，无论任何组成包声明的需求如何，也无论这是否被视为无效解析。</p>
<p>约束是<em>附加的</em>，因为它们与组成包的需求相结合，而覆盖是<em>绝对的</em>，因为它们完全替换组成包的需求。</p>
<p>也可以通过 <code>UV_OVERRIDE</code> 环境变量设置。</p></dd><dt id="uv-tool-run--prerelease"><a href="#uv-tool-run--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>：不允许所有预发布版本</li>
<li><code>allow</code>：允许所有预发布版本</li>
<li><code>if-necessary</code>：如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>：允许在其版本要求中具有显式预发布标记的第一方包的预发布版本</li>
<li><code>if-necessary-or-explicit</code>：如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-tool-run--project"><a href="#uv-tool-run--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-run--python"><a href="#uv-tool-run--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于构建运行环境的 Python 解释器。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-run--python-platform"><a href="#uv-tool-run--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装需求的平台。</p>
<p>表示为"目标三元组"，一个描述目标平台的 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标为 macOS（Darwin）时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与<em>目标</em>平台兼容的 wheel；因此，安装的发行版可能与<em>当前</em>平台不兼容。相反，任何从源代码构建的发行版可能与<em>目标</em>平台不兼容，因为它们将为<em>当前</em>平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>：<code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>：<code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>：<code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>：64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>：ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>：32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>：x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>：基于 ARM 的 macOS 目标，如 Apple Silicon 设备上所见</li>
<li><code>x86_64-apple-darwin</code>：x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>：ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>：ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>：<code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>：RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>：<code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>：<code>manylinux2014</code> 平台的 ARM64 目标。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>：ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>：<code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>：使用 Pyodide 2024 平台的 wasm32 目标。用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>：iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>：iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>：iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-tool-run--quiet"><a href="#uv-tool-run--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-run--refresh"><a href="#uv-tool-run--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-tool-run--refresh-package"><a href="#uv-tool-run--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-tool-run--reinstall"><a href="#uv-tool-run--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-tool-run--reinstall-package"><a href="#uv-tool-run--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-tool-run--resolution"><a href="#uv-tool-run--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>：解析每个包的最高兼容版本</li>
<li><code>lowest</code>：解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>：解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-tool-run--upgrade"><a href="#uv-tool-run--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-tool-run--upgrade-package"><a href="#uv-tool-run--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包的升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-tool-run--verbose"><a href="#uv-tool-run--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-tool-run--with"><a href="#uv-tool-run--with"><code>--with</code></a>, <code>-w</code> <i>with</i></dt><dd><p>运行并安装以下附加需求</p>
</dd><dt id="uv-tool-run--with-editable"><a href="#uv-tool-run--with-editable"><code>--with-editable</code></a> <i>with-editable</i></dt><dd><p>以可编辑模式运行并安装给定的包</p>
<p>在项目中使用时，这些依赖项将在一个单独的临时环境中分层在 uv 工具环境之上。允许这些依赖项与指定的依赖项冲突。</p>
</dd><dt id="uv-tool-run--with-requirements"><a href="#uv-tool-run--with-requirements"><code>--with-requirements</code></a> <i>with-requirements</i></dt><dd><p>运行并安装给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、具有内联元数据的 <code>.py</code> 文件和 <code>pylock.toml</code>。</p>
</dd></dl>

### uv tool install

安装 Python 包提供的命令。

包被安装到 uv 工具目录中的隔离虚拟环境中。可执行文件被链接到工具可执行目录，该目录根据 XDG 标准确定，可以通过 `uv tool dir --bin` 检索。

如果工具之前已安装，则现有工具通常将被替换。

<h3 class="cli-reference">用法</h3>

```
uv tool install [OPTIONS] <PACKAGE>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-tool-install--package"><a href="#uv-tool-install--package"<code>PACKAGE</code></a></dt><dd><p>要从中安装命令的包</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-install--allow-insecure-host"><a href="#uv-tool-install--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-install--build-constraints"><a href="#uv-tool-install--build-constraints"><code>--build-constraints</code></a>, <code>--build-constraint</code>, <code>-b</code> <i>build-constraints</i></dt><dd><p>在构建源发行版时，使用给定的需求文件约束构建依赖项。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的需求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>也可以通过 <code>UV_BUILD_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-tool-install--cache-dir"><a href="#uv-tool-install--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-install--color"><a href="#uv-tool-install--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-tool-install--compile-bytecode"><a href="#uv-tool-install--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；而是在首次导入模块时延迟执行编译。对于启动时间至关重要的用例，例如 CLI 应用程序和 Docker 容器，可以启用此选项以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括未被当前操作修改的包）以确保一致性。与 pip 一样，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--config-file"><a href="#uv-tool-install--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--config-setting"><a href="#uv-tool-install--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>要传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-install--config-settings-package"><a href="#uv-tool-install--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>要传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-install--constraints"><a href="#uv-tool-install--constraints"><code>--constraints</code></a>, <code>--constraint</code>, <code>-c</code> <i>constraints</i></dt><dd><p>使用给定的需求文件约束版本。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的需求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>这等效于 pip 的 <code>--constraint</code> 选项。</p>
<p>也可以通过 <code>UV_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-tool-install--default-index"><a href="#uv-tool-install--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-install--directory"><a href="#uv-tool-install--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基准进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-install--editable"><a href="#uv-tool-install--editable"><code>--editable</code></a>, <code>-e</code></dt><dd><p>以可编辑模式安装目标包，这样包源目录中的更改无需重新安装即可反映出来</p>
</dd><dt id="uv-tool-install--exclude-newer"><a href="#uv-tool-install--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-tool-install--exclude-newer-package"><a href="#uv-tool-install--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-tool-install--excludes"><a href="#uv-tool-install--excludes"><code>--excludes</code></a>, <code>--exclude</code> <i>excludes</i></dt><dd><p>使用给定的需求文件从解析中排除包。</p>
<p>排除文件是类似 <code>requirements.txt</code> 的文件，指定要从解析中排除的包。当包被排除时，它将完全从依赖列表中省略，并且其自身的依赖项在解析阶段将被忽略。排除是无条件的，因为需求说明符和标记被忽略；提供的文件中列出的任何包将从所有解析的环境中省略。</p>
<p>也可以通过 <code>UV_EXCLUDE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--extra-index-url"><a href="#uv-tool-install--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值优先级更高。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-install--find-links"><a href="#uv-tool-install--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-tool-install--force"><a href="#uv-tool-install--force"><code>--force</code></a></dt><dd><p>强制安装工具。</p>
<p>将替换可执行目录中具有相同名称的任何现有入口点。</p>
</dd><dt id="uv-tool-install--fork-strategy"><a href="#uv-tool-install--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>：优化为每个包选择最少数量的版本。如果旧版本与更广泛支持的 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>：优化为每个支持的 Python 版本选择每个包的最新支持版本</li>
</ul></dd><dt id="uv-tool-install--help"><a href="#uv-tool-install--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-tool-install--index"><a href="#uv-tool-install--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值优先级更高。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-install--index-strategy"><a href="#uv-tool-install--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名匹配结果的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-tool-install--index-url"><a href="#uv-tool-install--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-install--keyring-provider"><a href="#uv-tool-install--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-tool-install--link-mode"><a href="#uv-tool-install--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-tool-install--managed-python"><a href="#uv-tool-install--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-install--native-tls"><a href="#uv-tool-install--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本机证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本机证书存储，特别是如果您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-binary"><a href="#uv-tool-install--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-binary-package"><a href="#uv-tool-install--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-build"><a href="#uv-tool-install--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。已构建的源发行版的缓存 wheel 将被重用，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-build-isolation"><a href="#uv-tool-install--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-build-isolation-package"><a href="#uv-tool-install--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包的 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-tool-install--no-build-package"><a href="#uv-tool-install--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不要为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-cache"><a href="#uv-tool-install--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-config"><a href="#uv-tool-install--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-index"><a href="#uv-tool-install--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-tool-install--no-managed-python"><a href="#uv-tool-install--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-progress"><a href="#uv-tool-install--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-install--no-python-downloads"><a href="#uv-tool-install--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-install--no-sources"><a href="#uv-tool-install--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-tool-install--offline"><a href="#uv-tool-install--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--overrides"><a href="#uv-tool-install--overrides"><code>--overrides</code></a>, <code>--override</code> <i>overrides</i></dt><dd><p>使用给定的需求文件覆盖版本。</p>
<p>覆盖文件是类似 <code>requirements.txt</code> 的文件，强制安装特定版本的需求，无论任何组成包声明的需求如何，也无论这是否被视为无效解析。</p>
<p>约束是<em>附加的</em>，因为它们与组成包的需求相结合，而覆盖是<em>绝对的</em>，因为它们完全替换组成包的需求。</p>
<p>也可以通过 <code>UV_OVERRIDE</code> 环境变量设置。</p></dd><dt id="uv-tool-install--prerelease"><a href="#uv-tool-install--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>：不允许所有预发布版本</li>
<li><code>allow</code>：允许所有预发布版本</li>
<li><code>if-necessary</code>：如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>：允许在其版本要求中具有显式预发布标记的第一方包的预发布版本</li>
<li><code>if-necessary-or-explicit</code>：如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-tool-install--project"><a href="#uv-tool-install--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-install--python"><a href="#uv-tool-install--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于构建工具环境的 Python 解释器。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-install--python-platform"><a href="#uv-tool-install--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装需求的平台。</p>
<p>表示为"目标三元组"，一个描述目标平台的 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标为 macOS（Darwin）时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与<em>目标</em>平台兼容的 wheel；因此，安装的发行版可能与<em>当前</em>平台不兼容。相反，任何从源代码构建的发行版可能与<em>目标</em>平台不兼容，因为它们将为<em>当前</em>平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>：<code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>：<code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>：<code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>：64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>：ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>：32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>：x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>：基于 ARM 的 macOS 目标，如 Apple Silicon 设备上所见</li>
<li><code>x86_64-apple-darwin</code>：x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>：ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>：ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>：<code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>：RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>：<code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>：<code>manylinux2014</code> 平台的 ARM64 目标。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>：ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>：<code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>：使用 Pyodide 2024 平台的 wasm32 目标。用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>：iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>：iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>：iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-tool-install--quiet"><a href="#uv-tool-install--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-install--refresh"><a href="#uv-tool-install--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-tool-install--refresh-package"><a href="#uv-tool-install--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-tool-install--reinstall"><a href="#uv-tool-install--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。意味着 <code>--refresh</code></p>
</dd><dt id="uv-tool-install--reinstall-package"><a href="#uv-tool-install--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-tool-install--resolution"><a href="#uv-tool-install--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包需求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>：解析每个包的最高兼容版本</li>
<li><code>lowest</code>：解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>：解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-tool-install--upgrade"><a href="#uv-tool-install--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh</code></p>
</dd><dt id="uv-tool-install--upgrade-package"><a href="#uv-tool-install--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包的升级，忽略任何现有输出文件中的固定版本。意味着 <code>--refresh-package</code></p>
</dd><dt id="uv-tool-install--verbose"><a href="#uv-tool-install--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-tool-install--with"><a href="#uv-tool-install--with"><code>--with</code></a>, <code>-w</code> <i>with</i></dt><dd><p>包含以下附加需求</p>
</dd><dt id="uv-tool-install--with-editable"><a href="#uv-tool-install--with-editable"><code>--with-editable</code></a> <i>with-editable</i></dt><dd><p>以可编辑模式包含给定的包</p>
</dd><dt id="uv-tool-install--with-executables-from"><a href="#uv-tool-install--with-executables-from"><code>--with-executables-from</code></a> <i>with-executables-from</i></dt><dd><p>从以下包安装可执行文件</p>
</dd><dt id="uv-tool-install--with-requirements"><a href="#uv-tool-install--with-requirements"><code>--with-requirements</code></a> <i>with-requirements</i></dt><dd><p>运行并安装给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、具有内联元数据的 <code>.py</code> 文件和 <code>pylock.toml</code>。</p>
</dd></dl>

### uv tool upgrade

升级已安装的工具。

如果工具在安装时带有版本约束，升级时这些约束将被遵循——要升级超出原始约束的工具，请再次使用 `uv tool install`。

如果工具在安装时有特定设置，升级时这些设置将被保留。例如，如果在安装时提供了 `--prereleases allow`，则在升级时将继续遵循该设置。

<h3 class="cli-reference">用法</h3>

```
uv tool upgrade [OPTIONS] <NAME>...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-tool-upgrade--name"><a href="#uv-tool-upgrade--name"<code>NAME</code></a></dt><dd><p>要升级的工具名称，以及可选的版本说明符</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-upgrade--all"><a href="#uv-tool-upgrade--all"><code>--all</code></a></dt><dd><p>升级所有工具</p>
</dd><dt id="uv-tool-upgrade--allow-insecure-host"><a href="#uv-tool-upgrade--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--cache-dir"><a href="#uv-tool-upgrade--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--color"><a href="#uv-tool-upgrade--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-tool-upgrade--compile-bytecode"><a href="#uv-tool-upgrade--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python (<code>.py</code>) 文件编译为字节码 (<code>__pycache__/*.pyc</code>)；相反，编译会在首次导入模块时延迟执行。对于启动时间至关重要的用例（例如 CLI 应用程序和 Docker 容器），可以启用此选项，以更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括当前操作未修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以通过 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--config-file"><a href="#uv-tool-upgrade--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--config-setting"><a href="#uv-tool-upgrade--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-upgrade--config-setting-package"><a href="#uv-tool-upgrade--config-setting-package"><code>--config-setting-package</code></a>, <code>--config-settings-package</code> <i>config-setting-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-tool-upgrade--default-index"><a href="#uv-tool-upgrade--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--directory"><a href="#uv-tool-upgrade--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--exclude-newer"><a href="#uv-tool-upgrade--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--exclude-newer-package"><a href="#uv-tool-upgrade--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-tool-upgrade--extra-index-url"><a href="#uv-tool-upgrade--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--find-links"><a href="#uv-tool-upgrade--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件 (<code>.whl</code>) 或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则该页面必须包含指向符合上述格式的包文件的扁平链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--fork-strategy"><a href="#uv-tool-upgrade--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本选择每个包的最新版本（<code>requires-python</code>），同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 策略下，uv 将最小化每个包选择的版本数量，优先选择与更广泛的受支持 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果旧版本与更广泛的受支持 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>:  优化为每个受支持的 Python 版本选择每个包的最新受支持版本</li>
</ul></dd><dt id="uv-tool-upgrade--help"><a href="#uv-tool-upgrade--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-tool-upgrade--index"><a href="#uv-tool-upgrade--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>不支持将索引名称作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code>，或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--index-strategy"><a href="#uv-tool-upgrade--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用返回给定包名称匹配项的第一个索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在转到下一个索引之前穷尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-tool-upgrade--index-url"><a href="#uv-tool-upgrade--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--keyring-provider"><a href="#uv-tool-upgrade--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前，仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 来处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-tool-upgrade--link-mode"><a href="#uv-tool-upgrade--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>在 macOS 上默认为 <code>clone</code>（也称为写时复制），在 Linux 和 Windows 上默认为 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-tool-upgrade--managed-python"><a href="#uv-tool-upgrade--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--native-tls"><a href="#uv-tool-upgrade--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-binary"><a href="#uv-tool-upgrade--no-binary"><code>--no-binary</code></a></dt><dd><p>不安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-binary-package"><a href="#uv-tool-upgrade--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-build"><a href="#uv-tool-upgrade--no-build"><code>--no-build</code></a></dt><dd><p>不构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源发行版的缓存 wheel，但需要构建发行版的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-build-isolation"><a href="#uv-tool-upgrade--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-build-isolation-package"><a href="#uv-tool-upgrade--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设包在 PEP 518 中指定的构建依赖项已安装。</p>
</dd><dt id="uv-tool-upgrade--no-build-package"><a href="#uv-tool-upgrade--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不为特定包构建源发行版</p>
<p>也可以通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-cache"><a href="#uv-tool-upgrade--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-config"><a href="#uv-tool-upgrade--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-index"><a href="#uv-tool-upgrade--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-tool-upgrade--no-managed-python"><a href="#uv-tool-upgrade--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-progress"><a href="#uv-tool-upgrade--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--no-python-downloads"><a href="#uv-tool-upgrade--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-upgrade--no-sources"><a href="#uv-tool-upgrade--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--offline"><a href="#uv-tool-upgrade--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--prerelease"><a href="#uv-tool-upgrade--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包，以及在其声明的说明符中包含显式预发布标记的第一方要求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-tool-upgrade--project"><a href="#uv-tool-upgrade--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--python"><a href="#uv-tool-upgrade--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>升级工具，并指定其使用给定的 Python 解释器来构建其环境。
与 <code>--all</code> 一起使用以应用于所有工具。</p>
<p>有关 Python 发现和受支持的请求格式的详细信息，请参见 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-upgrade--python-platform"><a href="#uv-tool-upgrade--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装要求的平台。</p>
<p>表示为"目标三元组"，一个描述目标平台 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标平台为 macOS (Darwin) 时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标平台为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标平台为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与目标平台兼容的 wheel；因此，安装的发行版可能与当前平台不兼容。相反，从源代码构建的任何发行版可能与目标平台不兼容，因为它们将为当前平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>:  <code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>:  <code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>:  <code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>:  64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>:  ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>:  32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>:  x86 Linux 目标。等同于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>:  基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>:  x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>:  ARM64 Linux 目标。等同于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>:  ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>:  <code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>:  RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>:  <code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等同于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>:  <code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>:  <code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>:  <code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>:  <code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>:  <code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>:  <code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>:  <code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>:  <code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>:  <code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>:  <code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>:  <code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>:  <code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>:  <code>manylinux2014</code> 平台的 ARM64 目标。等同于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>:  <code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>:  <code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>:  <code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>:  <code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>:  <code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>:  <code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>:  <code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>:  <code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>:  <code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>:  <code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>:  <code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>:  <code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>:  ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>:  <code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>:  使用 Pyodide 2024 平台的 wasm32 目标。适用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>:  iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>:  iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>:  iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-tool-upgrade--quiet"><a href="#uv-tool-upgrade--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-upgrade--reinstall"><a href="#uv-tool-upgrade--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。隐含 <code>--refresh</code></p>
</dd><dt id="uv-tool-upgrade--reinstall-package"><a href="#uv-tool-upgrade--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-tool-upgrade--resolution"><a href="#uv-tool-upgrade--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>在给定包要求的不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-tool-upgrade--verbose"><a href="#uv-tool-upgrade--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv tool list

列出已安装的工具

<h3 class="cli-reference">用法</h3>

```
uv tool list [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-list--allow-insecure-host"><a href="#uv-tool-list--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-list--cache-dir"><a href="#uv-tool-list--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-list--color"><a href="#uv-tool-list--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-tool-list--config-file"><a href="#uv-tool-list--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-list--directory"><a href="#uv-tool-list--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-list--help"><a href="#uv-tool-list--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-tool-list--managed-python"><a href="#uv-tool-list--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-list--native-tls"><a href="#uv-tool-list--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-list--no-cache"><a href="#uv-tool-list--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-list--no-config"><a href="#uv-tool-list--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-list--no-managed-python"><a href="#uv-tool-list--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-list--no-progress"><a href="#uv-tool-list--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-list--offline"><a href="#uv-tool-list--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-list--project"><a href="#uv-tool-list--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-list--quiet"><a href="#uv-tool-list--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-list--show-extras"><a href="#uv-tool-list--show-extras"><code>--show-extras</code></a></dt><dd><p>是否显示与每个工具一起安装的额外要求</p>
</dd><dt id="uv-tool-list--show-paths"><a href="#uv-tool-list--show-paths"><code>--show-paths</code></a></dt><dd><p>是否显示每个工具环境和已安装可执行文件的路径</p>
</dd><dt id="uv-tool-list--show-python"><a href="#uv-tool-list--show-python"><code>--show-python</code></a></dt><dd><p>是否显示与每个工具关联的 Python 版本</p>
</dd><dt id="uv-tool-list--show-version-specifiers"><a href="#uv-tool-list--show-version-specifiers"><code>--show-version-specifiers</code></a></dt><dd><p>是否显示用于安装每个工具的版本说明符</p>
</dd><dt id="uv-tool-list--show-with"><a href="#uv-tool-list--show-with"><code>--show-with</code></a></dt><dd><p>是否显示与每个工具一起安装的附加要求</p>
</dd><dt id="uv-tool-list--verbose"><a href="#uv-tool-list--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv tool uninstall

卸载工具

<h3 class="cli-reference">用法</h3>

```
uv tool uninstall [OPTIONS] <NAME>...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-tool-uninstall--name"><a href="#uv-tool-uninstall--name"<code>NAME</code></a></dt><dd><p>要卸载的工具名称</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-uninstall--all"><a href="#uv-tool-uninstall--all"><code>--all</code></a></dt><dd><p>卸载所有工具</p>
</dd><dt id="uv-tool-uninstall--allow-insecure-host"><a href="#uv-tool-uninstall--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--cache-dir"><a href="#uv-tool-uninstall--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--color"><a href="#uv-tool-uninstall--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-tool-uninstall--config-file"><a href="#uv-tool-uninstall--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--directory"><a href="#uv-tool-uninstall--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--help"><a href="#uv-tool-uninstall--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-tool-uninstall--managed-python"><a href="#uv-tool-uninstall--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--native-tls"><a href="#uv-tool-uninstall--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--no-cache"><a href="#uv-tool-uninstall--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--no-config"><a href="#uv-tool-uninstall--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--no-managed-python"><a href="#uv-tool-uninstall--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--no-progress"><a href="#uv-tool-uninstall--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--no-python-downloads"><a href="#uv-tool-uninstall--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-uninstall--offline"><a href="#uv-tool-uninstall--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--project"><a href="#uv-tool-uninstall--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-uninstall--quiet"><a href="#uv-tool-uninstall--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-uninstall--verbose"><a href="#uv-tool-uninstall--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv tool update-shell

确保工具可执行目录在 `PATH` 上。

如果工具可执行目录不在 `PATH` 上，uv 将尝试将其添加到相关的 shell 配置文件中。

如果 shell 配置文件已经包含将可执行目录添加到路径的说明，但该目录不在 `PATH` 上，uv 将退出并报错。

工具可执行目录根据 XDG 标准确定，可以通过 `uv tool dir --bin` 检索。

<h3 class="cli-reference">用法</h3>

```
uv tool update-shell [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-update-shell--allow-insecure-host"><a href="#uv-tool-update-shell--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--cache-dir"><a href="#uv-tool-update-shell--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--color"><a href="#uv-tool-update-shell--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-tool-update-shell--config-file"><a href="#uv-tool-update-shell--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--directory"><a href="#uv-tool-update-shell--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--help"><a href="#uv-tool-update-shell--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-tool-update-shell--managed-python"><a href="#uv-tool-update-shell--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--native-tls"><a href="#uv-tool-update-shell--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--no-cache"><a href="#uv-tool-update-shell--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--no-config"><a href="#uv-tool-update-shell--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--no-managed-python"><a href="#uv-tool-update-shell--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--no-progress"><a href="#uv-tool-update-shell--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--no-python-downloads"><a href="#uv-tool-update-shell--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-update-shell--offline"><a href="#uv-tool-update-shell--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--project"><a href="#uv-tool-update-shell--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-update-shell--quiet"><a href="#uv-tool-update-shell--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-update-shell--verbose"><a href="#uv-tool-update-shell--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv tool dir

显示 uv 工具目录的路径。

工具目录用于存储已安装工具的环境和元数据。

默认情况下，工具存储在 uv 数据目录中，位于 Unix 上的 `$XDG_DATA_HOME/uv/tools` 或 `$HOME/.local/share/uv/tools`，以及 Windows 上的 `%APPDATA%\uv\data\tools`。

工具安装目录可以通过 `$UV_TOOL_DIR` 覆盖。

要查看 uv 安装可执行文件的目录，请使用 `--bin` 标志。

<h3 class="cli-reference">用法</h3>

```
uv tool dir [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-tool-dir--allow-insecure-host"><a href="#uv-tool-dir--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--bin"><a href="#uv-tool-dir--bin"><code>--bin</code></a></dt><dd><p>显示 <code>uv tool</code> 将安装可执行文件的目录。</p>
<p>默认情况下，<code>uv tool dir</code> 显示工具 Python 环境本身安装的目录，而不是包含链接可执行文件的目录。</p>
<p>工具可执行目录根据 XDG 标准确定，并源自以下环境变量（按优先级顺序）：</p>
<ul>
<li><code>$UV_TOOL_BIN_DIR</code></li>
<li><code>$XDG_BIN_HOME</code></li>
<li><code>$XDG_DATA_HOME/../bin</code></li>
<li><code>$HOME/.local/bin</code></li>
</ul>
</dd><dt id="uv-tool-dir--cache-dir"><a href="#uv-tool-dir--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--color"><a href="#uv-tool-dir--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-tool-dir--config-file"><a href="#uv-tool-dir--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--directory"><a href="#uv-tool-dir--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--help"><a href="#uv-tool-dir--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-tool-dir--managed-python"><a href="#uv-tool-dir--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--native-tls"><a href="#uv-tool-dir--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--no-cache"><a href="#uv-tool-dir--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--no-config"><a href="#uv-tool-dir--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--no-managed-python"><a href="#uv-tool-dir--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--no-progress"><a href="#uv-tool-dir--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--no-python-downloads"><a href="#uv-tool-dir--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-tool-dir--offline"><a href="#uv-tool-dir--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--project"><a href="#uv-tool-dir--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-tool-dir--quiet"><a href="#uv-tool-dir--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-tool-dir--verbose"><a href="#uv-tool-dir--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv python

管理 Python 版本和安装

通常，uv 首先在虚拟环境（活动的或在当前工作目录或任何父目录中的 `.venv` 目录中）中搜索 Python。如果不需要虚拟环境，uv 将搜索 Python 解释器。通过在 `PATH` 环境变量中搜索 Python 可执行文件来找到 Python 解释器。

在 Windows 上，还会在注册表中搜索 Python 可执行文件。

默认情况下，如果找不到版本，uv 将下载 Python。可以使用 `--no-python-downloads` 标志或 `python-downloads` 设置禁用此行为。

`--python` 选项允许请求不同的解释器。

支持以下 Python 版本请求格式：

- `<version>` 例如 `3`、`3.12`、`3.12.3`
- `<version-specifier>` 例如 `>=3.12,<3.13`
- `<version><short-variant>`（例如 `3.13t`、`3.12.0d`）
- `<version>+<variant>`（例如 `3.13+freethreaded`、`3.12.0+debug`）
- `<implementation>` 例如 `cpython` 或 `cp`
- `<implementation>@<version>` 例如 `cpython@3.12`
- `<implementation><version>` 例如 `cpython3.12` 或 `cp312`
- `<implementation><version-specifier>` 例如 `cpython>=3.12,<3.13`
- `<implementation>-<version>-<os>-<arch>-<libc>` 例如 `cpython-3.12.3-macos-aarch64-none`

此外，通常可以使用以下方式请求特定的系统 Python 解释器：

- `<executable-path>` 例如 `/opt/homebrew/bin/python3`
- `<executable-name>` 例如 `mypython3`
- `<install-dir>` 例如 `/some/environment/`

当使用 `--python` 选项时，适用正常的发现规则，但会检查发现的解释器是否与请求兼容，例如，如果请求 `pypy`，uv 将首先检查虚拟环境是否包含 PyPy 解释器，然后检查路径中的每个可执行文件是否是 PyPy 解释器。

uv 支持发现 CPython、PyPy 和 GraalPy 解释器。不支持的解释器将在发现过程中被跳过。如果请求了不支持的解释器实现，uv 将退出并报错。

<h3 class="cli-reference">用法</h3>

```
uv python [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-python-list"><code>uv python list</code></a></dt><dd><p>列出可用的 Python 安装</p></dd>
<dt><a href="#uv-python-install"><code>uv python install</code></a></dt><dd><p>下载并安装 Python 版本</p></dd>
<dt><a href="#uv-python-upgrade"><code>uv python upgrade</code></a></dt><dd><p>升级已安装的 Python 版本</p></dd>
<dt><a href="#uv-python-find"><code>uv python find</code></a></dt><dd><p>搜索 Python 安装</p></dd>
<dt><a href="#uv-python-pin"><code>uv python pin</code></a></dt><dd><p>固定到特定的 Python 版本</p></dd>
<dt><a href="#uv-python-dir"><code>uv python dir</code></a></dt><dd><p>显示 uv Python 安装目录</p></dd>
<dt><a href="#uv-python-uninstall"><code>uv python uninstall</code></a></dt><dd><p>卸载 Python 版本</p></dd>
<dt><a href="#uv-python-update-shell"><code>uv python update-shell</code></a></dt><dd><p>确保 Python 可执行目录在 <code>PATH</code> 上</p></dd>
</dl>

### uv python list

列出可用的 Python 安装。

默认情况下，显示已安装的 Python 版本以及每个受支持的 Python 主要版本的最新可用补丁版本的下载。

使用 `--managed-python` 仅查看托管的 Python 版本。

使用 `--no-managed-python` 省略托管的 Python 版本。

使用 `--all-versions` 查看所有可用的补丁版本。

使用 `--only-installed` 省略可用的下载。

<h3 class="cli-reference">用法</h3>

```
uv python list [OPTIONS] [REQUEST]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-list--request"><a href="#uv-python-list--request"<code>REQUEST</code></a></dt><dd><p>用于过滤的 Python 请求。</p>
<p>有关支持的请求格式，请参见 <a href="#uv-python">uv python</a>。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-list--all-arches"><a href="#uv-python-list--all-arches"><code>--all-arches</code></a>, <code>--all_architectures</code></dt><dd><p>列出所有架构的 Python 下载。</p>
<p>默认情况下，仅显示当前架构的下载。</p>
</dd><dt id="uv-python-list--all-platforms"><a href="#uv-python-list--all-platforms"><code>--all-platforms</code></a></dt><dd><p>列出所有平台的 Python 下载。</p>
<p>默认情况下，仅显示当前平台的下载。</p>
</dd><dt id="uv-python-list--all-versions"><a href="#uv-python-list--all-versions"><code>--all-versions</code></a></dt><dd><p>列出所有 Python 版本，包括旧的补丁版本。</p>
<p>默认情况下，每个次要版本仅显示最新的补丁版本。</p>
</dd><dt id="uv-python-list--allow-insecure-host"><a href="#uv-python-list--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表包含的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-list--cache-dir"><a href="#uv-python-list--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-list--color"><a href="#uv-python-list--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入支持颜色的终端或 TTY 时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-list--config-file"><a href="#uv-python-list--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-list--directory"><a href="#uv-python-list--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-list--help"><a href="#uv-python-list--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助信息</p>
</dd><dt id="uv-python-list--managed-python"><a href="#uv-python-list--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-list--native-tls"><a href="#uv-python-list--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-list--no-cache"><a href="#uv-python-list--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-list--no-config"><a href="#uv-python-list--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，会在当前目录、父目录或用户配置目录中发现配置文件。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-list--no-managed-python"><a href="#uv-python-list--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-list--no-progress"><a href="#uv-python-list--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-list--no-python-downloads"><a href="#uv-python-list--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-list--offline"><a href="#uv-python-list--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-list--only-downloads"><a href="#uv-python-list--only-downloads"><code>--only-downloads</code></a></dt><dd><p>仅显示可用的 Python 下载。</p>
<p>默认情况下，显示已安装的发行版和当前平台的可用下载。</p>
</dd><dt id="uv-python-list--only-installed"><a href="#uv-python-list--only-installed"><code>--only-installed</code></a></dt><dd><p>仅显示已安装的 Python 版本。</p>
<p>默认情况下，显示已安装的发行版和当前平台的可用下载。</p>
</dd><dt id="uv-python-list--output-format"><a href="#uv-python-list--output-format"><code>--output-format</code></a> <i>output-format</i></dt><dd><p>选择输出格式</p>
<p>[默认值: text]</p><p>可能的值：</p>
<ul>
<li><code>text</code>:  纯文本（供人类阅读）</li>
<li><code>json</code>:  JSON（供计算机处理）</li>
</ul></dd><dt id="uv-python-list--project"><a href="#uv-python-list--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-list--python-downloads-json-url"><a href="#uv-python-list--python-downloads-json-url"><code>--python-downloads-json-url</code></a> <i>python-downloads-json-url</i></dt><dd><p>指向自定义 Python 安装 JSON 的 URL</p>
</dd><dt id="uv-python-list--quiet"><a href="#uv-python-list--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-list--show-urls"><a href="#uv-python-list--show-urls"><code>--show-urls</code></a></dt><dd><p>显示可用 Python 下载的 URL。</p>
<p>默认情况下，这些显示为 <code>&lt;download available&gt;</code>。</p>
</dd><dt id="uv-python-list--verbose"><a href="#uv-python-list--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python install

下载并安装 Python 版本。

支持 CPython 和 PyPy。CPython 发行版从 Astral `python-build-standalone` 项目下载。PyPy 发行版从 `python.org` 下载。可用的 Python 版本随每个 uv 版本捆绑。要安装新的 Python 版本，您可能需要升级 uv。

Python 版本被安装到 uv Python 目录中，该目录可以通过 `uv python dir` 获取。

默认情况下，Python 可执行文件被添加到路径中的一个目录，并带有次要版本后缀，例如 `python3.13`。要安装 `python3` 和 `python`，请使用 `--default` 标志。使用 `uv python dir --bin` 查看目标目录。

可以请求多个 Python 版本。

查看 `uv help python` 以查看支持的请求格式。

<h3 class="cli-reference">用法</h3>

```
uv python install [OPTIONS] [TARGETS]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-install--targets"><a href="#uv-python-install--targets"<code>TARGETS</code></a></dt><dd><p>要安装的 Python 版本。</p>
<p>如果未提供，将从 <code>UV_PYTHON</code> 环境变量，然后从 <code>.python-versions</code> 或 <code>.python-version</code> 文件读取请求的 Python 版本。如果上述均不存在，uv 将检查是否已安装任何 Python 版本。如果没有，它将安装最新的稳定版 Python。</p>
<p>查看 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-install--allow-insecure-host"><a href="#uv-python-install--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-install--cache-dir"><a href="#uv-python-install--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-install--color"><a href="#uv-python-install--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-install--config-file"><a href="#uv-python-install--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-install--default"><a href="#uv-python-install--default"><code>--default</code></a></dt><dd><p>用作默认 Python 版本。</p>
<p>默认情况下，仅安装 <code>python{major}.{minor}</code> 可执行文件，例如 <code>python3.10</code>。当使用 <code>--default</code> 标志时，还会安装 <code>python{major}</code>（例如 <code>python3</code>）和 <code>python</code> 可执行文件。</p>
<p>替代的 Python 变体仍将包含其标签。例如，使用 <code>--default</code> 安装 3.13+freethreaded 将包括 <code>python3t</code> 和 <code>pythont</code>，而不是 <code>python3</code> 和 <code>python</code>。</p>
<p>如果请求了多个 Python 版本，uv 将报错退出。</p>
</dd><dt id="uv-python-install--directory"><a href="#uv-python-install--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-install--force"><a href="#uv-python-install--force"><code>--force</code></a>, <code>-f</code></dt><dd><p>在安装期间替换现有的 Python 可执行文件。</p>
<p>默认情况下，uv 将拒绝替换其不管理的可执行文件。</p>
<p>隐含 <code>--reinstall</code>。</p>
</dd><dt id="uv-python-install--help"><a href="#uv-python-install--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-install--install-dir"><a href="#uv-python-install--install-dir"><code>--install-dir</code></a>, <code>-i</code> <i>install-dir</i></dt><dd><p>存储 Python 安装的目录。</p>
<p>如果提供，后续操作将需要设置 <code>UV_PYTHON_INSTALL_DIR</code> 以便 uv 发现 Python 安装。</p>
<p>查看 <code>uv python dir</code> 以查看当前 Python 安装目录。默认为 <code>~/.local/share/uv/python</code>。</p>
<p>也可以通过 <code>UV_PYTHON_INSTALL_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-install--managed-python"><a href="#uv-python-install--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-install--mirror"><a href="#uv-python-install--mirror"><code>--mirror</code></a> <i>mirror</i></dt><dd><p>设置用作下载 Python 安装源的 URL。</p>
<p>提供的 URL 将替换例如 <code>https://github.com/astral-sh/python-build-standalone/releases/download/20240713/cpython-3.12.4%2B20240713-aarch64-apple-darwin-install_only.tar.gz</code> 中的 <code>https://github.com/astral-sh/python-build-standalone/releases/download</code>。</p>
<p>可以使用 <code>file://</code> URL 方案从本地目录读取发行版。</p>
</dd><dt id="uv-python-install--native-tls"><a href="#uv-python-install--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-install--no-bin"><a href="#uv-python-install--no-bin"><code>--no-bin</code></a></dt><dd><p>不将 Python 可执行文件安装到 <code>bin</code> 目录。</p>
<p>这也可以通过 <code>UV_PYTHON_INSTALL_BIN=0</code> 设置。</p>
</dd><dt id="uv-python-install--no-cache"><a href="#uv-python-install--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-install--no-config"><a href="#uv-python-install--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-install--no-managed-python"><a href="#uv-python-install--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-install--no-progress"><a href="#uv-python-install--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-install--no-python-downloads"><a href="#uv-python-install--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-install--no-registry"><a href="#uv-python-install--no-registry"><code>--no-registry</code></a></dt><dd><p>不在 Windows 注册表中注册 Python 安装。</p>
<p>这也可以通过 <code>UV_PYTHON_INSTALL_REGISTRY=0</code> 设置。</p>
</dd><dt id="uv-python-install--offline"><a href="#uv-python-install--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-install--project"><a href="#uv-python-install--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-install--pypy-mirror"><a href="#uv-python-install--pypy-mirror"><code>--pypy-mirror</code></a> <i>pypy-mirror</i></dt><dd><p>设置用作下载 PyPy 安装源的 URL。</p>
<p>提供的 URL 将替换例如 <code>https://downloads.python.org/pypy/pypy3.8-v7.3.7-osx64.tar.bz2</code> 中的 <code>https://downloads.python.org/pypy</code>。</p>
<p>可以使用 <code>file://</code> URL 方案从本地目录读取发行版。</p>
</dd><dt id="uv-python-install--python-downloads-json-url"><a href="#uv-python-install--python-downloads-json-url"><code>--python-downloads-json-url</code></a> <i>python-downloads-json-url</i></dt><dd><p>指向自定义 Python 安装 JSON 的 URL</p>
</dd><dt id="uv-python-install--quiet"><a href="#uv-python-install--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-install--reinstall"><a href="#uv-python-install--reinstall"><code>--reinstall</code></a>, <code>-r</code></dt><dd><p>重新安装请求的 Python 版本（如果已安装）。</p>
<p>默认情况下，如果版本已安装，uv 将成功退出。</p>
</dd><dt id="uv-python-install--upgrade"><a href="#uv-python-install--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>将现有的 Python 安装升级到最新的补丁版本。</p>
<p>默认情况下，uv 不会将已安装的 Python 版本升级到较新的补丁版本。使用 <code>--upgrade</code> 时，uv 将升级到指定次要版本可用的最新补丁版本。</p>
<p>如果请求的版本尚未安装，uv 将安装它们。</p>
<p>此选项仅支持次要版本请求，例如 <code>3.12</code>；如果请求补丁版本，例如 <code>3.12.2</code>，uv 将报错退出。</p>
</dd><dt id="uv-python-install--verbose"><a href="#uv-python-install--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python upgrade

升级已安装的 Python 版本。

将版本升级到最新的受支持补丁版本。需要 `python-upgrade` 预览功能。

可以提供要升级的目标 Python 次要版本，例如 `3.13`。可以提供多个版本来执行多次升级。

如果未提供目标版本，则 uv 将升级所有受管理的 CPython 版本。

在升级期间，uv 不会卸载过时的补丁版本。

执行升级时，由 uv 创建的虚拟环境将自动使用新版本。但是，如果虚拟环境是在升级功能添加之前创建的，它将继续使用旧的 Python 版本；要启用升级，必须重新创建环境。

尚不支持替代实现（如 PyPy）的升级。

<h3 class="cli-reference">用法</h3>

```
uv python upgrade [OPTIONS] [TARGETS]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-upgrade--targets"><a href="#uv-python-upgrade--targets"<code>TARGETS</code></a></dt><dd><p>要升级的 Python 次要版本。</p>
<p>如果未提供目标版本，则 uv 将升级所有受管理的 CPython 版本。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-upgrade--allow-insecure-host"><a href="#uv-python-upgrade--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--cache-dir"><a href="#uv-python-upgrade--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--color"><a href="#uv-python-upgrade--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-upgrade--config-file"><a href="#uv-python-upgrade--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--directory"><a href="#uv-python-upgrade--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--help"><a href="#uv-python-upgrade--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-upgrade--install-dir"><a href="#uv-python-upgrade--install-dir"><code>--install-dir</code></a>, <code>-i</code> <i>install-dir</i></dt><dd><p>存储 Python 安装的目录。</p>
<p>如果提供，后续操作将需要设置 <code>UV_PYTHON_INSTALL_DIR</code> 以便 uv 发现 Python 安装。</p>
<p>查看 <code>uv python dir</code> 以查看当前 Python 安装目录。默认为 <code>~/.local/share/uv/python</code>。</p>
<p>也可以通过 <code>UV_PYTHON_INSTALL_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--managed-python"><a href="#uv-python-upgrade--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--mirror"><a href="#uv-python-upgrade--mirror"><code>--mirror</code></a> <i>mirror</i></dt><dd><p>设置用作下载 Python 安装源的 URL。</p>
<p>提供的 URL 将替换例如 <code>https://github.com/astral-sh/python-build-standalone/releases/download/20240713/cpython-3.12.4%2B20240713-aarch64-apple-darwin-install_only.tar.gz</code> 中的 <code>https://github.com/astral-sh/python-build-standalone/releases/download</code>。</p>
<p>可以使用 <code>file://</code> URL 方案从本地目录读取发行版。</p>
</dd><dt id="uv-python-upgrade--native-tls"><a href="#uv-python-upgrade--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--no-cache"><a href="#uv-python-upgrade--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--no-config"><a href="#uv-python-upgrade--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--no-managed-python"><a href="#uv-python-upgrade--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--no-progress"><a href="#uv-python-upgrade--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--no-python-downloads"><a href="#uv-python-upgrade--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-upgrade--offline"><a href="#uv-python-upgrade--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--project"><a href="#uv-python-upgrade--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-upgrade--pypy-mirror"><a href="#uv-python-upgrade--pypy-mirror"><code>--pypy-mirror</code></a> <i>pypy-mirror</i></dt><dd><p>设置用作下载 PyPy 安装源的 URL。</p>
<p>提供的 URL 将替换例如 <code>https://downloads.python.org/pypy/pypy3.8-v7.3.7-osx64.tar.bz2</code> 中的 <code>https://downloads.python.org/pypy</code>。</p>
<p>可以使用 <code>file://</code> URL 方案从本地目录读取发行版。</p>
</dd><dt id="uv-python-upgrade--python-downloads-json-url"><a href="#uv-python-upgrade--python-downloads-json-url"><code>--python-downloads-json-url</code></a> <i>python-downloads-json-url</i></dt><dd><p>指向自定义 Python 安装 JSON 的 URL</p>
</dd><dt id="uv-python-upgrade--quiet"><a href="#uv-python-upgrade--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-upgrade--reinstall"><a href="#uv-python-upgrade--reinstall"><code>--reinstall</code></a>, <code>-r</code></dt><dd><p>重新安装最新的 Python 补丁（如果已安装）。</p>
<p>默认情况下，如果最新的补丁已安装，uv 将成功退出。</p>
</dd><dt id="uv-python-upgrade--verbose"><a href="#uv-python-upgrade--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python find

搜索 Python 安装。

显示 Python 可执行文件的路径。

查看 `uv help python` 以查看支持的请求格式和发现行为的详细信息。

<h3 class="cli-reference">用法</h3>

```
uv python find [OPTIONS] [REQUEST]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-find--request"><a href="#uv-python-find--request"<code>REQUEST</code></a></dt><dd><p>Python 请求。</p>
<p>查看 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-find--allow-insecure-host"><a href="#uv-python-find--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-find--cache-dir"><a href="#uv-python-find--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-find--color"><a href="#uv-python-find--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-find--config-file"><a href="#uv-python-find--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-find--directory"><a href="#uv-python-find--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-find--help"><a href="#uv-python-find--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-find--managed-python"><a href="#uv-python-find--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-find--native-tls"><a href="#uv-python-find--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-find--no-cache"><a href="#uv-python-find--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-find--no-config"><a href="#uv-python-find--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-find--no-managed-python"><a href="#uv-python-find--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-find--no-progress"><a href="#uv-python-find--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-find--no-project"><a href="#uv-python-find--no-project"><code>--no-project</code></a>, <code>--no_workspace</code></dt><dd><p>避免发现项目或工作区。</p>
<p>否则，当未提供请求时，将使用当前目录或父目录中项目的 Python 要求。</p>
</dd><dt id="uv-python-find--no-python-downloads"><a href="#uv-python-find--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-find--offline"><a href="#uv-python-find--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-find--project"><a href="#uv-python-find--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-find--python-downloads-json-url"><a href="#uv-python-find--python-downloads-json-url"><code>--python-downloads-json-url</code></a> <i>python-downloads-json-url</i></dt><dd><p>指向自定义 Python 安装 JSON 的 URL</p>
</dd><dt id="uv-python-find--quiet"><a href="#uv-python-find--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-find--script"><a href="#uv-python-find--script"><code>--script</code></a> <i>script</i></dt><dd><p>查找 Python 脚本的环境，而不是当前项目</p>
</dd><dt id="uv-python-find--show-version"><a href="#uv-python-find--show-version"><code>--show-version</code></a></dt><dd><p>显示将使用的 Python 版本，而不是解释器的路径</p>
</dd><dt id="uv-python-find--system"><a href="#uv-python-find--system"><code>--system</code></a></dt><dd><p>仅查找系统 Python 解释器。</p>
<p>默认情况下，uv 将报告它将使用的第一个 Python 解释器，包括活动虚拟环境中的解释器或当前工作目录或任何父目录中的虚拟环境中的解释器。</p>
<p><code>--system</code> 选项指示 uv 跳过虚拟环境 Python 解释器，并将其搜索限制在系统路径中。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-find--verbose"><a href="#uv-python-find--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python pin

固定到特定的 Python 版本。

将固定的 Python 版本写入 `.python-version` 文件，其他 uv 命令使用该文件来确定所需的 Python 版本。

如果未提供版本，uv 将查找现有的 `.python-version` 文件并显示当前固定的版本。如果未找到 `.python-version` 文件，uv 将报错退出。

查看 `uv help python` 以查看支持的请求格式。

<h3 class="cli-reference">用法</h3>

```
uv python pin [OPTIONS] [REQUEST]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-pin--request"><a href="#uv-python-pin--request"<code>REQUEST</code></a></dt><dd><p>Python 版本请求。</p>
<p>uv 支持的格式比读取 <code>.python-version</code> 文件的其他工具（即 <code>pyenv</code>）更多。如果需要与这些工具兼容，请仅使用版本号而不是复杂的请求，例如 <code>cpython@3.10</code>。</p>
<p>如果未提供请求，将显示当前固定的版本。</p>
<p>查看 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-pin--allow-insecure-host"><a href="#uv-python-pin--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-pin--cache-dir"><a href="#uv-python-pin--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-pin--color"><a href="#uv-python-pin--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-pin--config-file"><a href="#uv-python-pin--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-pin--directory"><a href="#uv-python-pin--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-pin--global"><a href="#uv-python-pin--global"><code>--global</code></a></dt><dd><p>更新全局 Python 版本固定。</p>
<p>将固定的 Python 版本写入 uv 用户配置目录中的 <code>.python-version</code> 文件：Linux/macOS 上的 <code>XDG_CONFIG_HOME/uv</code> 和 Windows 上的 <code>%APPDATA%/uv</code>。</p>
<p>当在工作目录或祖先目录中未找到本地 Python 版本固定时，将使用此版本。</p>
</dd><dt id="uv-python-pin--help"><a href="#uv-python-pin--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-pin--managed-python"><a href="#uv-python-pin--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-pin--native-tls"><a href="#uv-python-pin--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-pin--no-cache"><a href="#uv-python-pin--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-pin--no-config"><a href="#uv-python-pin--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-pin--no-managed-python"><a href="#uv-python-pin--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-pin--no-progress"><a href="#uv-python-pin--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-pin--no-project"><a href="#uv-python-pin--no-project"><code>--no-project</code></a>, <code>--no-workspace</code></dt><dd><p>避免验证 Python 固定是否与项目或工作区兼容。</p>
<p>默认情况下，会在当前目录或任何父目录中发现项目或工作区。如果找到工作区，将根据工作区的 <code>requires-python</code> 约束验证 Python 固定。</p>
</dd><dt id="uv-python-pin--no-python-downloads"><a href="#uv-python-pin--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-pin--offline"><a href="#uv-python-pin--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-pin--project"><a href="#uv-python-pin--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-pin--quiet"><a href="#uv-python-pin--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-pin--resolved"><a href="#uv-python-pin--resolved"><code>--resolved</code></a></dt><dd><p>写入解析后的 Python 解释器路径而不是请求。</p>
<p>确保使用完全相同的解释器。</p>
<p>此选项在将 <code>.python-version</code> 文件提交到版本控制时通常不安全使用。</p>
</dd><dt id="uv-python-pin--rm"><a href="#uv-python-pin--rm"><code>--rm</code></a></dt><dd><p>移除 Python 版本固定</p>
</dd><dt id="uv-python-pin--verbose"><a href="#uv-python-pin--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python dir

显示 uv Python 安装目录。

默认情况下，Python 安装存储在 uv 数据目录中，Unix 上为 `$XDG_DATA_HOME/uv/python` 或 `$HOME/.local/share/uv/python`，Windows 上为 `%APPDATA%\uv\data\python`。

Python 安装目录可以通过 `$UV_PYTHON_INSTALL_DIR` 覆盖。

要查看 uv 安装 Python 可执行文件的目录，请使用 `--bin` 标志。Python 可执行文件目录可以通过 `$UV_PYTHON_BIN_DIR` 覆盖。请注意，仅当启用预览模式时才会安装 Python 可执行文件。

<h3 class="cli-reference">用法</h3>

```
uv python dir [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-dir--allow-insecure-host"><a href="#uv-python-dir--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-dir--bin"><a href="#uv-python-dir--bin"><code>--bin</code></a></dt><dd><p>显示 <code>uv python</code> 将安装 Python 可执行文件的目录。</p>
<p>请注意，此目录仅在启用预览模式安装 Python 时使用。</p>
<p>Python 可执行文件目录根据 XDG 标准确定，并源自以下环境变量，按优先级顺序：</p>
<ul>
<li><code>$UV_PYTHON_BIN_DIR</code></li>
<li><code>$XDG_BIN_HOME</code></li>
<li><code>$XDG_DATA_HOME/../bin</code></li>
<li><code>$HOME/.local/bin</code></li>
</ul>
</dd><dt id="uv-python-dir--cache-dir"><a href="#uv-python-dir--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-dir--color"><a href="#uv-python-dir--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-dir--config-file"><a href="#uv-python-dir--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-dir--directory"><a href="#uv-python-dir--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-dir--help"><a href="#uv-python-dir--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-dir--managed-python"><a href="#uv-python-dir--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-dir--native-tls"><a href="#uv-python-dir--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-dir--no-cache"><a href="#uv-python-dir--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-dir--no-config"><a href="#uv-python-dir--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-dir--no-managed-python"><a href="#uv-python-dir--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-dir--no-progress"><a href="#uv-python-dir--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-dir--no-python-downloads"><a href="#uv-python-dir--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-dir--offline"><a href="#uv-python-dir--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-dir--project"><a href="#uv-python-dir--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-dir--quiet"><a href="#uv-python-dir--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-dir--verbose"><a href="#uv-python-dir--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python uninstall

卸载 Python 版本

<h3 class="cli-reference">用法</h3>

```
uv python uninstall [OPTIONS] <TARGETS>...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-python-uninstall--targets"><a href="#uv-python-uninstall--targets"<code>TARGETS</code></a></dt><dd><p>要卸载的 Python 版本。</p>
<p>查看 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-uninstall--all"><a href="#uv-python-uninstall--all"><code>--all</code></a></dt><dd><p>卸载所有受管理的 Python 版本</p>
</dd><dt id="uv-python-uninstall--allow-insecure-host"><a href="#uv-python-uninstall--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--cache-dir"><a href="#uv-python-uninstall--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--color"><a href="#uv-python-uninstall--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-uninstall--config-file"><a href="#uv-python-uninstall--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--directory"><a href="#uv-python-uninstall--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--help"><a href="#uv-python-uninstall--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-uninstall--install-dir"><a href="#uv-python-uninstall--install-dir"><code>--install-dir</code></a>, <code>-i</code> <i>install-dir</i></dt><dd><p>Python 被安装的目录</p>
<p>也可以通过 <code>UV_PYTHON_INSTALL_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--managed-python"><a href="#uv-python-uninstall--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--native-tls"><a href="#uv-python-uninstall--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--no-cache"><a href="#uv-python-uninstall--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--no-config"><a href="#uv-python-uninstall--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--no-managed-python"><a href="#uv-python-uninstall--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--no-progress"><a href="#uv-python-uninstall--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--no-python-downloads"><a href="#uv-python-uninstall--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-uninstall--offline"><a href="#uv-python-uninstall--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--project"><a href="#uv-python-uninstall--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-uninstall--quiet"><a href="#uv-python-uninstall--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-uninstall--verbose"><a href="#uv-python-uninstall--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv python update-shell

确保 Python 可执行文件目录在 `PATH` 上。

如果 Python 可执行文件目录不在 `PATH` 上，uv 将尝试将其添加到相关的 shell 配置文件中。

如果 shell 配置文件已经包含了将可执行文件目录添加到路径的说明，但该目录不在 `PATH` 上，uv 将报错退出。

Python 可执行文件目录根据 XDG 标准确定，可以通过 `uv python dir --bin` 获取。

<h3 class="cli-reference">用法</h3>

```
uv python update-shell [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-python-update-shell--allow-insecure-host"><a href="#uv-python-update-shell--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--cache-dir"><a href="#uv-python-update-shell--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--color"><a href="#uv-python-update-shell--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-python-update-shell--config-file"><a href="#uv-python-update-shell--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--directory"><a href="#uv-python-update-shell--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--help"><a href="#uv-python-update-shell--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-python-update-shell--managed-python"><a href="#uv-python-update-shell--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--native-tls"><a href="#uv-python-update-shell--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--no-cache"><a href="#uv-python-update-shell--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--no-config"><a href="#uv-python-update-shell--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--no-managed-python"><a href="#uv-python-update-shell--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--no-progress"><a href="#uv-python-update-shell--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--no-python-downloads"><a href="#uv-python-update-shell--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-python-update-shell--offline"><a href="#uv-python-update-shell--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--project"><a href="#uv-python-update-shell--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-python-update-shell--quiet"><a href="#uv-python-update-shell--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-python-update-shell--verbose"><a href="#uv-python-update-shell--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv pip

使用 pip 兼容的接口管理 Python 包

<h3 class="cli-reference">用法</h3>

```
uv pip [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-pip-compile"><code>uv pip compile</code></a></dt><dd><p>将 <code>requirements.in</code> 文件编译为 <code>requirements.txt</code> 或 <code>pylock.toml</code> 文件</p></dd>
<dt><a href="#uv-pip-sync"><code>uv pip sync</code></a></dt><dd><p>使用 <code>requirements.txt</code> 或 <code>pylock.toml</code> 文件同步环境</p></dd>
<dt><a href="#uv-pip-install"><code>uv pip install</code></a></dt><dd><p>将包安装到环境中</p></dd>
<dt><a href="#uv-pip-uninstall"><code>uv pip uninstall</code></a></dt><dd><p>从环境中卸载包</p></dd>
<dt><a href="#uv-pip-freeze"><code>uv pip freeze</code></a></dt><dd><p>以 requirements 格式列出环境中安装的包</p></dd>
<dt><a href="#uv-pip-list"><code>uv pip list</code></a></dt><dd><p>以表格格式列出环境中安装的包</p></dd>
<dt><a href="#uv-pip-show"><code>uv pip show</code></a></dt><dd><p>显示一个或多个已安装包的信息</p></dd>
<dt><a href="#uv-pip-tree"><code>uv pip tree</code></a></dt><dd><p>显示环境的依赖树</p></dd>
<dt><a href="#uv-pip-check"><code>uv pip check</code></a></dt><dd><p>验证已安装的包具有兼容的依赖项</p></dd>
</dl>

### uv pip compile

将 `requirements.in` 文件编译为 `requirements.txt` 或 `pylock.toml` 文件

<h3 class="cli-reference">用法</h3>

```
uv pip compile [OPTIONS] <SRC_FILE|--group <GROUP>>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-pip-compile--src_file"><a href="#uv-pip-compile--src_file"<code>SRC_FILE</code></a></dt><dd><p>包含给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、带有内联元数据的 <code>.py</code> 文件、<code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code>。</p>
<p>如果提供了 <code>pyproject.toml</code>、<code>setup.py</code> 或 <code>setup.cfg</code> 文件，uv 将提取相关项目的要求。</p>
<p>如果提供 <code>-</code>，则将从 stdin 读取要求。</p>
<p>要求文件的顺序和其中的要求顺序用于在解析期间确定优先级。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-compile--all-extras"><a href="#uv-pip-compile--all-extras"><code>--all-extras</code></a></dt><dd><p>包含所有可选依赖项。</p>
<p>仅适用于 <code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code> 源。</p>
</dd><dt id="uv-pip-compile--allow-insecure-host"><a href="#uv-pip-compile--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许到主机的非安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会针对系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过了 SSL 验证，可能使您遭受 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--annotation-style"><a href="#uv-pip-compile--annotation-style"><code>--annotation-style</code></a> <i>annotation-style</i></dt><dd><p>输出文件中包含的注释注解的样式，用于指示每个包的来源。</p>
<p>默认为 <code>split</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>line</code>:  在单行、逗号分隔的行上呈现注解</li>
<li><code>split</code>:  在每个单独的行上呈现每个注解</li>
</ul></dd><dt id="uv-pip-compile--build-constraints"><a href="#uv-pip-compile--build-constraints"><code>--build-constraints</code></a>, <code>--build-constraint</code>, <code>-b</code> <i>build-constraints</i></dt><dd><p>在构建源发行版时，使用给定的要求文件约束构建依赖项。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的要求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>也可以通过 <code>UV_BUILD_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--cache-dir"><a href="#uv-pip-compile--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--color"><a href="#uv-pip-compile--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-pip-compile--config-file"><a href="#uv-pip-compile--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--config-setting"><a href="#uv-pip-compile--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-pip-compile--config-settings-package"><a href="#uv-pip-compile--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-pip-compile--constraints"><a href="#uv-pip-compile--constraints"><code>--constraints</code></a>, <code>--constraint</code>, <code>-c</code> <i>constraints</i></dt><dd><p>使用给定的要求文件约束版本。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的要求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>这相当于 pip 的 <code>--constraint</code> 选项。</p>
<p>也可以通过 <code>UV_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--custom-compile-command"><a href="#uv-pip-compile--custom-compile-command"><code>--custom-compile-command</code></a> <i>custom-compile-command</i></dt><dd><p><code>uv pip compile</code> 生成的输出文件顶部包含的标题注释。</p>
<p>用于反映包装 <code>uv pip compile</code> 的自定义构建脚本和命令。</p>
<p>也可以通过 <code>UV_CUSTOM_COMPILE_COMMAND</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--default-index"><a href="#uv-pip-compile--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或布局格式相同的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--directory"><a href="#uv-pip-compile--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基础进行解析。</p>
<p>查看 <code>--project</code> 以仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--emit-build-options"><a href="#uv-pip-compile--emit-build-options"><code>--emit-build-options</code></a></dt><dd><p>在生成的输出文件中包含 <code>--no-binary</code> 和 <code>--only-binary</code> 条目</p>
</dd><dt id="uv-pip-compile--emit-find-links"><a href="#uv-pip-compile--emit-find-links"><code>--emit-find-links</code></a></dt><dd><p>在生成的输出文件中包含 <code>--find-links</code> 条目</p>
</dd><dt id="uv-pip-compile--emit-index-annotation"><a href="#uv-pip-compile--emit-index-annotation"><code>--emit-index-annotation</code></a></dt><dd><p>包含注释注解，指示用于解析每个包的索引（例如 <code># from https://pypi.org/simple</code>）</p>
</dd><dt id="uv-pip-compile--emit-index-url"><a href="#uv-pip-compile--emit-index-url"><code>--emit-index-url</code></a></dt><dd><p>在生成的输出文件中包含 <code>--index-url</code> 和 <code>--extra-index-url</code> 条目</p>
</dd><dt id="uv-pip-compile--exclude-newer"><a href="#uv-pip-compile--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--exclude-newer-package"><a href="#uv-pip-compile--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-pip-compile--excludes"><a href="#uv-pip-compile--excludes"><code>--excludes</code></a>, <code>--exclude</code> <i>excludes</i></dt><dd><p>使用给定的要求文件从解析中排除包。</p>
<p>排除文件是类似 <code>requirements.txt</code> 的文件，指定要从解析中排除的包。当包被排除时，它将完全从依赖列表中省略，并且在解析阶段将忽略其自身的依赖项。排除是无条件的，因为要求说明符和标记被忽略；提供的文件中列出的任何包将从所有解析的环境中省略。</p>
<p>也可以通过 <code>UV_EXCLUDE</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--extra"><a href="#uv-pip-compile--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>包含来自指定额外名称的可选依赖项；可以多次提供。</p>
<p>仅适用于 <code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code> 源。</p>
</dd><dt id="uv-pip-compile--extra-index-url"><a href="#uv-pip-compile--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code>。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或布局格式相同的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--find-links"><a href="#uv-pip-compile--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选发行版之外，还要搜索候选发行版的位置。</p>
<p>如果是路径，则目标必须是包含 wheel 文件（<code>.whl</code>）或源发行版（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录，这些文件位于顶层。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--fork-strategy"><a href="#uv-pip-compile--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的较旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>:  优化为每个包选择最少数量的版本。如果较旧的版本与更广泛支持的 Python 版本或平台兼容，则优先选择较旧的版本</li>
<li><code>requires-python</code>:  优化为每个支持的 Python 版本选择每个包的最新支持版本</li>
</ul></dd><dt id="uv-pip-compile--format"><a href="#uv-pip-compile--format"><code>--format</code></a> <i>format</i></dt><dd><p>解析结果应输出的格式。</p>
<p>支持 <code>requirements.txt</code> 和 <code>pylock.toml</code>（PEP 751）输出格式。</p>
<p>如果提供了输出文件，uv 将从输出文件的文件扩展名推断输出格式。否则，默认为 <code>requirements.txt</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>requirements.txt</code>:  以 <code>requirements.txt</code> 格式导出</li>
<li><code>pylock.toml</code>:  以 <code>pylock.toml</code> 格式导出</li>
</ul></dd><dt id="uv-pip-compile--generate-hashes"><a href="#uv-pip-compile--generate-hashes"><code>--generate-hashes</code></a></dt><dd><p>在输出文件中包含发行版哈希</p>
</dd><dt id="uv-pip-compile--group"><a href="#uv-pip-compile--group"><code>--group</code></a> <i>group</i></dt><dd><p>从 <code>pyproject.toml</code> 安装指定的依赖组。</p>
<p>如果未提供路径，则使用工作目录中的 <code>pyproject.toml</code>。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-pip-compile--help"><a href="#uv-pip-compile--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-compile--index"><a href="#uv-pip-compile--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或布局格式相同的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--index-strategy"><a href="#uv-pip-compile--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的版本（<code>first-index</code>）。这防止了"依赖混淆"攻击，攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>:  仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>:  在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>:  在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-pip-compile--index-url"><a href="#uv-pip-compile--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或布局格式相同的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--keyring-provider"><a href="#uv-pip-compile--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-pip-compile--link-mode"><a href="#uv-pip-compile--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅在构建源发行版时使用。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>:  从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>:  从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>:  从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>:  从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-pip-compile--managed-python"><a href="#uv-pip-compile--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--native-tls"><a href="#uv-pip-compile--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-annotate"><a href="#uv-pip-compile--no-annotate"><code>--no-annotate</code></a></dt><dd><p>排除指示每个包来源的注释注解</p>
</dd><dt id="uv-pip-compile--no-binary"><a href="#uv-pip-compile--no-binary"><code>--no-binary</code></a> <i>no-binary</i></dt><dd><p>不安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>可以提供多个包。使用 <code>:all:</code> 禁用所有包的二进制文件。使用 <code>:none:</code> 清除先前指定的包。</p>
</dd><dt id="uv-pip-compile--no-build"><a href="#uv-pip-compile--no-build"><code>--no-build</code></a></dt><dd><p>不构建源发行版。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源发行版的缓存 wheel，但需要构建发行版的操作将报错退出。</p>
<p><code>--only-binary :all:</code> 的别名。</p>
</dd><dt id="uv-pip-compile--no-build-isolation"><a href="#uv-pip-compile--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-build-isolation-package"><a href="#uv-pip-compile--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源发行版时禁用隔离。</p>
<p>假设 PEP 518 指定的包构建依赖项已安装。</p>
</dd><dt id="uv-pip-compile--no-cache"><a href="#uv-pip-compile--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-deps"><a href="#uv-pip-compile--no-deps"><code>--no-deps</code></a></dt><dd><p>忽略包依赖项，而是仅将命令行上明确列出的那些包添加到生成的要求文件中</p>
</dd><dt id="uv-pip-compile--no-emit-package"><a href="#uv-pip-compile--no-emit-package"><code>--no-emit-package</code></a>, <code>--unsafe-package</code> <i>no-emit-package</i></dt><dd><p>指定要从输出解析中省略的包。其依赖项仍将包含在解析中。相当于 pip-compile 的 <code>--unsafe-package</code> 选项</p>
</dd><dt id="uv-pip-compile--no-header"><a href="#uv-pip-compile--no-header"><code>--no-header</code></a></dt><dd><p>排除生成输出文件顶部的注释标题</p>
</dd><dt id="uv-pip-compile--no-index"><a href="#uv-pip-compile--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-pip-compile--no-managed-python"><a href="#uv-pip-compile--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-progress"><a href="#uv-pip-compile--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调器或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-python-downloads"><a href="#uv-pip-compile--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-compile--no-sources"><a href="#uv-pip-compile--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--no-strip-extras"><a href="#uv-pip-compile--no-strip-extras"><code>--no-strip-extras</code></a></dt><dd><p>在输出文件中包含 extras。</p>
<p>默认情况下，uv 会剥离 extras，因为由 extras 引入的任何包已经作为依赖项直接包含在输出文件中。此外，使用 <code>--no-strip-extras</code> 生成的输出文件不能用作 <code>install</code> 和 <code>sync</code> 调用中的约束文件。</p>
</dd><dt id="uv-pip-compile--no-strip-markers"><a href="#uv-pip-compile--no-strip-markers"><code>--no-strip-markers</code></a></dt><dd><p>在输出文件中包含环境标记。</p>
<p>默认情况下，uv 会剥离环境标记，因为 <code>compile</code> 生成的解析仅保证对目标环境正确。</p>
</dd><dt id="uv-pip-compile--offline"><a href="#uv-pip-compile--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--only-binary"><a href="#uv-pip-compile--only-binary"><code>--only-binary</code></a> <i>only-binary</i></dt><dd><p>仅使用预构建的 wheel；不构建源发行版。</p>
<p>启用后，解析将不会从给定包运行代码。将重用已构建源发行版的缓存 wheel，但需要构建发行版的操作将报错退出。</p>
<p>可以提供多个包。使用 <code>:all:</code> 禁用所有包的二进制文件。使用 <code>:none:</code> 清除先前指定的包。</p>
</dd><dt id="uv-pip-compile--output-file"><a href="#uv-pip-compile--output-file"><code>--output-file</code></a>, <code>-o</code> <i>output-file</i></dt><dd><p>将编译的要求写入给定的 <code>requirements.txt</code> 或 <code>pylock.toml</code> 文件。</p>
<p>如果文件已存在，则在解析依赖项时将优先使用现有版本，除非还指定了 <code>--upgrade</code>。</p>
</dd><dt id="uv-pip-compile--overrides"><a href="#uv-pip-compile--overrides"><code>--overrides</code></a>, <code>--override</code> <i>overrides</i></dt><dd><p>使用给定的要求文件覆盖版本。</p>
<p>覆盖文件是类似 <code>requirements.txt</code> 的文件，强制安装特定版本的要求，无论任何组成包声明的要求如何，也无论这是否被视为无效解析。</p>
<p>虽然约束是<em>累加的</em>，因为它们与组成包的要求相结合，但覆盖是<em>绝对的</em>，因为它们完全替换组成包的要求。</p>
<p>也可以通过 <code>UV_OVERRIDE</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--prerelease"><a href="#uv-pip-compile--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受<em>仅</em>发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方要求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可以通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于在其版本要求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本要求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-pip-compile--project"><a href="#uv-pip-compile--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录解析。</p>
<p>查看 <code>--directory</code> 以完全更改工作目录。</p>
<p>此设置在 <code>uv pip</code> 接口中使用时无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--python"><a href="#uv-pip-compile--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>解析期间使用的 Python 解释器。</p>
<p>构建源发行版以在没有 wheel 时确定包元数据需要 Python 解释器。</p>
<p>解释器也用于确定默认的最低 Python 版本，除非提供了 <code>--python-version</code>。</p>
<p>此选项遵循 <code>UV_PYTHON</code>，但当通过环境变量设置时，它会被 <code>--python-version</code> 覆盖。</p>
<p>查看 <a href="#uv-python">uv python</a> 了解 Python 发现和受支持请求格式的详细信息。</p>
</dd><dt id="uv-pip-compile--python-platform"><a href="#uv-pip-compile--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其解析要求的平台。</p>
<p>表示为"目标三元组"，一个字符串，根据其 CPU、供应商和操作系统名称描述目标平台，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标是 macOS（Darwin）时，默认最低版本是 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标是 iOS 时，默认最低版本是 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标是 Android 时，默认最低 Android API 级别是 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>:  <code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>:  <code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>:  <code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>:  64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>:  ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>:  32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>:  x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>:  基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>:  x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>:  ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>:  ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>:  <code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>:  RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>:  <code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>:  <code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>:  <code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>:  <code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>:  <code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>:  <code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>:  <code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>:  <code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>:  <code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>:  <code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>:  <code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>:  <code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>:  <code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>:  <code>manylinux2014</code> 平台的 ARM64 目标。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>:  <code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>:  <code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>:  <code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>:  <code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>:  <code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>:  <code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>:  <code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>:  <code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>:  <code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>:  <code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>:  <code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>:  <code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>:  ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>:  <code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>:  使用 Pyodide 2024 平台的 wasm32 目标。用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>:  iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>:  iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>:  iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-pip-compile--python-version"><a href="#uv-pip-compile--python-version"><code>--python-version</code></a> <i>python-version</i></dt><dd><p>用于解析的 Python 版本。</p>
<p>例如，<code>3.8</code> 或 <code>3.8.17</code>。</p>
<p>默认为用于解析的 Python 解释器的版本。</p>
<p>定义解析的要求必须支持的最低 Python 版本。</p>
<p>如果省略了补丁版本，则假定为最低补丁版本。例如，<code>3.8</code> 映射到 <code>3.8.0</code>。</p>
</dd><dt id="uv-pip-compile--quiet"><a href="#uv-pip-compile--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-compile--refresh"><a href="#uv-pip-compile--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-pip-compile--refresh-package"><a href="#uv-pip-compile--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-pip-compile--resolution"><a href="#uv-pip-compile--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>为给定包要求在不同兼容版本之间选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可以通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-pip-compile--system"><a href="#uv-pip-compile--system"><code>--system</code></a></dt><dd><p>将包安装到系统 Python 环境中。</p>
<p>默认情况下，uv 使用当前工作目录或任何父目录中的虚拟环境，回退到在 <code>PATH</code> 中搜索 Python 可执行文件。<code>--system</code> 选项指示 uv 避免使用虚拟环境 Python 并将其搜索限制在系统路径中。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-compile--torch-backend"><a href="#uv-pip-compile--torch-backend"><code>--torch-backend</code></a> <i>torch-backend</i></dt><dd><p>在获取 PyTorch 生态系统中的包时使用的后端（例如 <code>cpu</code>、<code>cu126</code> 或 <code>auto</code>）。</p>
<p>设置后，uv 将忽略为 PyTorch 生态系统中的包配置的索引 URL，而是使用定义的后端。</p>
<p>例如，当设置为 <code>cpu</code> 时，uv 将使用仅 CPU 的 PyTorch 索引；当设置为 <code>cu126</code> 时，uv 将使用 CUDA 12.6 的 PyTorch 索引。</p>
<p><code>auto</code> 模式将尝试根据当前安装的 CUDA 驱动程序检测适当的 PyTorch 索引。</p>
<p>此选项处于预览状态，可能在未来的任何版本中更改。</p>
<p>也可以通过 <code>UV_TORCH_BACKEND</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>auto</code>:  根据操作系统和 CUDA 驱动程序版本选择适当的 PyTorch 索引</li>
<li><code>cpu</code>:  使用仅 CPU 的 PyTorch 索引</li>
<li><code>cu130</code>:  使用 CUDA 13.0 的 PyTorch 索引</li>
<li><code>cu129</code>:  使用 CUDA 12.9 的 PyTorch 索引</li>
<li><code>cu128</code>:  使用 CUDA 12.8 的 PyTorch 索引</li>
<li><code>cu126</code>:  使用 CUDA 12.6 的 PyTorch 索引</li>
<li><code>cu125</code>:  使用 CUDA 12.5 的 PyTorch 索引</li>
<li><code>cu124</code>:  使用 CUDA 12.4 的 PyTorch 索引</li>
<li><code>cu123</code>:  使用 CUDA 12.3 的 PyTorch 索引</li>
<li><code>cu122</code>:  使用 CUDA 12.2 的 PyTorch 索引</li>
<li><code>cu121</code>:  使用 CUDA 12.1 的 PyTorch 索引</li>
<li><code>cu120</code>:  使用 CUDA 12.0 的 PyTorch 索引</li>
<li><code>cu118</code>:  使用 CUDA 11.8 的 PyTorch 索引</li>
<li><code>cu117</code>:  使用 CUDA 11.7 的 PyTorch 索引</li>
<li><code>cu116</code>:  使用 CUDA 11.6 的 PyTorch 索引</li>
<li><code>cu115</code>:  使用 CUDA 11.5 的 PyTorch 索引</li>
<li><code>cu114</code>:  使用 CUDA 11.4 的 PyTorch 索引</li>
<li><code>cu113</code>:  使用 CUDA 11.3 的 PyTorch 索引</li>
<li><code>cu112</code>:  使用 CUDA 11.2 的 PyTorch 索引</li>
<li><code>cu111</code>:  使用 CUDA 11.1 的 PyTorch 索引</li>
<li><code>cu110</code>:  使用 CUDA 11.0 的 PyTorch 索引</li>
<li><code>cu102</code>:  使用 CUDA 10.2 的 PyTorch 索引</li>
<li><code>cu101</code>:  使用 CUDA 10.1 的 PyTorch 索引</li>
<li><code>cu100</code>:  使用 CUDA 10.0 的 PyTorch 索引</li>
<li><code>cu92</code>:  使用 CUDA 9.2 的 PyTorch 索引</li>
<li><code>cu91</code>:  使用 CUDA 9.1 的 PyTorch 索引</li>
<li><code>cu90</code>:  使用 CUDA 9.0 的 PyTorch 索引</li>
<li><code>cu80</code>:  使用 CUDA 8.0 的 PyTorch 索引</li>
<li><code>rocm6.3</code>:  使用 ROCm 6.3 的 PyTorch 索引</li>
<li><code>rocm6.2.4</code>:  使用 ROCm 6.2.4 的 PyTorch 索引</li>
<li><code>rocm6.2</code>:  使用 ROCm 6.2 的 PyTorch 索引</li>
<li><code>rocm6.1</code>:  使用 ROCm 6.1 的 PyTorch 索引</li>
<li><code>rocm6.0</code>:  使用 ROCm 6.0 的 PyTorch 索引</li>
<li><code>rocm5.7</code>:  使用 ROCm 5.7 的 PyTorch 索引</li>
<li><code>rocm5.6</code>:  使用 ROCm 5.6 的 PyTorch 索引</li>
<li><code>rocm5.5</code>:  使用 ROCm 5.5 的 PyTorch 索引</li>
<li><code>rocm5.4.2</code>:  使用 ROCm 5.4.2 的 PyTorch 索引</li>
<li><code>rocm5.4</code>:  使用 ROCm 5.4 的 PyTorch 索引</li>
<li><code>rocm5.3</code>:  使用 ROCm 5.3 的 PyTorch 索引</li>
<li><code>rocm5.2</code>:  使用 ROCm 5.2 的 PyTorch 索引</li>
<li><code>rocm5.1.1</code>:  使用 ROCm 5.1.1 的 PyTorch 索引</li>
<li><code>rocm4.2</code>:  使用 ROCm 4.2 的 PyTorch 索引</li>
<li><code>rocm4.1</code>:  使用 ROCm 4.1 的 PyTorch 索引</li>
<li><code>rocm4.0.1</code>:  Use the PyTorch index for ROCm 4.0.1</li>
<li><code>rocm4.0.1</code>: 使用 ROCm 4.0.1 的 PyTorch 索引</li>
<li><code>xpu</code>: 使用 Intel XPU 的 PyTorch 索引</li>
</ul></dd><dt id="uv-pip-compile--universal"><a href="#uv-pip-compile--universal"><code>--universal</code></a></dt><dd><p>执行通用解析，尝试生成一个兼容所有操作系统、架构和 Python 实现的单一 <code>requirements.txt</code> 输出文件。</p>
<p>在通用模式下，当前 Python 版本（或用户提供的 <code>--python-version</code>）将被视为下限。例如，<code>--universal --python-version 3.7</code> 将为 Python 3.7 及更高版本生成通用解析。</p>
<p>隐含 <code>--no-strip-markers</code>。</p>
</dd><dt id="uv-pip-compile--upgrade"><a href="#uv-pip-compile--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh</code></p>
</dd><dt id="uv-pip-compile--upgrade-package"><a href="#uv-pip-compile--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包的升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-pip-compile--verbose"><a href="#uv-pip-compile--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip sync

使用 `requirements.txt` 或 `pylock.toml` 文件同步环境。

同步环境时，任何未在 `requirements.txt` 或 `pylock.toml` 文件中列出的包将被移除。要保留额外的包，请改用 `uv pip install`。

输入文件假定为 `pip compile` 或 `uv export` 操作的输出，其中将包含所有传递依赖项。如果文件中不存在传递依赖项，则不会安装它们。使用 `--strict` 选项在缺少任何传递依赖项时发出警告。

<h3 class="cli-reference">用法</h3>

```
uv pip sync [OPTIONS] <SRC_FILE>...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-pip-sync--src_file"><a href="#uv-pip-sync--src_file"<code>SRC_FILE</code></a></dt><dd><p>包含给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、带有内联元数据的 <code>.py</code> 文件、<code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code>。</p>
<p>如果提供了 <code>pyproject.toml</code>、<code>setup.py</code> 或 <code>setup.cfg</code> 文件，uv 将提取相关项目的要求。</p>
<p>如果提供 <code>-</code>，则将从标准输入读取要求。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-sync--all-extras"><a href="#uv-pip-sync--all-extras"><code>--all-extras</code></a></dt><dd><p>包含所有可选依赖项。</p>
<p>仅适用于 <code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code> 源。</p>
</dd><dt id="uv-pip-sync--allow-empty-requirements"><a href="#uv-pip-sync--allow-empty-requirements"><code>--allow-empty-requirements</code></a></dt><dd><p>允许同步空要求，这将清除环境中的所有包</p>
</dd><dt id="uv-pip-sync--allow-insecure-host"><a href="#uv-pip-sync--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它绕过 SSL 验证，可能使您面临中间人攻击。</p>
<p>也可以使用 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--break-system-packages"><a href="#uv-pip-sync--break-system-packages"><code>--break-system-packages</code></a></dt><dd><p>允许 uv 修改 <code>EXTERNALLY-MANAGED</code> Python 安装。</p>
<p>警告：<code>--break-system-packages</code> 旨在用于持续集成（CI）环境，当安装到由外部包管理器（如 <code>apt</code>）管理的 Python 安装时。应谨慎使用，因为此类 Python 安装明确建议不要由其他包管理器（如 uv 或 <code>pip</code>）修改。</p>
<p>也可以使用 <code>UV_BREAK_SYSTEM_PACKAGES</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--build-constraints"><a href="#uv-pip-sync--build-constraints"><code>--build-constraints</code></a>, <code>--build-constraint</code>, <code>-b</code> <i>build-constraints</i></dt><dd><p>在构建源分发时，使用给定的要求文件约束构建依赖项。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的要求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>也可以使用 <code>UV_BUILD_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--cache-dir"><a href="#uv-pip-sync--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以使用 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--color"><a href="#uv-pip-sync--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测颜色支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>: 仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>: 无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>: 禁用彩色输出</li>
</ul></dd><dt id="uv-pip-sync--compile-bytecode"><a href="#uv-pip-sync--compile-bytecode"><code>--compile-bytecode</code></a>, <code>--compile</code></dt><dd><p>安装后将 Python 文件编译为字节码。</p>
<p>默认情况下，uv 不会将 Python（<code>.py</code>）文件编译为字节码（<code>__pycache__/*.pyc</code>）；相反，编译在首次导入模块时延迟执行。对于启动时间关键的使用场景，如 CLI 应用程序和 Docker 容器，可以启用此选项，以用更长的安装时间换取更快的启动时间。</p>
<p>启用后，uv 将处理整个 site-packages 目录（包括当前操作未修改的包）以确保一致性。与 pip 类似，它也会忽略错误。</p>
<p>也可以使用 <code>UV_COMPILE_BYTECODE</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--config-file"><a href="#uv-pip-sync--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以使用 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--config-setting"><a href="#uv-pip-sync--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-pip-sync--config-settings-package"><a href="#uv-pip-sync--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-pip-sync--constraints"><a href="#uv-pip-sync--constraints"><code>--constraints</code></a>, <code>--constraint</code>, <code>-c</code> <i>constraints</i></dt><dd><p>使用给定的要求文件约束版本。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的要求的<em>版本</em>。但是，在约束文件中包含包<em>不会</em>触发该包的安装。</p>
<p>这相当于 pip 的 <code>--constraint</code> 选项。</p>
<p>也可以使用 <code>UV_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--default-index"><a href="#uv-pip-sync--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以使用 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--directory"><a href="#uv-pip-sync--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>有关仅更改项目根目录的信息，请参见 <code>--project</code>。</p>
<p>也可以使用 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--dry-run"><a href="#uv-pip-sync--dry-run"><code>--dry-run</code></a></dt><dd><p>执行试运行，即不实际安装任何内容，但解析依赖关系并打印结果计划</p>
</dd><dt id="uv-pip-sync--exclude-newer"><a href="#uv-pip-sync--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以使用 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--exclude-newer-package"><a href="#uv-pip-sync--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-pip-sync--extra"><a href="#uv-pip-sync--extra"><code>--extra</code></a> <i>extra</i></dt><dd><p>包含指定额外名称的可选依赖项；可以多次提供。</p>
<p>仅适用于 <code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code> 源。</p>
</dd><dt id="uv-pip-sync--extra-index-url"><a href="#uv-pip-sync--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：改用 <code>--index</code>）除了 <code>--index-url</code> 之外，要使用的额外包索引 URL。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以使用 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--find-links"><a href="#uv-pip-sync--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的位置之外，搜索候选分发的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源分发（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含符合上述格式的包文件的平面链接列表。</p>
<p>也可以使用 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--group"><a href="#uv-pip-sync--group"><code>--group</code></a> <i>group</i></dt><dd><p>从 <code>pylock.toml</code> 或 <code>pyproject.toml</code> 安装指定的依赖组。</p>
<p>如果未提供路径，则使用工作目录中的 <code>pylock.toml</code> 或 <code>pyproject.toml</code>。</p>
<p>可以多次提供。</p>
</dd><dt id="uv-pip-sync--help"><a href="#uv-pip-sync--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-sync--index"><a href="#uv-pip-sync--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>不支持将索引名称作为值。相对路径必须使用 Unix 上的 <code>./</code> 或 <code>../</code>，或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 来与索引名称进行区分。</p>
<p>也可以使用 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--index-strategy"><a href="#uv-pip-sync--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>针对多个索引 URL 进行解析时使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这可以防止"依赖混淆"攻击，即攻击者可以将恶意包以相同名称上传到备用索引。</p>
<p>也可以使用 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>: 仅使用第一个返回给定包名称匹配结果的索引中的结果</li>
<li><code>unsafe-first-match</code>: 在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>: 在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-pip-sync--index-url"><a href="#uv-pip-sync--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：改用 <code>--default-index</code>）Python 包索引的 URL（默认：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503（简单存储库 API）的存储库，或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以使用 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--keyring-provider"><a href="#uv-pip-sync--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以使用 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>: 不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>: 使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-pip-sync--link-mode"><a href="#uv-pip-sync--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过删除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以使用 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>: 从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>: 从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>: 从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>: 从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-pip-sync--managed-python"><a href="#uv-pip-sync--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以使用 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--native-tls"><a href="#uv-pip-sync--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以使用 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-allow-empty-requirements"><a href="#uv-pip-sync--no-allow-empty-requirements"><code>--no-allow-empty-requirements</code></a></dt><dt id="uv-pip-sync--no-binary"><a href="#uv-pip-sync--no-binary"><code>--no-binary</code></a> <i>no-binary</i></dt><dd><p>不安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>可以提供多个包。使用 <code>:all:</code> 禁用所有包的二进制文件。使用 <code>:none:</code> 清除先前指定的包。</p>
</dd><dt id="uv-pip-sync--no-break-system-packages"><a href="#uv-pip-sync--no-break-system-packages"><code>--no-break-system-packages</code></a></dt><dt id="uv-pip-sync--no-build"><a href="#uv-pip-sync--no-build"><code>--no-build</code></a></dt><dd><p>不构建源分发。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源分发的缓存 wheel，但需要构建分发的操作将退出并报错。</p>
<p><code>--only-binary :all:</code> 的别名。</p>
</dd><dt id="uv-pip-sync--no-build-isolation"><a href="#uv-pip-sync--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源分发时禁用隔离。</p>
<p>假定 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以使用 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-cache"><a href="#uv-pip-sync--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免从缓存读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以使用 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-index"><a href="#uv-pip-sync--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-pip-sync--no-managed-python"><a href="#uv-pip-sync--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以使用 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-progress"><a href="#uv-pip-sync--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可以使用 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-python-downloads"><a href="#uv-pip-sync--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-sync--no-sources"><a href="#uv-pip-sync--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可以使用 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--no-verify-hashes"><a href="#uv-pip-sync--no-verify-hashes"><code>--no-verify-hashes</code></a></dt><dd><p>禁用要求文件中哈希的验证。</p>
<p>默认情况下，uv 将验证要求文件中任何可用的哈希，但不会要求所有要求都有关联的哈希。要强制进行哈希验证，请使用 <code>--require-hashes</code>。</p>
<p>也可以使用 <code>UV_NO_VERIFY_HASHES</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--offline"><a href="#uv-pip-sync--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以使用 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--only-binary"><a href="#uv-pip-sync--only-binary"><code>--only-binary</code></a> <i>only-binary</i></dt><dd><p>仅使用预构建的 wheel；不构建源分发。</p>
<p>启用后，解析将不会从给定的包运行代码。将重用已构建源分发的缓存 wheel，但需要构建分发的操作将退出并报错。</p>
<p>可以提供多个包。使用 <code>:all:</code> 禁用所有包的二进制文件。使用 <code>:none:</code> 清除先前指定的包。</p>
</dd><dt id="uv-pip-sync--prefix"><a href="#uv-pip-sync--prefix"><code>--prefix</code></a> <i>prefix</i></dt><dd><p>将包安装到指定目录下的 <code>lib</code>、<code>bin</code> 和其他顶级文件夹中，就像该位置存在虚拟环境一样。</p>
<p>通常，建议使用 <code>--python</code> 安装到备用环境，因为通过 <code>--prefix</code> 安装的脚本和其他工件将引用安装解释器，而不是添加到 <code>--prefix</code> 目录的任何解释器，从而使它们不可移植。</p>
<p>与其他安装操作不同，此命令不需要发现现有的 Python 环境，并且仅搜索用于包解析的 Python 解释器。如果找不到合适的 Python 解释器，uv 将安装一个。要禁用此功能，请添加 <code>--no-python-downloads</code>。</p>
</dd><dt id="uv-pip-sync--project"><a href="#uv-pip-sync--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录进行解析。</p>
<p>有关完全更改工作目录的信息，请参见 <code>--directory</code>。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以使用 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--python"><a href="#uv-pip-sync--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应安装包的 Python 解释器。</p>
<p>默认情况下，同步需要虚拟环境。可以提供备用 Python 的路径，但仅建议在持续集成（CI）环境中使用，并且应谨慎使用，因为它可以修改系统 Python 安装。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参见 <a href="#uv-python">uv python</a>。</p>
<p>也可以使用 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--python-platform"><a href="#uv-pip-sync--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应为其安装要求的平台。</p>
<p>表示为"目标三元组"，一个描述目标平台 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标为 macOS（Darwin）时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>警告：指定后，uv 将选择与<em>目标</em>平台兼容的 wheel；因此，安装的分发版可能与<em>当前</em>平台不兼容。相反，任何从源代码构建的分发版可能与<em>目标</em>平台不兼容，因为它们将为<em>当前</em>平台构建。<code>--python-platform</code> 选项适用于高级用例。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>: <code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>: <code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>: <code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>: 64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>: ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>: 32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>: x86 Linux 目标。等效于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>: 基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>: x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>: ARM64 Linux 目标。等效于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>: ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>: <code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>: RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>: <code>x86_64</code> 目标，用于 <code>manylinux2014</code> 平台。等效于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_17</code> 平台</li>
<li><code>x86_64-manylinux_2_28</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_28</code> 平台</li>
<li><code>x86_64-manylinux_2_31</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_31</code> 平台</li>
<li><code>x86_64-manylinux_2_32</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_32</code> 平台</li>
<li><code>x86_64-manylinux_2_33</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_33</code> 平台</li>
<li><code>x86_64-manylinux_2_34</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_34</code> 平台</li>
<li><code>x86_64-manylinux_2_35</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_35</code> 平台</li>
<li><code>x86_64-manylinux_2_36</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_36</code> 平台</li>
<li><code>x86_64-manylinux_2_37</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_37</code> 平台</li>
<li><code>x86_64-manylinux_2_38</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_38</code> 平台</li>
<li><code>x86_64-manylinux_2_39</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_39</code> 平台</li>
<li><code>x86_64-manylinux_2_40</code>: <code>x86_64</code> 目标，用于 <code>manylinux_2_40</code> 平台</li>
<li><code>aarch64-manylinux2014</code>: ARM64 目标，用于 <code>manylinux2014</code> 平台。等效于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>: ARM64 目标，用于 <code>manylinux_2_17</code> 平台</li>
<li><code>aarch64-manylinux_2_28</code>: ARM64 目标，用于 <code>manylinux_2_28</code> 平台</li>
<li><code>aarch64-manylinux_2_31</code>: ARM64 目标，用于 <code>manylinux_2_31</code> 平台</li>
<li><code>aarch64-manylinux_2_32</code>: ARM64 目标，用于 <code>manylinux_2_32</code> 平台</li>
<li><code>aarch64-manylinux_2_33</code>: ARM64 目标，用于 <code>manylinux_2_33</code> 平台</li>
<li><code>aarch64-manylinux_2_34</code>: ARM64 目标，用于 <code>manylinux_2_34</code> 平台</li>
<li><code>aarch64-manylinux_2_35</code>: ARM64 目标，用于 <code>manylinux_2_35</code> 平台</li>
<li><code>aarch64-manylinux_2_36</code>: ARM64 目标，用于 <code>manylinux_2_36</code> 平台</li>
<li><code>aarch64-manylinux_2_37</code>: ARM64 目标，用于 <code>manylinux_2_37</code> 平台</li>
<li><code>aarch64-manylinux_2_38</code>: ARM64 目标，用于 <code>manylinux_2_38</code> 平台</li>
<li><code>aarch64-manylinux_2_39</code>: ARM64 目标，用于 <code>manylinux_2_39</code> 平台</li>
<li><code>aarch64-manylinux_2_40</code>: ARM64 目标，用于 <code>manylinux_2_40</code> 平台</li>
<li><code>aarch64-linux-android</code>: ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>: <code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>: 使用 Pyodide 2024 平台的 wasm32 目标。适用于 Python 3.12</li>
<li><code>arm64-apple-ios</code>: iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>: iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>: iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-pip-sync--python-version"><a href="#uv-pip-sync--python-version"><code>--python-version</code></a> <i>python-version</i></dt><dd><p>要求应支持的最低 Python 版本（例如 <code>3.7</code> 或 <code>3.7.9</code>）。</p>
<p>如果省略了补丁版本，则假定为最低补丁版本。例如，<code>3.7</code> 映射到 <code>3.7.0</code>。</p>
</dd><dt id="uv-pip-sync--quiet"><a href="#uv-pip-sync--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向标准输出写入任何输出。</p>
</dd><dt id="uv-pip-sync--refresh"><a href="#uv-pip-sync--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存的数据</p>
</dd><dt id="uv-pip-sync--refresh-package"><a href="#uv-pip-sync--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-pip-sync--reinstall"><a href="#uv-pip-sync--reinstall"><code>--reinstall</code></a>, <code>--force-reinstall</code></dt><dd><p>重新安装所有包，无论它们是否已安装。隐含 <code>--refresh</code></p>
</dd><dt id="uv-pip-sync--reinstall-package"><a href="#uv-pip-sync--reinstall-package"><code>--reinstall-package</code></a> <i>reinstall-package</i></dt><dd><p>重新安装特定包，无论它是否已安装。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-pip-sync--require-hashes"><a href="#uv-pip-sync--require-hashes"><code>--require-hashes</code></a></dt><dd><p>要求每个要求都有匹配的哈希。</p>
<p>默认情况下，uv 将验证要求文件中任何可用的哈希，但不会要求所有要求都有关联的哈希。</p>
<p>当启用 <code>--require-hashes</code> 时，<em>所有</em>要求必须包含一个哈希或一组哈希，并且<em>所有</em>要求必须要么固定到确切版本（例如 <code>==1.0.0</code>），要么通过直接 URL 指定。</p>
<p>哈希检查模式引入了许多额外的约束：</p>
<ul>
<li>不支持 Git 依赖项。- 不支持可编辑安装。- 不支持本地依赖项，除非它们指向特定的 wheel（<code>.whl</code>）或源存档（<code>.zip</code>、<code>.tar.gz</code>），而不是目录。</li>
</ul>
<p>也可以使用 <code>UV_REQUIRE_HASHES</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--strict"><a href="#uv-pip-sync--strict"><code>--strict</code></a></dt><dd><p>完成安装后验证 Python 环境，以检测具有缺失依赖项或其他问题的包</p>
</dd><dt id="uv-pip-sync--system"><a href="#uv-pip-sync--system"><code>--system</code></a></dt><dd><p>将包安装到系统 Python 环境中。</p>
<p>默认情况下，uv 安装到当前工作目录或任何父目录中的虚拟环境。<code>--system</code> 选项指示 uv 改用系统 <code>PATH</code> 中找到的第一个 Python。</p>
<p>警告：<code>--system</code> 旨在用于持续集成（CI）环境，应谨慎使用，因为它可以修改系统 Python 安装。</p>
<p>也可以使用 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-sync--target"><a href="#uv-pip-sync--target"><code>--target</code></a> <i>target</i></dt><dd><p>将包安装到指定目录，而不是虚拟或系统 Python 环境中。包将安装在目录的顶层。</p>
<p>与其他安装操作不同，此命令不需要发现现有的 Python 环境，并且仅搜索用于包解析的 Python 解释器。如果找不到合适的 Python 解释器，uv 将安装一个。要禁用此功能，请添加 <code>--no-python-downloads</code>。</p>
</dd><dt id="uv-pip-sync--torch-backend"><a href="#uv-pip-sync--torch-backend"><code>--torch-backend</code></a> <i>torch-backend</i></dt><dd><p>获取 PyTorch 生态系统中的包时使用的后端（例如 <code>cpu</code>、<code>cu126</code> 或 <code>auto</code>）。</p>
<p>设置后，uv 将忽略为 PyTorch 生态系统中的包配置的索引 URL，并将改用定义的后端。</p>
<p>例如，当设置为 <code>cpu</code> 时，uv 将使用仅 CPU 的 PyTorch 索引；当设置为 <code>cu126</code> 时，uv 将使用 CUDA 12.6 的 PyTorch 索引。</p>
<p><code>auto</code> 模式将尝试根据当前安装的 CUDA 驱动程序检测适当的 PyTorch 索引。</p>
<p>此选项处于预览状态，可能在未来的任何版本中更改。</p>
<p>也可以使用 <code>UV_TORCH_BACKEND</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>auto</code>: 根据操作系统和 CUDA 驱动程序版本选择适当的 PyTorch 索引</li>
<li><code>cpu</code>: 使用仅 CPU 的 PyTorch 索引</li>
<li><code>cu130</code>: 使用 CUDA 13.0 的 PyTorch 索引</li>
<li><code>cu129</code>: 使用 CUDA 12.9 的 PyTorch 索引</li>
<li><code>cu128</code>: 使用 CUDA 12.8 的 PyTorch 索引</li>
<li><code>cu126</code>: 使用 CUDA 12.6 的 PyTorch 索引</li>
<li><code>cu125</code>: 使用 CUDA 12.5 的 PyTorch 索引</li>
<li><code>cu124</code>: 使用 CUDA 12.4 的 PyTorch 索引</li>
<li><code>cu123</code>: 使用 CUDA 12.3 的 PyTorch 索引</li>
<li><code>cu122</code>: 使用 CUDA 12.2 的 PyTorch 索引</li>
<li><code>cu121</code>: 使用 CUDA 12.1 的 PyTorch 索引</li>
<li><code>cu120</code>: 使用 CUDA 12.0 的 PyTorch 索引</li>
<li><code>cu118</code>: 使用 CUDA 11.8 的 PyTorch 索引</li>
<li><code>cu117</code>: 使用 CUDA 11.7 的 PyTorch 索引</li>
<li><code>cu116</code>: 使用 CUDA 11.6 的 PyTorch 索引</li>
<li><code>cu115</code>: 使用 CUDA 11.5 的 PyTorch 索引</li>
<li><code>cu114</code>: 使用 CUDA 11.4 的 PyTorch 索引</li>
<li><code>cu113</code>: 使用 CUDA 11.3 的 PyTorch 索引</li>
<li><code>cu112</code>: 使用 CUDA 11.2 的 PyTorch 索引</li>
<li><code>cu111</code>: 使用 CUDA 11.1 的 PyTorch 索引</li>
<li><code>cu110</code>: 使用 CUDA 11.0 的 PyTorch 索引</li>
<li><code>cu102</code>: 使用 CUDA 10.2 的 PyTorch 索引</li>
<li><code>cu101</code>: 使用 CUDA 10.1 的 PyTorch 索引</li>
<li><code>cu100</code>: 使用 CUDA 10.0 的 PyTorch 索引</li>
<li><code>cu92</code>: 使用 CUDA 9.2 的 PyTorch 索引</li>
<li><code>cu91</code>: 使用 CUDA 9.1 的 PyTorch 索引</li>
<li><code>cu90</code>: 使用 CUDA 9.0 的 PyTorch 索引</li>
<li><code>cu80</code>: 使用 CUDA 8.0 的 PyTorch 索引</li>
<li><code>rocm6.3</code>: 使用 ROCm 6.3 的 PyTorch 索引</li>
<li><code>rocm6.2.4</code>: 使用 ROCm 6.2.4 的 PyTorch 索引</li>
<li><code>rocm6.2</code>: 使用 ROCm 6.2 的 PyTorch 索引</li>
<li><code>rocm6.1</code>: 使用 ROCm 6.1 的 PyTorch 索引</li>
<li><code>rocm6.0</code>: 使用 ROCm 6.0 的 PyTorch 索引</li>
<li><code>rocm5.7</code>: 使用 ROCm 5.7 的 PyTorch 索引</li>
<li><code>rocm5.6</code>: 使用 ROCm 5.6 的 PyTorch 索引</li>
<li><code>rocm5.5</code>: 使用 ROCm 5.5 的 PyTorch 索引</li>
<li><code>rocm5.4.2</code>: 使用 ROCm 5.4.2 的 PyTorch 索引</li>
<li><code>rocm5.4</code>: 使用 ROCm 5.4 的 PyTorch 索引</li>
<li><code>rocm5.3</code>: 使用 ROCm 5.3 的 PyTorch 索引</li>
<li><code>rocm5.2</code>: 使用 ROCm 5.2 的 PyTorch 索引</li>
<li><code>rocm5.1.1</code>: 使用 ROCm 5.1.1 的 PyTorch 索引</li>
<li><code>rocm4.2</code>: 使用 ROCm 4.2 的 PyTorch 索引</li>
<li><code>rocm4.1</code>: 使用 ROCm 4.1 的 PyTorch 索引</li>
<li><code>rocm4.0.1</code>: 使用 ROCm 4.0.1 的 PyTorch 索引</li>
<li><code>xpu</code>: 使用 Intel XPU 的 PyTorch 索引</li>
</ul></dd><dt id="uv-pip-sync--verbose"><a href="#uv-pip-sync--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度的日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip uninstall

从环境中卸载包

<h3 class="cli-reference">用法</h3>

```
uv pip uninstall [OPTIONS] <PACKAGE|--requirements <REQUIREMENTS>>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-pip-uninstall--package"><a href="#uv-pip-uninstall--package"<code>PACKAGE</code></a></dt><dd><p>卸载所有列出的包</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-uninstall--allow-insecure-host"><a href="#uv-pip-uninstall--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--break-system-packages"><a href="#uv-pip-uninstall--break-system-packages"><code>--break-system-packages</code></a></dt><dd><p>允许 uv 修改 <code>EXTERNALLY-MANAGED</code> Python 安装。</p>
<p>警告：<code>--break-system-packages</code> 旨在用于持续集成（CI）环境中，当安装到由外部包管理器（如 <code>apt</code>）管理的 Python 安装时。应谨慎使用，因为此类 Python 安装明确建议不要由其他包管理器（如 uv 或 <code>pip</code>）进行修改。</p>
<p>也可以通过 <code>UV_BREAK_SYSTEM_PACKAGES</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--cache-dir"><a href="#uv-pip-uninstall--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--color"><a href="#uv-pip-uninstall--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-uninstall--config-file"><a href="#uv-pip-uninstall--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--directory"><a href="#uv-pip-uninstall--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--dry-run"><a href="#uv-pip-uninstall--dry-run"><code>--dry-run</code></a></dt><dd><p>执行试运行，即不实际卸载任何内容，但打印最终计划</p>
</dd><dt id="uv-pip-uninstall--help"><a href="#uv-pip-uninstall--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-uninstall--keyring-provider"><a href="#uv-pip-uninstall--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行远程需求文件的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-pip-uninstall--managed-python"><a href="#uv-pip-uninstall--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--native-tls"><a href="#uv-pip-uninstall--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--no-break-system-packages"><a href="#uv-pip-uninstall--no-break-system-packages"><code>--no-break-system-packages</code></a></dt><dt id="uv-pip-uninstall--no-cache"><a href="#uv-pip-uninstall--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--no-config"><a href="#uv-pip-uninstall--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--no-managed-python"><a href="#uv-pip-uninstall--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--no-progress"><a href="#uv-pip-uninstall--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--no-python-downloads"><a href="#uv-pip-uninstall--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-uninstall--offline"><a href="#uv-pip-uninstall--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--prefix"><a href="#uv-pip-uninstall--prefix"><code>--prefix</code></a> <i>prefix</i></dt><dd><p>从指定的 <code>--prefix</code> 目录卸载包</p>
</dd><dt id="uv-pip-uninstall--project"><a href="#uv-pip-uninstall--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--python"><a href="#uv-pip-uninstall--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应从中卸载包的 Python 解释器。</p>
<p>默认情况下，卸载需要虚拟环境。可以提供备用 Python 的路径，但仅建议在持续集成（CI）环境中使用，并应谨慎使用，因为它可以修改系统 Python 安装。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--quiet"><a href="#uv-pip-uninstall--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-uninstall--requirements"><a href="#uv-pip-uninstall--requirements"><code>--requirements</code></a>, <code>--requirement</code>, <code>-r</code> <i>requirements</i></dt><dd><p>卸载给定文件中列出的包。</p>
<p>支持以下格式：<code>requirements.txt</code>、带有内联元数据的 <code>.py</code> 文件、<code>pylock.toml</code>、<code>pyproject.toml</code>、<code>setup.py</code> 和 <code>setup.cfg</code>。</p>
</dd><dt id="uv-pip-uninstall--system"><a href="#uv-pip-uninstall--system"><code>--system</code></a></dt><dd><p>使用系统 Python 卸载包。</p>
<p>默认情况下，uv 从当前工作目录或任何父目录中的虚拟环境卸载。<code>--system</code> 选项指示 uv 改为使用系统 <code>PATH</code> 中找到的第一个 Python。</p>
<p>警告：<code>--system</code> 旨在用于持续集成（CI）环境，应谨慎使用，因为它可以修改系统 Python 安装。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-uninstall--target"><a href="#uv-pip-uninstall--target"><code>--target</code></a> <i>target</i></dt><dd><p>从指定的 <code>--target</code> 目录卸载包</p>
</dd><dt id="uv-pip-uninstall--verbose"><a href="#uv-pip-uninstall--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip freeze

以需求格式列出环境中安装的包

<h3 class="cli-reference">用法</h3>

```
uv pip freeze [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-freeze--allow-insecure-host"><a href="#uv-pip-freeze--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--cache-dir"><a href="#uv-pip-freeze--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--color"><a href="#uv-pip-freeze--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-freeze--config-file"><a href="#uv-pip-freeze--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--directory"><a href="#uv-pip-freeze--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--exclude-editable"><a href="#uv-pip-freeze--exclude-editable"><code>--exclude-editable</code></a></dt><dd><p>从输出中排除任何可编辑的包</p>
</dd><dt id="uv-pip-freeze--help"><a href="#uv-pip-freeze--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-freeze--managed-python"><a href="#uv-pip-freeze--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--native-tls"><a href="#uv-pip-freeze--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--no-cache"><a href="#uv-pip-freeze--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--no-config"><a href="#uv-pip-freeze--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--no-managed-python"><a href="#uv-pip-freeze--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--no-progress"><a href="#uv-pip-freeze--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--no-python-downloads"><a href="#uv-pip-freeze--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-freeze--offline"><a href="#uv-pip-freeze--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--path"><a href="#uv-pip-freeze--path"><code>--path</code></a> <i>paths</i></dt><dd><p>限制到指定的安装路径以列出包（可以多次使用）</p>
</dd><dt id="uv-pip-freeze--project"><a href="#uv-pip-freeze--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--python"><a href="#uv-pip-freeze--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应列出其包的 Python 解释器。</p>
<p>默认情况下，uv 在虚拟环境中列出包，但如果未找到虚拟环境，将显示系统 Python 环境中的包。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--quiet"><a href="#uv-pip-freeze--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-freeze--strict"><a href="#uv-pip-freeze--strict"><code>--strict</code></a></dt><dd><p>验证 Python 环境，以检测具有缺失依赖项和其他问题的包</p>
</dd><dt id="uv-pip-freeze--system"><a href="#uv-pip-freeze--system"><code>--system</code></a></dt><dd><p>列出系统 Python 环境中的包。</p>
<p>禁用虚拟环境的发现。</p>
<p>有关 Python 发现的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-freeze--verbose"><a href="#uv-pip-freeze--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip list

以表格格式列出环境中安装的包

<h3 class="cli-reference">用法</h3>

```
uv pip list [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-list--allow-insecure-host"><a href="#uv-pip-list--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-list--cache-dir"><a href="#uv-pip-list--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-list--color"><a href="#uv-pip-list--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-list--config-file"><a href="#uv-pip-list--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-list--default-index"><a href="#uv-pip-list--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-list--directory"><a href="#uv-pip-list--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-list--editable"><a href="#uv-pip-list--editable"><code>--editable</code></a>, <code>-e</code></dt><dd><p>仅包含可编辑项目</p>
</dd><dt id="uv-pip-list--exclude"><a href="#uv-pip-list--exclude"><code>--exclude</code></a> <i>exclude</i></dt><dd><p>从输出中排除指定的包</p>
</dd><dt id="uv-pip-list--exclude-editable"><a href="#uv-pip-list--exclude-editable"><code>--exclude-editable</code></a></dt><dd><p>从输出中排除任何可编辑的包</p>
</dd><dt id="uv-pip-list--exclude-newer"><a href="#uv-pip-list--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-pip-list--extra-index-url"><a href="#uv-pip-list--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-list--find-links"><a href="#uv-pip-list--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选分发之外，还要搜索候选分发的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源分发（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-pip-list--format"><a href="#uv-pip-list--format"><code>--format</code></a> <i>format</i></dt><dd><p>选择输出格式</p>
<p>[默认值：columns]</p><p>可能的值：</p>
<ul>
<li><code>columns</code>：以人类可读的表格显示包列表</li>
<li><code>freeze</code>：以类似 <code>pip freeze</code> 的格式显示包列表，每行一个包及其版本</li>
<li><code>json</code>：以机器可读的 JSON 格式显示包列表</li>
</ul></dd><dt id="uv-pip-list--help"><a href="#uv-pip-list--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-list--index"><a href="#uv-pip-list--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-list--index-strategy"><a href="#uv-pip-list--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时要使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，攻击者可以在备用索引上上传具有相同名称的恶意包。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-pip-list--index-url"><a href="#uv-pip-list--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-list--keyring-provider"><a href="#uv-pip-list--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-pip-list--managed-python"><a href="#uv-pip-list--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-list--native-tls"><a href="#uv-pip-list--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-list--no-cache"><a href="#uv-pip-list--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-list--no-config"><a href="#uv-pip-list--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-list--no-index"><a href="#uv-pip-list--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-pip-list--no-managed-python"><a href="#uv-pip-list--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-list--no-progress"><a href="#uv-pip-list--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-list--no-python-downloads"><a href="#uv-pip-list--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-list--offline"><a href="#uv-pip-list--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-list--outdated"><a href="#uv-pip-list--outdated"><code>--outdated</code></a></dt><dd><p>列出过时的包。</p>
<p>每个包的最新版本将与已安装版本一起显示。最新的包将从输出中省略。</p>
</dd><dt id="uv-pip-list--project"><a href="#uv-pip-list--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-list--python"><a href="#uv-pip-list--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应列出其包的 Python 解释器。</p>
<p>默认情况下，uv 在虚拟环境中列出包，但如果未找到虚拟环境，将显示系统 Python 环境中的包。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-list--quiet"><a href="#uv-pip-list--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-list--strict"><a href="#uv-pip-list--strict"><code>--strict</code></a></dt><dd><p>验证 Python 环境，以检测具有缺失依赖项和其他问题的包</p>
</dd><dt id="uv-pip-list--system"><a href="#uv-pip-list--system"><code>--system</code></a></dt><dd><p>列出系统 Python 环境中的包。</p>
<p>禁用虚拟环境的发现。</p>
<p>有关 Python 发现的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-list--verbose"><a href="#uv-pip-list--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip show

显示有关一个或多个已安装包的信息

<h3 class="cli-reference">用法</h3>

```
uv pip show [OPTIONS] [PACKAGE]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-pip-show--package"><a href="#uv-pip-show--package"<code>PACKAGE</code></a></dt><dd><p>要显示的包</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-show--allow-insecure-host"><a href="#uv-pip-show--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-show--cache-dir"><a href="#uv-pip-show--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-show--color"><a href="#uv-pip-show--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-show--config-file"><a href="#uv-pip-show--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-show--directory"><a href="#uv-pip-show--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-show--files"><a href="#uv-pip-show--files"><code>--files</code></a>, <code>-f</code></dt><dd><p>显示每个包的完整已安装文件列表</p>
</dd><dt id="uv-pip-show--help"><a href="#uv-pip-show--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-show--managed-python"><a href="#uv-pip-show--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-show--native-tls"><a href="#uv-pip-show--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-show--no-cache"><a href="#uv-pip-show--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-show--no-config"><a href="#uv-pip-show--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-show--no-managed-python"><a href="#uv-pip-show--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-show--no-progress"><a href="#uv-pip-show--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-show--no-python-downloads"><a href="#uv-pip-show--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-show--offline"><a href="#uv-pip-show--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-show--project"><a href="#uv-pip-show--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-show--python"><a href="#uv-pip-show--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>在其中查找包的 Python 解释器。</p>
<p>默认情况下，uv 在虚拟环境中查找包，但如果未找到虚拟环境，将在系统 Python 环境中查找包。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-show--quiet"><a href="#uv-pip-show--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-show--strict"><a href="#uv-pip-show--strict"><code>--strict</code></a></dt><dd><p>验证 Python 环境，以检测具有缺失依赖项和其他问题的包</p>
</dd><dt id="uv-pip-show--system"><a href="#uv-pip-show--system"><code>--system</code></a></dt><dd><p>在系统 Python 环境中显示包。</p>
<p>禁用虚拟环境的发现。</p>
<p>有关 Python 发现的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-show--verbose"><a href="#uv-pip-show--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip tree

显示环境的依赖树

<h3 class="cli-reference">用法</h3>

```
uv pip tree [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-tree--allow-insecure-host"><a href="#uv-pip-tree--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--cache-dir"><a href="#uv-pip-tree--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--color"><a href="#uv-pip-tree--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-tree--config-file"><a href="#uv-pip-tree--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--default-index"><a href="#uv-pip-tree--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--depth"><a href="#uv-pip-tree--depth"><code>--depth</code></a>, <code>-d</code> <i>depth</i></dt><dd><p>依赖树的最大显示深度</p>
<p>[默认值：255]</p></dd><dt id="uv-pip-tree--directory"><a href="#uv-pip-tree--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--exclude-newer"><a href="#uv-pip-tree--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--extra-index-url"><a href="#uv-pip-tree--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--find-links"><a href="#uv-pip-tree--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选分发之外，还要搜索候选分发的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源分发（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--help"><a href="#uv-pip-tree--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-tree--index"><a href="#uv-pip-tree--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--index-strategy"><a href="#uv-pip-tree--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时要使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，攻击者可以在备用索引上上传具有相同名称的恶意包。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-pip-tree--index-url"><a href="#uv-pip-tree--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--invert"><a href="#uv-pip-tree--invert"><code>--invert</code></a>, <code>--reverse</code></dt><dd><p>显示给定包的反向依赖关系。此标志将反转树并显示依赖于给定包的包</p>
</dd><dt id="uv-pip-tree--keyring-provider"><a href="#uv-pip-tree--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-pip-tree--managed-python"><a href="#uv-pip-tree--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--native-tls"><a href="#uv-pip-tree--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--no-cache"><a href="#uv-pip-tree--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--no-config"><a href="#uv-pip-tree--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--no-dedupe"><a href="#uv-pip-tree--no-dedupe"><code>--no-dedupe</code></a></dt><dd><p>不对重复的依赖项进行去重。通常，当一个包已经显示其依赖项时，后续出现将不会重新显示其依赖项，并包含一个 (*) 表示它已经显示过。此标志将导致这些重复项被重复显示</p>
</dd><dt id="uv-pip-tree--no-index"><a href="#uv-pip-tree--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-pip-tree--no-managed-python"><a href="#uv-pip-tree--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--no-progress"><a href="#uv-pip-tree--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--no-python-downloads"><a href="#uv-pip-tree--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-tree--offline"><a href="#uv-pip-tree--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--outdated"><a href="#uv-pip-tree--outdated"><code>--outdated</code></a></dt><dd><p>显示树中每个包的最新可用版本</p>
</dd><dt id="uv-pip-tree--package"><a href="#uv-pip-tree--package"><code>--package</code></a> <i>package</i></dt><dd><p>仅显示指定的包</p>
</dd><dt id="uv-pip-tree--project"><a href="#uv-pip-tree--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--prune"><a href="#uv-pip-tree--prune"><code>--prune</code></a> <i>prune</i></dt><dd><p>从依赖树的显示中修剪给定的包</p>
</dd><dt id="uv-pip-tree--python"><a href="#uv-pip-tree--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应列出其包的 Python 解释器。</p>
<p>默认情况下，uv 在虚拟环境中列出包，但如果未找到虚拟环境，将显示系统 Python 环境中的包。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--quiet"><a href="#uv-pip-tree--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-tree--show-sizes"><a href="#uv-pip-tree--show-sizes"><code>--show-sizes</code></a></dt><dd><p>显示树中包的压缩 wheel 大小</p>
</dd><dt id="uv-pip-tree--show-version-specifiers"><a href="#uv-pip-tree--show-version-specifiers"><code>--show-version-specifiers</code></a></dt><dd><p>显示对每个包施加的版本约束</p>
</dd><dt id="uv-pip-tree--strict"><a href="#uv-pip-tree--strict"><code>--strict</code></a></dt><dd><p>验证 Python 环境，以检测具有缺失依赖项和其他问题的包</p>
</dd><dt id="uv-pip-tree--system"><a href="#uv-pip-tree--system"><code>--system</code></a></dt><dd><p>列出系统 Python 环境中的包。</p>
<p>禁用虚拟环境的发现。</p>
<p>有关 Python 发现的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-tree--verbose"><a href="#uv-pip-tree--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv pip check

验证已安装的包具有兼容的依赖项

<h3 class="cli-reference">用法</h3>

```
uv pip check [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-pip-check--allow-insecure-host"><a href="#uv-pip-check--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-pip-check--cache-dir"><a href="#uv-pip-check--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-pip-check--color"><a href="#uv-pip-check--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-pip-check--config-file"><a href="#uv-pip-check--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-pip-check--directory"><a href="#uv-pip-check--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-pip-check--help"><a href="#uv-pip-check--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-pip-check--managed-python"><a href="#uv-pip-check--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-check--native-tls"><a href="#uv-pip-check--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-pip-check--no-cache"><a href="#uv-pip-check--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-pip-check--no-config"><a href="#uv-pip-check--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-pip-check--no-managed-python"><a href="#uv-pip-check--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-check--no-progress"><a href="#uv-pip-check--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-pip-check--no-python-downloads"><a href="#uv-pip-check--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-pip-check--offline"><a href="#uv-pip-check--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-pip-check--project"><a href="#uv-pip-check--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-pip-check--python"><a href="#uv-pip-check--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>应检查其包的 Python 解释器。</p>
<p>默认情况下，uv 在虚拟环境中检查包，但如果未找到虚拟环境，将检查系统 Python 环境中的包。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-check--python-platform"><a href="#uv-pip-check--python-platform"><code>--python-platform</code></a> <i>python-platform</i></dt><dd><p>应检查其包的平台。</p>
<p>默认情况下，已安装的包将针对当前解释器的平台进行检查。</p>
<p>表示为"目标三元组"，一个描述目标平台 CPU、供应商和操作系统名称的字符串，如 <code>x86_64-unknown-linux-gnu</code> 或 <code>aarch64-apple-darwin</code>。</p>
<p>当目标为 macOS（Darwin）时，默认最低版本为 <code>13.0</code>。使用 <code>MACOSX_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 iOS 时，默认最低版本为 <code>13.0</code>。使用 <code>IPHONEOS_DEPLOYMENT_TARGET</code> 指定不同的最低版本，例如 <code>14.0</code>。</p>
<p>当目标为 Android 时，默认最低 Android API 级别为 <code>24</code>。使用 <code>ANDROID_API_LEVEL</code> 指定不同的最低版本，例如 <code>26</code>。</p>
<p>可能的值：</p>
<ul>
<li><code>windows</code>：<code>x86_64-pc-windows-msvc</code> 的别名，Windows 的默认目标</li>
<li><code>linux</code>：<code>x86_64-unknown-linux-gnu</code> 的别名，Linux 的默认目标</li>
<li><code>macos</code>：<code>aarch64-apple-darwin</code> 的别名，macOS 的默认目标</li>
<li><code>x86_64-pc-windows-msvc</code>：64 位 x86 Windows 目标</li>
<li><code>aarch64-pc-windows-msvc</code>：ARM64 Windows 目标</li>
<li><code>i686-pc-windows-msvc</code>：32 位 x86 Windows 目标</li>
<li><code>x86_64-unknown-linux-gnu</code>：x86 Linux 目标。等同于 <code>x86_64-manylinux_2_28</code></li>
<li><code>aarch64-apple-darwin</code>：基于 ARM 的 macOS 目标，见于 Apple Silicon 设备</li>
<li><code>x86_64-apple-darwin</code>：x86 macOS 目标</li>
<li><code>aarch64-unknown-linux-gnu</code>：ARM64 Linux 目标。等同于 <code>aarch64-manylinux_2_28</code></li>
<li><code>aarch64-unknown-linux-musl</code>：ARM64 Linux 目标</li>
<li><code>x86_64-unknown-linux-musl</code>：<code>x86_64</code> Linux 目标</li>
<li><code>riscv64-unknown-linux</code>：RISCV64 Linux 目标</li>
<li><code>x86_64-manylinux2014</code>：<code>manylinux2014</code> 平台的 <code>x86_64</code> 目标。等同于 <code>x86_64-manylinux_2_17</code></li>
<li><code>x86_64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>x86_64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 <code>x86_64</code> 目标</li>
<li><code>aarch64-manylinux2014</code>：<code>manylinux2014</code> 平台的 ARM64 目标。等同于 <code>aarch64-manylinux_2_17</code></li>
<li><code>aarch64-manylinux_2_17</code>：<code>manylinux_2_17</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_28</code>：<code>manylinux_2_28</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_31</code>：<code>manylinux_2_31</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_32</code>：<code>manylinux_2_32</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_33</code>：<code>manylinux_2_33</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_34</code>：<code>manylinux_2_34</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_35</code>：<code>manylinux_2_35</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_36</code>：<code>manylinux_2_36</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_37</code>：<code>manylinux_2_37</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_38</code>：<code>manylinux_2_38</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_39</code>：<code>manylinux_2_39</code> 平台的 ARM64 目标</li>
<li><code>aarch64-manylinux_2_40</code>：<code>manylinux_2_40</code> 平台的 ARM64 目标</li>
<li><code>aarch64-linux-android</code>：ARM64 Android 目标</li>
<li><code>x86_64-linux-android</code>：<code>x86_64</code> Android 目标</li>
<li><code>wasm32-pyodide2024</code>：使用 Pyodide 2024 平台的 wasm32 目标。旨在与 Python 3.12 一起使用</li>
<li><code>arm64-apple-ios</code>：iOS 设备的 ARM64 目标</li>
<li><code>arm64-apple-ios-simulator</code>：iOS 模拟器的 ARM64 目标</li>
<li><code>x86_64-apple-ios-simulator</code>：iOS 模拟器的 <code>x86_64</code> 目标</li>
</ul></dd><dt id="uv-pip-check--python-version"><a href="#uv-pip-check--python-version"><code>--python-version</code></a> <i>python-version</i></dt><dd><p>应针对其检查包的 Python 版本。</p>
<p>默认情况下，已安装的包将针对当前解释器的版本进行检查。</p>
</dd><dt id="uv-pip-check--quiet"><a href="#uv-pip-check--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-pip-check--system"><a href="#uv-pip-check--system"><code>--system</code></a></dt><dd><p>检查系统 Python 环境中的包。</p>
<p>禁用虚拟环境的发现。</p>
<p>有关 Python 发现的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_SYSTEM_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-pip-check--verbose"><a href="#uv-pip-check--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv venv

创建虚拟环境。

默认情况下，在工作目录中创建一个名为 `.venv` 的虚拟环境。可以位置性地提供替代路径。

如果在项目中，可以使用 `UV_PROJECT_ENVIRONMENT` 环境变量更改默认环境名称；这仅当从项目根目录运行时适用。

如果目标路径存在虚拟环境，它将被移除，并创建一个新的空虚拟环境。

使用 uv 时，不需要激活虚拟环境。uv 将在工作目录或任何父目录中找到名为 `.venv` 的虚拟环境。

<h3 class="cli-reference">用法</h3>

```
uv venv [OPTIONS] [PATH]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-venv--path"><a href="#uv-venv--path"<code>PATH</code></a></dt><dd><p>要创建的虚拟环境的路径。</p>
<p>默认为工作目录中的 <code>.venv</code>。</p>
<p>相对路径相对于工作目录解析。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-venv--allow-existing"><a href="#uv-venv--allow-existing"><code>--allow-existing</code></a></dt><dd><p>保留目标路径上的任何现有文件或目录。</p>
<p>默认情况下，如果给定路径非空，<code>uv venv</code> 将退出并报错。<code>--allow-existing</code> 选项将改为写入给定路径，无论其内容如何，并且不会事先清除它。</p>
<p>警告：如果现有虚拟环境和新建虚拟环境链接到不同的 Python 解释器，此选项可能导致意外行为。</p>
</dd><dt id="uv-venv--allow-insecure-host"><a href="#uv-venv--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-venv--cache-dir"><a href="#uv-venv--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-venv--clear"><a href="#uv-venv--clear"><code>--clear</code></a>, <code>-c</code></dt><dd><p>移除目标路径上的任何现有文件或目录。</p>
<p>默认情况下，如果给定路径非空，<code>uv venv</code> 将退出并报错。<code>--clear</code> 选项将改为在创建新虚拟环境之前清除非空路径。</p>
<p>也可以通过 <code>UV_VENV_CLEAR</code> 环境变量设置。</p></dd><dt id="uv-venv--color"><a href="#uv-venv--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-venv--config-file"><a href="#uv-venv--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-venv--default-index"><a href="#uv-venv--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-venv--directory"><a href="#uv-venv--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-venv--exclude-newer"><a href="#uv-venv--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-venv--exclude-newer-package"><a href="#uv-venv--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-venv--extra-index-url"><a href="#uv-venv--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-venv--find-links"><a href="#uv-venv--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选分发之外，还要搜索候选分发的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源分发（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-venv--help"><a href="#uv-venv--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-venv--index"><a href="#uv-venv--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-venv--index-strategy"><a href="#uv-venv--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时要使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，攻击者可以在备用索引上上传具有相同名称的恶意包。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-venv--index-url"><a href="#uv-venv--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-venv--keyring-provider"><a href="#uv-venv--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-venv--link-mode"><a href="#uv-venv--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅用于安装种子包。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过移除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-venv--managed-python"><a href="#uv-venv--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-venv--native-tls"><a href="#uv-venv--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-venv--no-cache"><a href="#uv-venv--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读取或写入缓存，而是在操作期间使用临时目录</p>
<p>也可以通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-venv--no-config"><a href="#uv-venv--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>, <code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中发现。</p>
<p>也可以通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-venv--no-index"><a href="#uv-venv--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-venv--no-managed-python"><a href="#uv-venv--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用 uv 管理的 Python 版本的使用。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可以通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-venv--no-progress"><a href="#uv-venv--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，微调框或进度条。</p>
<p>也可以通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-venv--no-project"><a href="#uv-venv--no-project"><code>--no-project</code></a>, <code>--no-workspace</code></dt><dd><p>避免发现项目或工作区。</p>
<p>默认情况下，uv 会在当前目录或任何父目录中搜索项目，以确定虚拟环境的默认路径并检查 Python 版本约束（如果有）。</p>
</dd><dt id="uv-venv--no-python-downloads"><a href="#uv-venv--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-venv--offline"><a href="#uv-venv--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可以通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-venv--project"><a href="#uv-venv--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录内运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（如相对路径）将相对于当前工作目录解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可以通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-venv--prompt"><a href="#uv-venv--prompt"><code>--prompt</code></a> <i>prompt</i></dt><dd><p>为虚拟环境提供替代提示前缀。</p>
<p>默认情况下，提示取决于是否向 <code>uv venv</code> 提供了路径。如果提供了（例如 <code>uv venv project</code>），提示将设置为目录名称。如果未提供（<code>uv venv</code>），提示将设置为当前目录的名称。</p>
<p>如果提供了 "."，则无论是否向 <code>uv venv</code> 提供了路径，都将使用当前目录名称。</p>
</dd><dt id="uv-venv--python"><a href="#uv-venv--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于虚拟环境的 Python 解释器。</p>
<p>在虚拟环境创建期间，uv 不会在虚拟环境中查找 Python 解释器。</p>
<p>有关 Python 发现和支持的请求格式的详细信息，请参阅 <a href="#uv-python">uv python</a>。</p>
<p>也可以通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-venv--quiet"><a href="#uv-venv--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，其中 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-venv--refresh"><a href="#uv-venv--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存的数据</p>
</dd><dt id="uv-venv--refresh-package"><a href="#uv-venv--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-venv--relocatable"><a href="#uv-venv--relocatable"><code>--relocatable</code></a></dt><dd><p>使虚拟环境可重定位。</p>
<p>可重定位的虚拟环境可以移动和重新分发，而不会使其关联的入口点和激活脚本失效。</p>
<p>请注意，这只能保证标准的 <code>console_scripts</code> 和 <code>gui_scripts</code>。其他脚本如果带有通用的 <code>#!python[w]</code> shebang，可能会被调整，而二进制文件则保持不变。</p>
<p>由于使环境可重定位（通过写入相对路径而不是绝对路径），入口点和脚本本身将*不能*重定位。换句话说，将这些入口点和脚本复制到环境之外的位置将不起作用，因为它们引用的是相对于环境本身的路径。</p>
</dd><dt id="uv-venv--seed"><a href="#uv-venv--seed"><code>--seed</code></a></dt><dd><p>将种子包（一个或多个：<code>pip</code>、<code>setuptools</code> 和 <code>wheel</code>）安装到虚拟环境中。</p>
<p>请注意，<code>setuptools</code> 和 <code>wheel</code> 不包含在 Python 3.12+ 环境中。</p>
<p>也可以通过 <code>UV_VENV_SEED</code> 环境变量设置。</p></dd><dt id="uv-venv--system-site-packages"><a href="#uv-venv--system-site-packages"><code>--system-site-packages</code></a></dt><dd><p>给予虚拟环境对系统站点包目录的访问权限。</p>
<p>与 <code>pip</code> 不同，当使用 <code>--system-site-packages</code> 创建虚拟环境时，uv 在运行诸如 <code>uv pip list</code> 或 <code>uv pip install</code> 之类的命令时*不会*考虑系统站点包。<code>--system-site-packages</code> 标志将在运行时为虚拟环境提供对系统站点包目录的访问权限，但不会影响 uv 命令的行为。</p>
</dd><dt id="uv-venv--verbose"><a href="#uv-venv--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv build

将 Python 包构建为源分发和 wheel。

`uv build` 接受目录或源分发的路径，默认为当前工作目录。

默认情况下，如果传递目录，`uv build` 将从源目录构建源分发（"sdist"），并从源分发构建二进制分发（"wheel"）。

`uv build --sdist` 可用于仅构建源分发，`uv build --wheel` 可用于仅构建二进制分发，`uv build --sdist --wheel` 可用于从源构建两种分发。

如果传递源分发，`uv build --wheel` 将从源分发构建 wheel。

<h3 class="cli-reference">用法</h3>

```
uv build [OPTIONS] [SRC]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-build--src"><a href="#uv-build--src"<code>SRC</code></a></dt><dd><p>应从中构建分发的目录，或要构建为 wheel 的源分发归档。</p>
<p>默认为当前工作目录。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-build--all-packages"><a href="#uv-build--all-packages"><code>--all-packages</code></a>, <code>--all</code></dt><dd><p>构建工作区中的所有包。</p>
<p>将从提供的源目录或当前目录（如果未提供源目录）发现工作区。</p>
<p>如果工作区成员不存在，uv 将退出并报错。</p>
</dd><dt id="uv-build--allow-insecure-host"><a href="#uv-build--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许对主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：此列表中包含的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您暴露于 MITM 攻击。</p>
<p>也可以通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-build--build-constraints"><a href="#uv-build--build-constraints"><code>--build-constraints</code></a>, <code>--build-constraint</code>, <code>-b</code> <i>build-constraints</i></dt><dd><p>在构建分发时使用给定的需求文件约束构建依赖项。</p>
<p>约束文件是类似 <code>requirements.txt</code> 的文件，仅控制安装的构建依赖项的*版本*。但是，在约束文件中包含包不会*自行*触发该包的包含。</p>
<p>也可以通过 <code>UV_BUILD_CONSTRAINT</code> 环境变量设置。</p></dd><dt id="uv-build--cache-dir"><a href="#uv-build--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>默认为 macOS 和 Linux 上的 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，以及 Windows 上的 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可以通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-build--clear"><a href="#uv-build--clear"><code>--clear</code></a></dt><dd><p>在构建之前清除输出目录，移除过时的构件</p>
</dd><dt id="uv-build--color"><a href="#uv-build--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>：仅当输出到支持颜色的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>：无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>：禁用彩色输出</li>
</ul></dd><dt id="uv-build--config-file"><a href="#uv-build--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可以通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-build--config-setting"><a href="#uv-build--config-setting"><code>--config-setting</code></a>, <code>--config-settings</code>, <code>-C</code> <i>config-setting</i></dt><dd><p>传递给 PEP 517 构建后端的设置，指定为 <code>KEY=VALUE</code> 对</p>
</dd><dt id="uv-build--config-settings-package"><a href="#uv-build--config-settings-package"><code>--config-settings-package</code></a>, <code>--config-settings-package</code> <i>config-settings-package</i></dt><dd><p>传递给特定包的 PEP 517 构建后端的设置，指定为 <code>PACKAGE:KEY=VALUE</code> 对</p>
</dd><dt id="uv-build--default-index"><a href="#uv-build--default-index"><code>--default-index</code></a> <i>default-index</i></dt><dd><p>默认包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--index</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_DEFAULT_INDEX</code> 环境变量设置。</p></dd><dt id="uv-build--directory"><a href="#uv-build--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可以通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-build--exclude-newer"><a href="#uv-build--exclude-newer"><code>--exclude-newer</code></a> <i>exclude-newer</i></dt><dd><p>将候选包限制为在给定日期之前上传的包。</p>
<p>接受 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）和系统配置时区中相同格式的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>也可以通过 <code>UV_EXCLUDE_NEWER</code> 环境变量设置。</p></dd><dt id="uv-build--exclude-newer-package"><a href="#uv-build--exclude-newer-package"><code>--exclude-newer-package</code></a> <i>exclude-newer-package</i></dt><dd><p>将特定包的候选包限制为在给定日期之前上传的包。</p>
<p>接受格式为 <code>PACKAGE=DATE</code> 的包-日期对，其中 <code>DATE</code> 是 RFC 3339 时间戳（例如 <code>2006-12-02T02:07:43Z</code>）或系统配置时区中的本地日期（例如 <code>2006-12-02</code>）。</p>
<p>可以为不同的包多次提供。</p>
</dd><dt id="uv-build--extra-index-url"><a href="#uv-build--extra-index-url"><code>--extra-index-url</code></a> <i>extra-index-url</i></dt><dd><p>（已弃用：使用 <code>--index</code> 代替）要使用的额外包索引 URL，除了 <code>--index-url</code> 之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--index-url</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--extra-index-url</code> 标志时，较早的值具有更高的优先级。</p>
<p>也可以通过 <code>UV_EXTRA_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-build--find-links"><a href="#uv-build--find-links"><code>--find-links</code></a>, <code>-f</code> <i>find-links</i></dt><dd><p>除了在注册表索引中找到的候选分发之外，还要搜索候选分发的位置。</p>
<p>如果是路径，则目标必须是顶层包含 wheel 文件（<code>.whl</code>）或源分发（例如 <code>.tar.gz</code> 或 <code>.zip</code>）的目录。</p>
<p>如果是 URL，则页面必须包含指向符合上述格式的包文件的平面链接列表。</p>
<p>也可以通过 <code>UV_FIND_LINKS</code> 环境变量设置。</p></dd><dt id="uv-build--force-pep517"><a href="#uv-build--force-pep517"><code>--force-pep517</code></a></dt><dd><p>始终通过 PEP 517 构建，不要对 uv 构建后端使用快速路径。</p>
<p>默认情况下，对于使用 uv 构建后端的包，uv 不会创建 PEP 517 构建环境，而是使用直接调用构建后端的快速路径。此选项强制始终使用 PEP 517。</p>
</dd><dt id="uv-build--fork-strategy"><a href="#uv-build--fork-strategy"><code>--fork-strategy</code></a> <i>fork-strategy</i></dt><dd><p>在跨 Python 版本和平台选择给定包的多个版本时要使用的策略。</p>
<p>默认情况下，uv 将优化为每个支持的 Python 版本（<code>requires-python</code>）选择每个包的最新版本，同时最小化跨平台选择的版本数量。</p>
<p>在 <code>fewest</code> 下，uv 将最小化每个包选择的版本数量，优先选择与更广泛支持的 Python 版本或平台兼容的旧版本。</p>
<p>也可以通过 <code>UV_FORK_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>fewest</code>：优化为每个包选择最少数量的版本。如果旧版本与更广泛支持的 Python 版本或平台兼容，则可能优先选择旧版本</li>
<li><code>requires-python</code>：优化为每个支持的 Python 版本选择每个包的最新支持版本</li>
</ul></dd><dt id="uv-build--help"><a href="#uv-build--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-build--index"><a href="#uv-build--index"><code>--index</code></a> <i>index</i></dt><dd><p>解析依赖项时要使用的 URL，除了默认索引之外。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>通过此标志提供的所有索引的优先级高于由 <code>--default-index</code> 指定的索引（默认为 PyPI）。当提供多个 <code>--index</code> 标志时，较早的值具有更高的优先级。</p>
<p>索引名称不支持作为值。相对路径必须通过 Unix 上的 <code>./</code> 或 <code>../</code> 或 Windows 上的 <code>.\\</code>、<code>..\\</code>、<code>./</code> 或 <code>../</code> 与索引名称区分开。</p>
<p>也可以通过 <code>UV_INDEX</code> 环境变量设置。</p></dd><dt id="uv-build--index-strategy"><a href="#uv-build--index-strategy"><code>--index-strategy</code></a> <i>index-strategy</i></dt><dd><p>在针对多个索引 URL 进行解析时要使用的策略。</p>
<p>默认情况下，uv 将在给定包可用的第一个索引处停止，并将解析限制在该第一个索引上存在的包（<code>first-index</code>）。这防止了"依赖混淆"攻击，攻击者可以在备用索引上上传具有相同名称的恶意包。</p>
<p>也可以通过 <code>UV_INDEX_STRATEGY</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>first-index</code>：仅使用第一个返回给定包名称匹配项的索引的结果</li>
<li><code>unsafe-first-match</code>：在所有索引中搜索每个包名称，在移动到下一个索引之前耗尽第一个索引的版本</li>
<li><code>unsafe-best-match</code>：在所有索引中搜索每个包名称，优先选择找到的"最佳"版本。如果一个包版本在多个索引中，则仅查看第一个索引的条目</li>
</ul></dd><dt id="uv-build--index-url"><a href="#uv-build--index-url"><code>--index-url</code></a>, <code>-i</code> <i>index-url</i></dt><dd><p>（已弃用：使用 <code>--default-index</code> 代替）Python 包索引的 URL（默认为：<a href="https://pypi.org/simple">https://pypi.org/simple</a>）。</p>
<p>接受符合 PEP 503 的存储库（简单存储库 API），或具有相同格式的本地目录。</p>
<p>此标志给出的索引的优先级低于通过 <code>--extra-index-url</code> 标志指定的所有其他索引。</p>
<p>也可以通过 <code>UV_INDEX_URL</code> 环境变量设置。</p></dd><dt id="uv-build--keyring-provider"><a href="#uv-build--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行索引 URL 的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可以通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>：不使用 keyring 进行凭据查找</li>
<li><code>subprocess</code>：使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-build--link-mode"><a href="#uv-build--link-mode"><code>--link-mode</code></a> <i>link-mode</i></dt><dd><p>从全局缓存安装包时使用的方法。</p>
<p>此选项仅在构建源分发时使用。</p>
<p>默认为 macOS 上的 <code>clone</code>（也称为写时复制），以及 Linux 和 Windows 上的 <code>hardlink</code>。</p>
<p>警告：不鼓励使用符号链接模式，因为它们会在缓存和目标环境之间创建紧密耦合。例如，清除缓存（<code>uv cache clean</code>）将通过移除底层源文件来破坏所有已安装的包。请谨慎使用符号链接。</p>
<p>也可以通过 <code>UV_LINK_MODE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>clone</code>：从 wheel 克隆（即写时复制）包到 <code>site-packages</code> 目录</li>
<li><code>copy</code>：从 wheel 复制包到 <code>site-packages</code> 目录</li>
<li><code>hardlink</code>：从 wheel 硬链接包到 <code>site-packages</code> 目录</li>
<li><code>symlink</code>：从 wheel 符号链接包到 <code>site-packages</code> 目录</li>
</ul></dd><dt id="uv-build--managed-python"><a href="#uv-build--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可以通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-build--native-tls"><a href="#uv-build--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一套可靠的信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是如果您依赖包含在系统证书存储中的企业信任根（例如，用于强制代理）。</p>
<p>也可以通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-build--no-binary"><a href="#uv-build--no-binary"><code>--no-binary</code></a></dt><dd><p>不要安装预构建的 wheel。</p>
<p>给定的包将从源代码构建和安装。解析器仍将使用预构建的 wheel 来提取包元数据（如果可用）。</p>
<p>也可以通过 <code>UV_NO_BINARY</code> 环境变量设置。</p></dd><dt id="uv-build--no-binary-package"><a href="#uv-build--no-binary-package"><code>--no-binary-package</code></a> <i>no-binary-package</i></dt><dd><p>不要为特定包安装预构建的 wheel</p>
<p>也可以通过 <code>UV_NO_BINARY_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-build--no-build"><a href="#uv-build--no-build"><code>--no-build</code></a></dt><dd><p>不要构建源分发。</p>
<p>启用后，解析将不会运行任意 Python 代码。将重用已构建源分发的缓存 wheel，但需要构建分发的操作将退出并报错。</p>
<p>也可以通过 <code>UV_NO_BUILD</code> 环境变量设置。</p></dd><dt id="uv-build--no-build-isolation"><a href="#uv-build--no-build-isolation"><code>--no-build-isolation</code></a></dt><dd><p>构建源分发时禁用隔离。</p>
<p>假定 PEP 518 指定的构建依赖项已安装。</p>
<p>也可以通过 <code>UV_NO_BUILD_ISOLATION</code> 环境变量设置。</p></dd><dt id="uv-build--no-build-isolation-package"><a href="#uv-build--no-build-isolation-package"><code>--no-build-isolation-package</code></a> <i>no-build-isolation-package</i></dt><dd><p>为特定包构建源分发时禁用隔离。</p>
<p>假定包的 PEP 518 指定的构建依赖项已安装。</p>
</dd><dt id="uv-build--no-build-logs"><a href="#uv-build--no-build-logs"><code>--no-build-logs</code></a></dt><dd><p>隐藏构建后端的日志</p>
</dd>
<dt id="uv-build--no-build-package"><a href="#uv-build--no-build-package"><code>--no-build-package</code></a> <i>no-build-package</i></dt><dd><p>不为特定包构建源码分发</p>
<p>也可通过 <code>UV_NO_BUILD_PACKAGE</code> 环境变量设置。</p></dd><dt id="uv-build--no-cache"><a href="#uv-build--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-build--no-config"><a href="#uv-build--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-build--no-create-gitignore"><a href="#uv-build--no-create-gitignore"><code>--no-create-gitignore</code></a></dt><dd><p>不在输出目录中创建 <code>.gitignore</code> 文件。</p>
<p>默认情况下，uv 会在输出目录中创建一个 <code>.gitignore</code> 文件以将构建产物排除在版本控制之外。使用此标志时，该文件将被忽略。</p>
</dd><dt id="uv-build--no-index"><a href="#uv-build--no-index"><code>--no-index</code></a></dt><dd><p>忽略注册表索引（例如 PyPI），而是依赖直接 URL 依赖项和通过 <code>--find-links</code> 提供的依赖项</p>
</dd><dt id="uv-build--no-managed-python"><a href="#uv-build--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-build--no-progress"><a href="#uv-build--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-build--no-python-downloads"><a href="#uv-build--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-build--no-sources"><a href="#uv-build--no-sources"><code>--no-sources</code></a></dt><dd><p>解析依赖项时忽略 <code>tool.uv.sources</code> 表。用于针对符合标准的、可发布的包元数据进行锁定，而不是使用任何工作区、Git、URL 或本地路径源</p>
<p>也可通过 <code>UV_NO_SOURCES</code> 环境变量设置。</p></dd><dt id="uv-build--no-verify-hashes"><a href="#uv-build--no-verify-hashes"><code>--no-verify-hashes</code></a></dt><dd><p>禁用对需求文件中哈希值的验证。</p>
<p>默认情况下，uv 将验证需求文件中任何可用的哈希值，但不会要求所有需求都具有关联的哈希值。要强制进行哈希验证，请使用 <code>--require-hashes</code>。</p>
<p>也可通过 <code>UV_NO_VERIFY_HASHES</code> 环境变量设置。</p></dd><dt id="uv-build--offline"><a href="#uv-build--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-build--out-dir"><a href="#uv-build--out-dir"><code>--out-dir</code></a>, <code>-o</code> <i>out-dir</i></dt><dd><p>分发文件应写入的输出目录。</p>
<p>默认为源目录内的 <code>dist</code> 子目录，或包含源码分发存档的目录。</p>
</dd><dt id="uv-build--package"><a href="#uv-build--package"><code>--package</code></a> <i>package</i></dt><dd><p>构建工作区中的特定包。</p>
<p>工作区将从提供的源目录中发现，如果未提供源目录，则从当前目录发现。</p>
<p>如果工作区成员不存在，uv 将报错退出。</p>
</dd><dt id="uv-build--prerelease"><a href="#uv-build--prerelease"><code>--prerelease</code></a> <i>prerelease</i></dt><dd><p>考虑预发布版本时使用的策略。</p>
<p>默认情况下，uv 将接受仅发布预发布版本的包的预发布版本，以及在其声明的说明符中包含显式预发布标记的第一方需求（<code>if-necessary-or-explicit</code>）。</p>
<p>也可通过 <code>UV_PRERELEASE</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disallow</code>:  不允许所有预发布版本</li>
<li><code>allow</code>:  允许所有预发布版本</li>
<li><code>if-necessary</code>:  如果包的所有版本都是预发布版本，则允许预发布版本</li>
<li><code>explicit</code>:  对于版本需求中具有显式预发布标记的第一方包，允许预发布版本</li>
<li><code>if-necessary-or-explicit</code>:  如果包的所有版本都是预发布版本，或者包在其版本需求中具有显式预发布标记，则允许预发布版本</li>
</ul></dd><dt id="uv-build--project"><a href="#uv-build--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-build--python"><a href="#uv-build--python"><code>--python</code></a>, <code>-p</code> <i>python</i></dt><dd><p>用于构建环境的 Python 解释器。</p>
<p>默认情况下，构建在隔离的虚拟环境中执行。发现的解释器将用于创建这些环境，并将根据平台进行符号链接或复制。</p>
<p>请参阅 <a href="#uv-python">uv python</a> 以查看支持的请求格式。</p>
<p>也可通过 <code>UV_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-build--quiet"><a href="#uv-build--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-build--refresh"><a href="#uv-build--refresh"><code>--refresh</code></a></dt><dd><p>刷新所有缓存数据</p>
</dd><dt id="uv-build--refresh-package"><a href="#uv-build--refresh-package"><code>--refresh-package</code></a> <i>refresh-package</i></dt><dd><p>刷新特定包的缓存数据</p>
</dd><dt id="uv-build--require-hashes"><a href="#uv-build--require-hashes"><code>--require-hashes</code></a></dt><dd><p>要求每个需求都有匹配的哈希值。</p>
<p>默认情况下，uv 将验证需求文件中任何可用的哈希值，但不会要求所有需求都具有关联的哈希值。</p>
<p>启用 <code>--require-hashes</code> 时，所有需求必须包含一个哈希或一组哈希，并且所有需求必须固定到确切版本（例如 <code>==1.0.0</code>），或通过直接 URL 指定。</p>
<p>哈希检查模式引入了一些额外的约束：</p>
<ul>
<li>不支持 Git 依赖项。 - 不支持可编辑安装。 - 不支持本地依赖项，除非它们指向特定的 wheel（<code>.whl</code>）或源码存档（<code>.zip</code>、<code>.tar.gz</code>），而不是目录。</li>
</ul>
<p>也可通过 <code>UV_REQUIRE_HASHES</code> 环境变量设置。</p></dd><dt id="uv-build--resolution"><a href="#uv-build--resolution"><code>--resolution</code></a> <i>resolution</i></dt><dd><p>为给定包需求在不同兼容版本之间进行选择时使用的策略。</p>
<p>默认情况下，uv 将使用每个包的最新兼容版本（<code>highest</code>）。</p>
<p>也可通过 <code>UV_RESOLUTION</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>highest</code>:  解析每个包的最高兼容版本</li>
<li><code>lowest</code>:  解析每个包的最低兼容版本</li>
<li><code>lowest-direct</code>:  解析任何直接依赖项的最低兼容版本，以及任何传递依赖项的最高兼容版本</li>
</ul></dd><dt id="uv-build--sdist"><a href="#uv-build--sdist"><code>--sdist</code></a></dt><dd><p>从给定目录构建源码分发（"sdist"）</p>
</dd><dt id="uv-build--upgrade"><a href="#uv-build--upgrade"><code>--upgrade</code></a>, <code>-U</code></dt><dd><p>允许包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh</code></p>
</dd><dt id="uv-build--upgrade-package"><a href="#uv-build--upgrade-package"><code>--upgrade-package</code></a>, <code>-P</code> <i>upgrade-package</i></dt><dd><p>允许特定包升级，忽略任何现有输出文件中的固定版本。隐含 <code>--refresh-package</code></p>
</dd><dt id="uv-build--verbose"><a href="#uv-build--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd><dt id="uv-build--wheel"><a href="#uv-build--wheel"><code>--wheel</code></a></dt><dd><p>从给定目录构建二进制分发（"wheel"）</p>
</dd></dl>

## uv publish

将分发包上传到索引

<h3 class="cli-reference">用法</h3>

```
uv publish [OPTIONS] [FILES]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-publish--files"><a href="#uv-publish--files"<code>FILES</code></a></dt><dd><p>要上传的文件路径。接受通配符表达式。</p>
<p>默认为 <code>dist</code> 目录。仅选择 wheel 和源码分发，同时忽略其他文件。</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-publish--allow-insecure-host"><a href="#uv-publish--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-publish--cache-dir"><a href="#uv-publish--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-publish--check-url"><a href="#uv-publish--check-url"><code>--check-url</code></a> <i>check-url</i></dt><dd><p>检查索引 URL 中是否存在现有文件以跳过重复上传。</p>
<p>此选项允许重试仅在部分文件上传后失败的发布，并处理由于并行上传相同文件而导致的错误。</p>
<p>在上传之前，会检查索引。如果索引中已存在完全相同的文件，则不会上传该文件。如果在上传过程中发生错误，将再次检查索引，以处理相同文件被并行上传两次的情况。</p>
<p>确切行为因索引而异。上传到 PyPI 时，即使没有 <code>--check-url</code>，上传相同文件也会成功，而大多数其他索引会报错。上传到 pyx 时，可以从发布 URL 自动推断索引 URL。</p>
<p>索引必须提供受支持的哈希之一（SHA-256、SHA-384 或 SHA-512）。</p>
<p>也可通过 <code>UV_PUBLISH_CHECK_URL</code> 环境变量设置。</p></dd><dt id="uv-publish--color"><a href="#uv-publish--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-publish--config-file"><a href="#uv-publish--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-publish--directory"><a href="#uv-publish--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-publish--dry-run"><a href="#uv-publish--dry-run"><code>--dry-run</code></a></dt><dd><p>执行空运行而不上传文件。</p>
<p>启用后，如果提供了 <code>--check-url</code>，命令将检查现有文件，并在支持的情况下对索引执行验证，但不会上传任何文件。</p>
</dd><dt id="uv-publish--help"><a href="#uv-publish--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-publish--index"><a href="#uv-publish--index"><code>--index</code></a> <i>index</i></dt><dd><p>配置中用于发布的索引名称。</p>
<p>索引必须具有 <code>publish-url</code> 设置，例如：</p>
<pre><code class="language-toml">[[tool.uv.index]]
name = "pypi"
url = "https://pypi.org/simple"
publish-url = "https://upload.pypi.org/legacy/"
</code></pre>
<p>索引 <code>url</code> 将用于检查现有文件以跳过重复上传。</p>
<p>使用这些设置，以下两次调用是等效的：</p>
<pre><code class="language-shell">uv publish --index pypi
uv publish --publish-url https://upload.pypi.org/legacy/ --check-url https://pypi.org/simple
</code></pre>
<p>也可通过 <code>UV_PUBLISH_INDEX</code> 环境变量设置。</p></dd><dt id="uv-publish--keyring-provider"><a href="#uv-publish--keyring-provider"><code>--keyring-provider</code></a> <i>keyring-provider</i></dt><dd><p>尝试使用 <code>keyring</code> 进行远程需求文件的身份验证。</p>
<p>目前仅支持 <code>--keyring-provider subprocess</code>，它配置 uv 使用 <code>keyring</code> CLI 处理身份验证。</p>
<p>默认为 <code>disabled</code>。</p>
<p>也可通过 <code>UV_KEYRING_PROVIDER</code> 环境变量设置。</p><p>可能的值：</p>
<ul>
<li><code>disabled</code>:  不使用密钥环进行凭据查找</li>
<li><code>subprocess</code>:  使用 <code>keyring</code> 命令进行凭据查找</li>
</ul></dd><dt id="uv-publish--managed-python"><a href="#uv-publish--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-publish--native-tls"><a href="#uv-publish--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-publish--no-cache"><a href="#uv-publish--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-publish--no-config"><a href="#uv-publish--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-publish--no-managed-python"><a href="#uv-publish--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-publish--no-progress"><a href="#uv-publish--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-publish--no-python-downloads"><a href="#uv-publish--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-publish--offline"><a href="#uv-publish--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-publish--password"><a href="#uv-publish--password"><code>--password</code></a>, <code>-p</code> <i>password</i></dt><dd><p>上传的密码</p>
<p>也可通过 <code>UV_PUBLISH_PASSWORD</code> 环境变量设置。</p></dd><dt id="uv-publish--project"><a href="#uv-publish--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-publish--publish-url"><a href="#uv-publish--publish-url"><code>--publish-url</code></a> <i>publish-url</i></dt><dd><p>上传端点的 URL（不是索引 URL）。</p>
<p>请注意，索引访问（例如 <code>https:://.../simple</code>）和索引上传通常有不同的 URL。</p>
<p>默认为 PyPI 的发布 URL（<a href="https://upload.pypi.org/legacy/">https://upload.pypi.org/legacy/</a>）。</p>
<p>也可通过 <code>UV_PUBLISH_URL</code> 环境变量设置。</p></dd><dt id="uv-publish--quiet"><a href="#uv-publish--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-publish--token"><a href="#uv-publish--token"><code>--token</code></a>, <code>-t</code> <i>token</i></dt><dd><p>上传的令牌。</p>
<p>使用令牌等效于将 <code>__token__</code> 作为 <code>--username</code> 传递，并将令牌作为 <code>--password</code> 密码传递。</p>
<p>也可通过 <code>UV_PUBLISH_TOKEN</code> 环境变量设置。</p></dd><dt id="uv-publish--trusted-publishing"><a href="#uv-publish--trusted-publishing"><code>--trusted-publishing</code></a> <i>trusted-publishing</i></dt><dd><p>配置可信发布。</p>
<p>默认情况下，uv 在受支持的环境中运行时检查可信发布，但如果未配置则忽略它。</p>
<p>uv 支持的可信发布环境包括 GitHub Actions 和 GitLab CI/CD。</p>
<p>可能的值：</p>
<ul>
<li><code>automatic</code>:  当我们处于受支持的环境时尝试可信发布，如果失败则继续</li>
<li><code>always</code></li>
<li><code>never</code></li>
</ul></dd><dt id="uv-publish--username"><a href="#uv-publish--username"><code>--username</code></a>, <code>-u</code> <i>username</i></dt><dd><p>上传的用户名</p>
<p>也可通过 <code>UV_PUBLISH_USERNAME</code> 环境变量设置。</p></dd><dt id="uv-publish--verbose"><a href="#uv-publish--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv cache

管理 uv 的缓存

<h3 class="cli-reference">用法</h3>

```
uv cache [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-cache-clean"><code>uv cache clean</code></a></dt><dd><p>清除缓存，移除所有条目或与特定包关联的条目</p></dd>
<dt><a href="#uv-cache-prune"><code>uv cache prune</code></a></dt><dd><p>从缓存中修剪所有无法访问的对象</p></dd>
<dt><a href="#uv-cache-dir"><code>uv cache dir</code></a></dt><dd><p>显示缓存目录</p></dd>
<dt><a href="#uv-cache-size"><code>uv cache size</code></a></dt><dd><p>显示缓存大小</p></dd>
</dl>

### uv cache clean

清除缓存，移除所有条目或与特定包关联的条目

<h3 class="cli-reference">用法</h3>

```
uv cache clean [OPTIONS] [PACKAGE]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-cache-clean--package"><a href="#uv-cache-clean--package"<code>PACKAGE</code></a></dt><dd><p>要从缓存中移除的包</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-cache-clean--allow-insecure-host"><a href="#uv-cache-clean--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--cache-dir"><a href="#uv-cache-clean--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--color"><a href="#uv-cache-clean--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-cache-clean--config-file"><a href="#uv-cache-clean--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--directory"><a href="#uv-cache-clean--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--force"><a href="#uv-cache-clean--force"><code>--force</code></a></dt><dd><p>强制移除缓存，忽略使用中检查。</p>
<p>默认情况下，<code>uv cache clean</code> 将阻塞直到没有进程正在读取缓存。当使用 <code>--force</code> 时，<code>uv cache clean</code> 将在不获取锁的情况下继续。</p>
</dd><dt id="uv-cache-clean--help"><a href="#uv-cache-clean--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-cache-clean--managed-python"><a href="#uv-cache-clean--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--native-tls"><a href="#uv-cache-clean--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--no-cache"><a href="#uv-cache-clean--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--no-config"><a href="#uv-cache-clean--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--no-managed-python"><a href="#uv-cache-clean--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--no-progress"><a href="#uv-cache-clean--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--no-python-downloads"><a href="#uv-cache-clean--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-cache-clean--offline"><a href="#uv-cache-clean--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--project"><a href="#uv-cache-clean--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-cache-clean--quiet"><a href="#uv-cache-clean--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-cache-clean--verbose"><a href="#uv-cache-clean--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv cache prune

从缓存中修剪所有无法访问的对象

<h3 class="cli-reference">用法</h3>

```
uv cache prune [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-cache-prune--allow-insecure-host"><a href="#uv-cache-prune--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--cache-dir"><a href="#uv-cache-prune--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--ci"><a href="#uv-cache-prune--ci"><code>--ci</code></a></dt><dd><p>针对持续集成环境（如 GitHub Actions）中的持久性优化缓存。</p>
<p>默认情况下，uv 会缓存它从源码构建的 wheel 以及它直接下载的预构建 wheel，以实现高性能的包安装。但在某些场景下，持久化预构建 wheel 可能是不希望的。例如，在 GitHub Actions 中，从缓存中省略预构建 wheel 并在每次运行时重新下载它们会更快。然而，缓存从源码构建的 wheel 通常更快，因为 wheel 构建过程可能很昂贵，特别是对于扩展模块。</p>
<p>在 <code>--ci</code> 模式下，uv 将从缓存中修剪任何预构建的 wheel，但保留从源码构建的任何 wheel。</p>
</dd><dt id="uv-cache-prune--color"><a href="#uv-cache-prune--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-cache-prune--config-file"><a href="#uv-cache-prune--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--directory"><a href="#uv-cache-prune--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--force"><a href="#uv-cache-prune--force"><code>--force</code></a></dt><dd><p>强制移除缓存，忽略使用中检查。</p>
<p>默认情况下，<code>uv cache prune</code> 将阻塞直到没有进程正在读取缓存。当使用 <code>--force</code> 时，<code>uv cache prune</code> 将在不获取锁的情况下继续。</p>
</dd><dt id="uv-cache-prune--help"><a href="#uv-cache-prune--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-cache-prune--managed-python"><a href="#uv-cache-prune--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--native-tls"><a href="#uv-cache-prune--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--no-cache"><a href="#uv-cache-prune--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--no-config"><a href="#uv-cache-prune--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--no-managed-python"><a href="#uv-cache-prune--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--no-progress"><a href="#uv-cache-prune--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--no-python-downloads"><a href="#uv-cache-prune--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-cache-prune--offline"><a href="#uv-cache-prune--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--project"><a href="#uv-cache-prune--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-cache-prune--quiet"><a href="#uv-cache-prune--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-cache-prune--verbose"><a href="#uv-cache-prune--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv cache dir

显示缓存目录。

默认情况下，缓存存储在 Unix 上的 `$XDG_CACHE_HOME/uv` 或 `$HOME/.cache/uv`，以及 Windows 上的 `%LOCALAPPDATA%\uv\cache`。

当使用 `--no-cache` 时，缓存存储在临时目录中，并在进程退出时丢弃。

可以通过 `cache-dir` 设置、`--cache-dir` 选项或 `$UV_CACHE_DIR` 环境变量指定替代缓存目录。

请注意，为了性能，缓存目录位于 uv 正在操作的 Python 环境所在的同一文件系统上非常重要。

<h3 class="cli-reference">用法</h3>

```
uv cache dir [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-cache-dir--allow-insecure-host"><a href="#uv-cache-dir--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--cache-dir"><a href="#uv-cache-dir--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--color"><a href="#uv-cache-dir--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-cache-dir--config-file"><a href="#uv-cache-dir--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--directory"><a href="#uv-cache-dir--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--help"><a href="#uv-cache-dir--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-cache-dir--managed-python"><a href="#uv-cache-dir--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--native-tls"><a href="#uv-cache-dir--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--no-cache"><a href="#uv-cache-dir--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--no-config"><a href="#uv-cache-dir--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--no-managed-python"><a href="#uv-cache-dir--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--no-progress"><a href="#uv-cache-dir--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--no-python-downloads"><a href="#uv-cache-dir--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-cache-dir--offline"><a href="#uv-cache-dir--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--project"><a href="#uv-cache-dir--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-cache-dir--quiet"><a href="#uv-cache-dir--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-cache-dir--verbose"><a href="#uv-cache-dir--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv cache size

显示缓存大小。

显示缓存目录的总大小。这包括所有下载和构建的 wheel、源码分发和其他缓存数据。默认情况下，以原始字节输出大小；使用 `--human` 获取人类可读的输出。

<h3 class="cli-reference">用法</h3>

```
uv cache size [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-cache-size--allow-insecure-host"><a href="#uv-cache-size--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-cache-size--cache-dir"><a href="#uv-cache-size--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-cache-size--color"><a href="#uv-cache-size--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-cache-size--config-file"><a href="#uv-cache-size--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-cache-size--directory"><a href="#uv-cache-size--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-cache-size--help"><a href="#uv-cache-size--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-cache-size--human"><a href="#uv-cache-size--human"><code>--human</code></a>, <code>--human-readable</code>, <code>-H</code></dt><dd><p>以人类可读格式显示缓存大小（例如，<code>1.2 GiB</code> 而不是原始字节）</p>
</dd><dt id="uv-cache-size--managed-python"><a href="#uv-cache-size--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-size--native-tls"><a href="#uv-cache-size--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-cache-size--no-cache"><a href="#uv-cache-size--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-cache-size--no-config"><a href="#uv-cache-size--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-cache-size--no-managed-python"><a href="#uv-cache-size--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-cache-size--no-progress"><a href="#uv-cache-size--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-cache-size--no-python-downloads"><a href="#uv-cache-size--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-cache-size--offline"><a href="#uv-cache-size--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-cache-size--project"><a href="#uv-cache-size--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-cache-size--quiet"><a href="#uv-cache-size--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-cache-size--verbose"><a href="#uv-cache-size--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv self

管理 uv 可执行文件

<h3 class="cli-reference">用法</h3>

```
uv self [OPTIONS] <COMMAND>
```

<h3 class="cli-reference">命令</h3>

<dl class="cli-reference"><dt><a href="#uv-self-update"><code>uv self update</code></a></dt><dd><p>更新 uv</p></dd>
<dt><a href="#uv-self-version"><code>uv self version</code></a></dt><dd><p>显示 uv 的版本</p></dd>
</dl>

### uv self update

更新 uv

<h3 class="cli-reference">用法</h3>

```
uv self update [OPTIONS] [TARGET_VERSION]
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-self-update--target_version"><a href="#uv-self-update--target_version"<code>TARGET_VERSION</code></a></dt><dd><p>更新到指定版本。如果未提供，uv 将更新到最新版本</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-self-update--allow-insecure-host"><a href="#uv-self-update--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-self-update--cache-dir"><a href="#uv-self-update--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-self-update--color"><a href="#uv-self-update--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-self-update--config-file"><a href="#uv-self-update--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-self-update--directory"><a href="#uv-self-update--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-self-update--dry-run"><a href="#uv-self-update--dry-run"><code>--dry-run</code></a></dt><dd><p>运行但不执行更新</p>
</dd><dt id="uv-self-update--help"><a href="#uv-self-update--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-self-update--managed-python"><a href="#uv-self-update--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-self-update--native-tls"><a href="#uv-self-update--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-self-update--no-cache"><a href="#uv-self-update--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-self-update--no-config"><a href="#uv-self-update--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-self-update--no-managed-python"><a href="#uv-self-update--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-self-update--no-progress"><a href="#uv-self-update--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-self-update--no-python-downloads"><a href="#uv-self-update--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-self-update--offline"><a href="#uv-self-update--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-self-update--project"><a href="#uv-self-update--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-self-update--quiet"><a href="#uv-self-update--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-self-update--token"><a href="#uv-self-update--token"><code>--token</code></a> <i>token</i></dt><dd><p>用于身份验证的 GitHub 令牌。不需要令牌，但使用令牌可以减少遇到速率限制的机会</p>
<p>也可通过 <code>UV_GITHUB_TOKEN</code> 环境变量设置。</p></dd><dt id="uv-self-update--verbose"><a href="#uv-self-update--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

### uv self version

显示 uv 的版本

<h3 class="cli-reference">用法</h3>

```
uv self version [OPTIONS]
```

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-self-version--allow-insecure-host"><a href="#uv-self-version--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-self-version--cache-dir"><a href="#uv-self-version--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-self-version--color"><a href="#uv-self-version--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-self-version--config-file"><a href="#uv-self-version--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-self-version--directory"><a href="#uv-self-version--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-self-version--help"><a href="#uv-self-version--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-self-version--managed-python"><a href="#uv-self-version--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-self-version--native-tls"><a href="#uv-self-version--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-self-version--no-cache"><a href="#uv-self-version--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-self-version--no-config"><a href="#uv-self-version--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-self-version--no-managed-python"><a href="#uv-self-version--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-self-version--no-progress"><a href="#uv-self-version--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-self-version--no-python-downloads"><a href="#uv-self-version--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-self-version--offline"><a href="#uv-self-version--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-self-version--output-format"><a href="#uv-self-version--output-format"><code>--output-format</code></a> <i>output-format</i></dt><dt id="uv-self-version--project"><a href="#uv-self-version--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-self-version--quiet"><a href="#uv-self-version--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-self-version--short"><a href="#uv-self-version--short"><code>--short</code></a></dt><dd><p>仅打印版本</p>
</dd><dt id="uv-self-version--verbose"><a href="#uv-self-version--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>

## uv generate-shell-completion

生成 shell 补全

<h3 class="cli-reference">用法</h3>

```
uv generate-shell-completion [OPTIONS] <SHELL>
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-generate-shell-completion--shell"><a href="#uv-generate-shell-completion--shell"<code>SHELL</code></a></dt><dd><p>要为其生成补全脚本的 shell</p>
</dd></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-generate-shell-completion--allow-insecure-host"><a href="#uv-generate-shell-completion--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-generate-shell-completion--directory"><a href="#uv-generate-shell-completion--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-generate-shell-completion--managed-python"><a href="#uv-generate-shell-completion--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-generate-shell-completion--no-managed-python"><a href="#uv-generate-shell-completion--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-generate-shell-completion--project"><a href="#uv-generate-shell-completion--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd></dl>

## uv help

显示命令的文档

<h3 class="cli-reference">用法</h3>

```
uv help [OPTIONS] [COMMAND]...
```

<h3 class="cli-reference">参数</h3>

<dl class="cli-reference"><dt id="uv-help--command"><a href="#uv-help--command"<code>COMMAND</code></a></dt></dl>

<h3 class="cli-reference">选项</h3>

<dl class="cli-reference"><dt id="uv-help--allow-insecure-host"><a href="#uv-help--allow-insecure-host"><code>--allow-insecure-host</code></a>, <code>--trusted-host</code> <i>allow-insecure-host</i></dt><dd><p>允许与主机的不安全连接。</p>
<p>可以多次提供。</p>
<p>期望接收主机名（例如 <code>localhost</code>）、主机-端口对（例如 <code>localhost:8080</code>）或 URL（例如 <code>https://localhost</code>）。</p>
<p>警告：包含在此列表中的主机将不会根据系统的证书存储进行验证。仅在具有已验证来源的安全网络中使用 <code>--allow-insecure-host</code>，因为它会绕过 SSL 验证，可能使您遭受中间人攻击。</p>
<p>也可通过 <code>UV_INSECURE_HOST</code> 环境变量设置。</p></dd><dt id="uv-help--cache-dir"><a href="#uv-help--cache-dir"><code>--cache-dir</code></a> <i>cache-dir</i></dt><dd><p>缓存目录的路径。</p>
<p>在 macOS 和 Linux 上默认为 <code>$XDG_CACHE_HOME/uv</code> 或 <code>$HOME/.cache/uv</code>，在 Windows 上默认为 <code>%LOCALAPPDATA%\uv\cache</code>。</p>
<p>要查看缓存目录的位置，请运行 <code>uv cache dir</code>。</p>
<p>也可通过 <code>UV_CACHE_DIR</code> 环境变量设置。</p></dd><dt id="uv-help--color"><a href="#uv-help--color"><code>--color</code></a> <i>color-choice</i></dt><dd><p>控制输出中颜色的使用。</p>
<p>默认情况下，当写入终端时，uv 会自动检测对颜色的支持。</p>
<p>可能的值：</p>
<ul>
<li><code>auto</code>:  仅当输出到具有支持的终端或 TTY 时启用彩色输出</li>
<li><code>always</code>:  无论检测到的环境如何，都启用彩色输出</li>
<li><code>never</code>:  禁用彩色输出</li>
</ul></dd><dt id="uv-help--config-file"><a href="#uv-help--config-file"><code>--config-file</code></a> <i>config-file</i></dt><dd><p>用于配置的 <code>uv.toml</code> 文件的路径。</p>
<p>虽然 uv 配置可以包含在 <code>pyproject.toml</code> 文件中，但在此上下文中不允许。</p>
<p>也可通过 <code>UV_CONFIG_FILE</code> 环境变量设置。</p></dd><dt id="uv-help--directory"><a href="#uv-help--directory"><code>--directory</code></a> <i>directory</i></dt><dd><p>在运行命令之前切换到给定目录。</p>
<p>相对路径以给定目录为基目录进行解析。</p>
<p>请参阅 <code>--project</code> 仅更改项目根目录。</p>
<p>也可通过 <code>UV_WORKING_DIRECTORY</code> 环境变量设置。</p></dd><dt id="uv-help--help"><a href="#uv-help--help"><code>--help</code></a>, <code>-h</code></dt><dd><p>显示此命令的简明帮助</p>
</dd><dt id="uv-help--managed-python"><a href="#uv-help--managed-python"><code>--managed-python</code></a></dt><dd><p>要求使用 uv 管理的 Python 版本。</p>
<p>默认情况下，uv 优先使用它管理的 Python 版本。但是，如果未安装 uv 管理的 Python，它将使用系统 Python 版本。此选项禁用系统 Python 版本的使用。</p>
<p>也可通过 <code>UV_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-help--native-tls"><a href="#uv-help--native-tls"><code>--native-tls</code></a></dt><dd><p>是否从平台的本地证书存储加载 TLS 证书。</p>
<p>默认情况下，uv 从捆绑的 <code>webpki-roots</code> crate 加载证书。<code>webpki-roots</code> 是来自 Mozilla 的一组可靠信任根，将它们包含在 uv 中提高了可移植性和性能（尤其是在 macOS 上）。</p>
<p>但是，在某些情况下，您可能希望使用平台的本地证书存储，特别是当您依赖包含在系统证书存储中的公司信任根（例如，用于强制代理）时。</p>
<p>也可通过 <code>UV_NATIVE_TLS</code> 环境变量设置。</p></dd><dt id="uv-help--no-cache"><a href="#uv-help--no-cache"><code>--no-cache</code></a>, <code>--no-cache-dir</code>, <code>-n</code></dt><dd><p>避免读写缓存，而是在操作期间使用临时目录</p>
<p>也可通过 <code>UV_NO_CACHE</code> 环境变量设置。</p></dd><dt id="uv-help--no-config"><a href="#uv-help--no-config"><code>--no-config</code></a></dt><dd><p>避免发现配置文件（<code>pyproject.toml</code>、<code>uv.toml</code>）。</p>
<p>通常，配置文件会在当前目录、父目录或用户配置目录中被发现。</p>
<p>也可通过 <code>UV_NO_CONFIG</code> 环境变量设置。</p></dd><dt id="uv-help--no-managed-python"><a href="#uv-help--no-managed-python"><code>--no-managed-python</code></a></dt><dd><p>禁用使用 uv 管理的 Python 版本。</p>
<p>相反，uv 将在系统上搜索合适的 Python 版本。</p>
<p>也可通过 <code>UV_NO_MANAGED_PYTHON</code> 环境变量设置。</p></dd><dt id="uv-help--no-pager"><a href="#uv-help--no-pager"><code>--no-pager</code></a></dt><dd><p>打印帮助时禁用分页器</p>
</dd><dt id="uv-help--no-progress"><a href="#uv-help--no-progress"><code>--no-progress</code></a></dt><dd><p>隐藏所有进度输出。</p>
<p>例如，旋转器或进度条。</p>
<p>也可通过 <code>UV_NO_PROGRESS</code> 环境变量设置。</p></dd><dt id="uv-help--no-python-downloads"><a href="#uv-help--no-python-downloads"><code>--no-python-downloads</code></a></dt><dd><p>禁用 Python 的自动下载。</p>
</dd><dt id="uv-help--offline"><a href="#uv-help--offline"><code>--offline</code></a></dt><dd><p>禁用网络访问。</p>
<p>禁用后，uv 将仅使用本地缓存的数据和本地可用的文件。</p>
<p>也可通过 <code>UV_OFFLINE</code> 环境变量设置。</p></dd><dt id="uv-help--project"><a href="#uv-help--project"><code>--project</code></a> <i>project</i></dt><dd><p>在给定的项目目录中运行命令。</p>
<p>所有 <code>pyproject.toml</code>、<code>uv.toml</code> 和 <code>.python-version</code> 文件将通过从项目根目录向上遍历目录树来发现，项目的虚拟环境（<code>.venv</code>）也是如此。</p>
<p>其他命令行参数（例如相对路径）将相对于当前工作目录进行解析。</p>
<p>请参阅 <code>--directory</code> 以完全更改工作目录。</p>
<p>在 <code>uv pip</code> 接口中使用时，此设置无效。</p>
<p>也可通过 <code>UV_PROJECT</code> 环境变量设置。</p></dd><dt id="uv-help--quiet"><a href="#uv-help--quiet"><code>--quiet</code></a>, <code>-q</code></dt><dd><p>使用安静输出。</p>
<p>重复此选项，例如 <code>-qq</code>，将启用静默模式，在该模式下 uv 不会向 stdout 写入任何输出。</p>
</dd><dt id="uv-help--verbose"><a href="#uv-help--verbose"><code>--verbose</code></a>, <code>-v</code></dt><dd><p>使用详细输出。</p>
<p>您可以使用 <code>RUST_LOG</code> 环境变量配置细粒度日志记录。（<a href="https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives">https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html#directives</a>）</p>
</dd></dl>