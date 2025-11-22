# 管理包

## 安装包

要将包安装到虚拟环境中，例如安装 Flask：

```console
$ uv pip install flask
```

要安装包并启用可选依赖项，例如安装 Flask 并包含 "dotenv" 额外功能：

```console
$ uv pip install "flask[dotenv]"
```

要安装多个包，例如 Flask 和 Ruff：

```console
$ uv pip install flask ruff
```

要安装具有版本约束的包，例如 Ruff v0.2.0 或更新版本：

```console
$ uv pip install 'ruff>=0.2.0'
```

要安装特定版本的包，例如 Ruff v0.3.0：

```console
$ uv pip install 'ruff==0.3.0'
```

要从磁盘安装包：

```console
$ uv pip install "ruff @ ./projects/ruff"
```

要从 GitHub 安装包：

```console
$ uv pip install "git+https://github.com/astral-sh/ruff"
```

要从 GitHub 安装特定引用（如标签、提交或分支）的包：

```console
$ # 安装一个标签
$ uv pip install "git+https://github.com/astral-sh/ruff@v0.2.0"

$ # 安装一个提交
$ uv pip install "git+https://github.com/astral-sh/ruff@1fadefa67b26508cc59cf38e6130bde2243c929d"

$ # 安装一个分支
$ uv pip install "git+https://github.com/astral-sh/ruff@main"
```

有关从私有仓库安装的信息，请参阅 [Git 认证](../concepts/authentication/git.md) 文档。

## 可编辑包

对于可编辑包，当其源代码发生更改时，无需重新安装即可生效。

将当前项目安装为可编辑包：

```console
$ uv pip install -e .
```

将其他目录中的项目安装为可编辑包：

```console
$ uv pip install -e "ruff @ ./project/ruff"
```

## 从文件安装包

可以从标准文件格式一次性安装多个包。

从 `requirements.txt` 文件安装：

```console
$ uv pip install -r requirements.txt
```

有关 `requirements.txt` 文件的更多信息，请参阅 [`uv pip compile`](./compile.md) 文档。

从 `pyproject.toml` 文件安装：

```console
$ uv pip install -r pyproject.toml
```

从 `pyproject.toml` 文件安装并启用可选依赖项，例如启用 "foo" 额外功能：

```console
$ uv pip install -r pyproject.toml --extra foo
```

从 `pyproject.toml` 文件安装并启用所有可选依赖项：

```console
$ uv pip install -r pyproject.toml --all-extras
```

要安装当前项目目录 `pyproject.toml` 中的依赖组，例如组 `foo`：

```console
$ uv pip install --group foo
```

要指定应从哪个项目目录获取依赖组：

```console
$ uv pip install --project some/path/ --group foo --group bar
```

或者，您可以为每个组指定一个 `pyproject.toml` 文件的路径：

```console
$ uv pip install --group some/path/pyproject.toml:foo --group other/pyproject.toml:bar
```

!!! note

    与 pip 类似，`--group` 标志不适用于通过其他标志（如 `-r` 或 `-e`）指定的源。
    例如，`uv pip install -r some/path/pyproject.toml --group foo` 会从 `./pyproject.toml` 获取组 `foo`，而**不是**从 `some/path/pyproject.toml` 获取。

## 卸载包

要卸载一个包，例如 Flask：

```console
$ uv pip uninstall flask
```

要卸载多个包，例如 Flask 和 Ruff：

```console
$ uv pip uninstall flask ruff
```