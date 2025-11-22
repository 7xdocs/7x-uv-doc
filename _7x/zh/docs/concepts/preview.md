# 预览功能

uv 提供了可选的预览功能，以便在向所有用户启用之前收集社区反馈，并增强对更改带来净收益的信心。

## 启用预览功能

要启用所有预览功能，请使用 `--preview` 标志：

```console
$ uv run --preview ...
```

或者，设置 `UV_PREVIEW` 环境变量：

```console
$ UV_PREVIEW=1 uv run ...
```

要启用特定的预览功能，请使用 `--preview-features` 标志：

```console
$ uv run --preview-features foo ...
```

可以重复使用 `--preview-features` 标志来启用多个功能：

```console
$ uv run --preview-features foo --preview-features bar ...
```

或者，功能可以在逗号分隔的列表中提供：

```console
$ uv run --preview-features foo,bar ...
```

`UV_PREVIEW_FEATURES` 环境变量可以类似地使用，例如：

```console
$ UV_PREVIEW_FEATURES=foo,bar uv run ...
```

为了向后兼容，启用不存在的预览功能会发出警告，但不会报错。

## 使用预览功能

通常，如果行为变更由某种用户交互控制，则无需更改任何预览设置即可使用预览功能。例如，在 `pylock.toml` 支持处于预览阶段时，您可以使用 `uv pip install` 和 `pylock.toml` 文件而无需额外配置，因为指定 `pylock.toml` 文件表明您希望使用该功能。但是，会显示一条警告，指出该功能处于预览状态。可以启用预览功能以消除此警告。

其他预览功能会更改行为，而无需您更改 uv 的使用方式。例如，当启用 `python-upgrade` 功能时，`uv python install` 的默认行为会发生改变，允许 uv 透明地升级 Python 版本。此功能需要启用预览标志才能正常使用。

## 可用的预览功能

以下预览功能可用：

- `add-bounds`：允许配置 [`uv add`](../reference/settings.md#add-bounds) 调用的默认边界。
- `json-output`：允许在各种 uv 命令中使用 `--output-format json`。
- `package-conflicts`：允许在包级别定义工作区冲突。
- `pylock`：允许从 `pylock.toml` 文件安装。
- `python-install-default`：允许[安装 `python` 和 `python3` 可执行文件](./python-versions.md#installing-python-executables)。
- `python-upgrade`：允许[透明升级 Python 版本](./python-versions.md#upgrading-python-versions)。
- `format`：允许使用 `uv format`。
- `native-auth`：允许在[系统原生位置](../concepts/authentication/http.md#the-uv-credentials-store)存储凭据。
- `workspace-metadata`：允许使用 `uv workspace metadata`。
- `workspace-dir`：允许使用 `uv workspace dir`。
- `workspace-list`：允许使用 `uv workspace list`。

## 禁用预览功能

可以使用 `--no-preview` 选项来禁用预览功能。