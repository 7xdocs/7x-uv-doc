# 安装 uv

## 安装方法

使用我们提供的独立安装程序或您选择的包管理器来安装 uv。

### 独立安装程序

uv 提供了一个独立的安装程序来下载和安装：

=== "macOS 和 Linux"

    使用 `curl` 下载脚本并使用 `sh` 执行：

    ```console
    $ curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

    如果您的系统没有 `curl`，可以使用 `wget`：

    ```console
    $ wget -qO- https://astral.sh/uv/install.sh | sh
    ```

    通过在 URL 中包含版本号来请求特定版本：

    ```console
    $ curl -LsSf https://astral.sh/uv/0.9.10/install.sh | sh
    ```

=== "Windows"

    使用 `irm` 下载脚本并使用 `iex` 执行：

    ```pwsh-session
    PS> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```

    更改[执行策略](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4#powershell-execution-policies)允许运行来自互联网的脚本。

    通过在 URL 中包含版本号来请求特定版本：

    ```pwsh-session
    PS> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/0.9.10/install.ps1 | iex"
    ```

!!! 提示

    安装脚本可以在使用前进行检查：

    === "macOS 和 Linux"

        ```console
        $ curl -LsSf https://astral.sh/uv/install.sh | less
        ```

    === "Windows"

        ```pwsh-session
        PS> powershell -c "irm https://astral.sh/uv/install.ps1 | more"
        ```

    或者，可以直接从 [GitHub](#github-releases) 下载安装程序或二进制文件。

有关自定义 uv 安装的详细信息，请参阅[安装程序](../reference/installer.md)的参考文档。

### PyPI

为了方便起见，uv 已发布到 [PyPI](https://pypi.org/project/uv/)。

如果从 PyPI 安装，我们建议将 uv 安装到隔离的环境中，例如使用 `pipx`：

```console
$ pipx install uv
```

当然，也可以使用 `pip`：

```console
$ pip install uv
```

!!! 注意

    uv 为许多平台提供了预构建的发行版（wheel）；如果某个平台没有可用的 wheel，uv 将从源代码构建，这需要 Rust 工具链。有关从源代码构建 uv 的详细信息，请参阅[贡献设置指南](https://github.com/astral-sh/uv/blob/main/CONTRIBUTING.md#setup)。

### Homebrew

uv 在 Homebrew 核心包中可用。

```console
$ brew install uv
```

### MacPorts

uv 可通过 [MacPorts](https://ports.macports.org/port/uv/) 获取。

```console
$ sudo port install uv
```

### WinGet

uv 可通过 [WinGet](https://winstall.app/apps/astral-sh.uv) 获取。

```console
$ winget install --id=astral-sh.uv  -e
```

### Scoop

uv 可通过 [Scoop](https://scoop.sh/#/apps?q=uv) 获取。

```console
$ scoop install main/uv
```

### Docker

uv 在 [`ghcr.io/astral-sh/uv`](https://github.com/astral-sh/uv/pkgs/container/uv) 提供了 Docker 镜像。

有关更多详细信息，请参阅我们在 [Docker 中使用 uv](../guides/integration/docker.md) 的指南。

### GitHub Releases

uv 的发布构件可以直接从 [GitHub Releases](https://github.com/astral-sh/uv/releases) 下载。

每个发布页面都包含所有支持平台的二进制文件，以及通过 `github.com` 而非 `astral.sh` 使用独立安装程序的说明。

### Cargo

uv 可以通过 Cargo 获取，但由于其依赖未发布的 crate，必须从 Git 构建，而不是从 [crates.io](https://crates.io) 安装。

```console
$ cargo install --git https://github.com/astral-sh/uv uv
```

!!! 注意

    此方法从源代码构建 uv，需要兼容的 Rust 工具链。

## 升级 uv

当 uv 通过独立安装程序安装时，它可以按需自我更新：

```console
$ uv self update
```

!!! 提示

    更新 uv 将重新运行安装程序，并可能修改您的 Shell 配置文件。要禁用此行为，请设置 `UV_NO_MODIFY_PATH=1`。

当使用其他安装方法时，自我更新功能被禁用。请改用包管理器的升级方法。例如，使用 `pip`：

```console
$ pip install --upgrade uv
```

## Shell 自动补全

!!! 提示

    您可以运行 `echo $SHELL` 来帮助确定您使用的 Shell。

要为 uv 命令启用 Shell 自动补全，请运行以下命令之一：

=== "Bash"

    ```bash
    echo 'eval "$(uv generate-shell-completion bash)"' >> ~/.bashrc
    ```

=== "Zsh"

    ```bash
    echo 'eval "$(uv generate-shell-completion zsh)"' >> ~/.zshrc
    ```

=== "fish"

    ```bash
    echo 'uv generate-shell-completion fish | source' > ~/.config/fish/completions/uv.fish
    ```

=== "Elvish"

    ```bash
    echo 'eval (uv generate-shell-completion elvish | slurp)' >> ~/.elvish/rc.elv
    ```

=== "PowerShell / pwsh"

    ```powershell
    if (!(Test-Path -Path $PROFILE)) {
      New-Item -ItemType File -Path $PROFILE -Force
    }
    Add-Content -Path $PROFILE -Value '(& uv generate-shell-completion powershell) | Out-String | Invoke-Expression'
    ```

要为 uvx 启用 Shell 自动补全，请运行以下命令之一：

=== "Bash"

    ```bash
    echo 'eval "$(uvx --generate-shell-completion bash)"' >> ~/.bashrc
    ```

=== "Zsh"

    ```bash
    echo 'eval "$(uvx --generate-shell-completion zsh)"' >> ~/.zshrc
    ```

=== "fish"

    ```bash
    echo 'uvx --generate-shell-completion fish | source' > ~/.config/fish/completions/uvx.fish
    ```

=== "Elvish"

    ```bash
    echo 'eval (uvx --generate-shell-completion elvish | slurp)' >> ~/.elvish/rc.elv
    ```

=== "PowerShell / pwsh"

    ```powershell
    if (!(Test-Path -Path $PROFILE)) {
      New-Item -ItemType File -Path $PROFILE -Force
    }
    Add-Content -Path $PROFILE -Value '(& uvx --generate-shell-completion powershell) | Out-String | Invoke-Expression'
    ```

然后重启 Shell 或重新加载 Shell 配置文件。

## 卸载

如果您需要从系统中移除 uv，请按照以下步骤操作：

1.  清理存储的数据（可选）：

    ```console
    $ uv cache clean
    $ rm -r "$(uv python dir)"
    $ rm -r "$(uv tool dir)"
    ```

    !!! 提示

        在移除二进制文件之前，您可能希望移除 uv 存储的任何数据。有关 uv 存储数据位置的详细信息，请参阅[存储参考](../reference/storage.md)。

2.  移除 uv、uvx 和 uvw 二进制文件：

    === "macOS 和 Linux"

        ```console
        $ rm ~/.local/bin/uv ~/.local/bin/uvx
        ```

    === "Windows"

        ```pwsh-session
        PS> rm $HOME\.local\bin\uv.exe
        PS> rm $HOME\.local\bin\uvx.exe
        PS> rm $HOME\.local\bin\uvw.exe
        ```

    !!! 注意

        在 0.5.0 版本之前，uv 被安装到 `~/.cargo/bin`。可以从那里移除二进制文件来卸载。从旧版本升级不会自动移除 `~/.cargo/bin` 中的二进制文件。

## 后续步骤

请参阅[第一步](./first-steps.md)或直接跳转到[指南](../guides/index.md)开始使用 uv。