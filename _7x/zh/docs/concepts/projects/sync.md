# 锁定与同步

锁定是将项目依赖项解析到[锁定文件](./layout.md#the-lockfile)的过程。同步是将锁定文件中的部分包安装到[项目环境](./layout.md#the-project-environment)的过程。

## 自动锁定与同步

在 uv 中，锁定和同步是*自动*进行的。例如，当使用 `uv run` 时，会在调用请求的命令之前锁定和同步项目。这确保了项目环境始终是最新的。类似地，读取锁定文件的命令（例如 `uv tree`）会在运行前自动更新锁定文件。

要禁用自动锁定，请使用 `--locked` 选项：

```console
$ uv run --locked ...
```

如果锁定文件不是最新的，uv 将引发错误而不是更新锁定文件。

要使用锁定文件而不检查它是否是最新的，请使用 `--frozen` 选项：

```console
$ uv run --frozen ...
```

类似地，要运行命令而不检查环境是否是最新的，请使用 `--no-sync` 选项：

```console
$ uv run --no-sync ...
```

## 检查锁定文件

在判断锁定文件是否为最新时，uv 会检查它是否与项目元数据匹配。例如，如果你向 `pyproject.toml` 添加了一个依赖项，锁定文件将被视为过时。类似地，如果你更改了某个依赖项的版本约束，使得锁定的版本被排除在外，锁定文件也将被视为过时。但是，如果你更改版本约束后，现有的锁定版本仍然在约束范围内，则锁定文件仍将被视为是最新的。

你可以通过向 `uv lock` 传递 `--check` 标志来检查锁定文件是否为最新：

```console
$ uv lock --check
```

这等效于其他命令的 `--locked` 标志。

!!! important

    当有新版本的包发布时，uv 不会认为锁定文件过时 —— 如果你想升级依赖项，需要显式更新锁定文件。有关详细信息，请参阅[升级锁定的包版本](#upgrading-locked-package-versions)的文档。

## 创建锁定文件

虽然锁定文件是[自动](#automatic-lock-and-sync)创建的，但也可以使用 `uv lock` 显式创建或更新锁定文件：

```console
$ uv lock
```

## 同步环境

虽然环境是[自动](#automatic-lock-and-sync)同步的，但也可以使用 `uv sync` 显式同步环境：

```console
$ uv sync
```

手动同步环境对于确保编辑器具有正确版本的依赖项特别有用。

### 可编辑安装

当环境同步时，uv 会将项目（以及其他工作区成员）作为*可编辑*包安装，这样在环境反映更改时就不需要重新同步。

要选择退出此行为，请使用 `--no-editable` 选项。

!!! note

    如果项目未定义构建系统，则不会被安装。有关详细信息，请参阅[构建系统](./config.md#build-systems)文档。

### 保留无关包

默认情况下，同步是"精确的"，这意味着它将删除锁定文件中不存在的任何包。

要保留无关包，请使用 `--inexact` 选项：

```console
$ uv sync --inexact
```

### 同步可选依赖项

uv 从 `[project.optional-dependencies]` 表中读取可选依赖项。这些通常被称为"extras"。

默认情况下，uv 不会同步 extras。使用 `--extra` 选项来包含一个 extra。

```console
$ uv sync --extra foo
```

要快速启用所有 extras，请使用 `--all-extras` 选项。

有关如何管理可选依赖项的详细信息，请参阅[可选依赖项](./dependencies.md#optional-dependencies)文档。

### 同步开发依赖项

uv 从 `[dependency-groups]` 表（根据 [PEP 735](https://peps.python.org/pep-0735/) 定义）中读取开发依赖项。

`dev` 组是特殊情况，默认情况下会被同步。有关更改默认值的详细信息，请参阅[默认组](./dependencies.md#default-groups)文档。

可以使用 `--no-dev` 标志来排除 `dev` 组。

可以使用 `--only-dev` 标志来*仅*安装 `dev` 组，*而不*安装项目及其依赖项。

可以使用 `--all-groups`、`--no-default-groups`、`--group <name>`、`--only-group <name>` 和 `--no-group <name>` 选项来包含或排除其他组。`--only-group` 的语义与 `--only-dev` 相同，项目将不会被包含。但是，`--only-group` 也会排除默认组。

组的排除总是优先于包含，因此给定命令：

```
$ uv sync --no-group foo --group foo
```

`foo` 组将不会被安装。

有关如何管理开发依赖项的详细信息，请参阅[开发依赖项](./dependencies.md#development-dependencies)文档。

## 升级锁定的包版本

对于已存在的 `uv.lock` 文件，在运行 `uv sync` 和 `uv lock` 时，uv 将优先使用先前锁定的包版本。只有当项目的依赖项约束排除了先前锁定的版本时，包版本才会更改。

要升级所有包：

```console
$ uv lock --upgrade
```

要将单个包升级到最新版本，同时保留所有其他包的锁定版本：

```console
$ uv lock --upgrade-package <package>
```

要将单个包升级到特定版本：

```console
$ uv lock --upgrade-package <package>==<version>
```

在所有情况下，升级都受限于项目的依赖项约束。例如，如果项目为某个包定义了上限版本，则升级不会超过该版本。

!!! note

    uv 对 Git 依赖项应用了类似的逻辑。例如，如果一个 Git 依赖项引用了 `main` 分支，在现有的 `uv.lock` 文件中，uv 将优先使用锁定的提交 SHA，而不是 `main` 分支上的最新提交，除非使用了 `--upgrade` 或 `--upgrade-package` 标志。

这些标志也可以提供给 `uv sync` 或 `uv run`，以更新锁定文件*和*环境。

## 导出锁定文件

如果你需要将 uv 与其他工具或工作流集成，可以使用 `uv export --format requirements-txt` 将 `uv.lock` 导出为 `requirements.txt` 格式。生成的 `requirements.txt` 文件可以通过 `uv pip install` 或其他工具（如 `pip`）进行安装。

通常，我们不建议同时使用 `uv.lock` 和 `requirements.txt` 文件。如果你发现自己需要导出 `uv.lock` 文件，请考虑开一个 issue 来讨论你的使用场景。

## 部分安装

有时分多个步骤执行安装会很有帮助，例如，在构建 Docker 镜像时为了优化层缓存。为此，`uv sync` 提供了几个标志。

- `--no-install-project`: 不安装当前项目
- `--no-install-workspace`: 不安装任何工作区成员，包括根项目
- `--no-install-package <NO_INSTALL_PACKAGE>`: 不安装给定的包

当使用这些选项时，目标的所有依赖项仍然会被安装。例如，`--no-install-project` 将*省略项目*，但不会省略其任何依赖项。

如果使用不当，这些标志可能导致环境损坏，因为某个包可能缺少其依赖项。