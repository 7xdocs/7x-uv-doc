# 功能特性

uv 为 Python 开发提供核心功能——从安装 Python 和编写简单脚本，到支持多 Python 版本和多平台的大型项目开发。

uv 的接口可以划分为几个部分，这些部分既可以独立使用，也可以组合使用。

## Python 版本

安装和管理 Python 本身。

- `uv python install`: 安装 Python 版本。
- `uv python list`: 查看可用的 Python 版本。
- `uv python find`: 查找已安装的 Python 版本。
- `uv python pin`: 将当前项目固定使用特定的 Python 版本。
- `uv python uninstall`: 卸载 Python 版本。

请参阅 [安装 Python 指南](../guides/install-python.md) 开始使用。

## 脚本

执行独立的 Python 脚本，例如 `example.py`。

- `uv run`: 运行脚本。
- `uv add --script`: 为脚本添加依赖。
- `uv remove --script`: 从脚本移除依赖。

请参阅 [运行脚本指南](../guides/scripts.md) 开始使用。

## 项目

创建和处理 Python 项目（即包含 `pyproject.toml` 的项目）。

- `uv init`: 创建新的 Python 项目。
- `uv add`: 为项目添加依赖。
- `uv remove`: 从项目移除依赖。
- `uv sync`: 将项目依赖与环境同步。
- `uv lock`: 为项目依赖创建锁文件。
- `uv run`: 在项目环境中运行命令。
- `uv tree`: 查看项目的依赖树。
- `uv build`: 将项目构建为分发包。
- `uv publish`: 将项目发布到包索引。

请参阅 [项目指南](../guides/projects.md) 开始使用。

## 工具

运行和安装发布到 Python 包索引的工具，例如 `ruff` 或 `black`。

- `uvx` / `uv tool run`: 在临时环境中运行工具。
- `uv tool install`: 为用户全局安装工具。
- `uv tool uninstall`: 卸载工具。
- `uv tool list`: 列出已安装的工具。
- `uv tool update-shell`: 更新 Shell 以包含工具可执行文件。

请参阅 [工具指南](../guides/tools.md) 开始使用。

## pip 接口

手动管理环境和包——旨在用于遗留工作流或高级命令无法提供足够控制的情况。

创建虚拟环境（替代 `venv` 和 `virtualenv`）：

- `uv venv`: 创建新的虚拟环境。

有关详细信息，请参阅 [使用环境](../pip/environments.md) 文档。

管理环境中的包（替代 [`pip`](https://github.com/pypa/pip) 和 [`pipdeptree`](https://github.com/tox-dev/pipdeptree)）：

- `uv pip install`: 将包安装到当前环境中。
- `uv pip show`: 显示已安装包的详细信息。
- `uv pip freeze`: 列出已安装的包及其版本。
- `uv pip check`: 检查当前环境中的包是否兼容。
- `uv pip list`: 列出已安装的包。
- `uv pip uninstall`: 卸载包。
- `uv pip tree`: 查看环境的依赖树。

有关详细信息，请参阅 [管理包](../pip/packages.md) 文档。

锁定环境中的包（替代 [`pip-tools`](https://github.com/jazzband/pip-tools)）：

- `uv pip compile`: 将需求文件编译为锁文件。
- `uv pip sync`: 使用锁文件同步环境。

有关详细信息，请参阅 [锁定环境](../pip/compile.md) 文档。

!!! important

    这些命令并不完全实现其所基于工具的接口和行为。偏离常见工作流越远，越可能遇到差异。详情请查阅 [pip 兼容性指南](../pip/compatibility.md)。

## 实用工具

管理和检查 uv 的状态，例如缓存、存储目录或执行自我更新：

- `uv cache clean`: 移除缓存条目。
- `uv cache prune`: 移除过时的缓存条目。
- `uv cache dir`: 显示 uv 缓存目录路径。
- `uv tool dir`: 显示 uv 工具目录路径。
- `uv python dir`: 显示 uv 安装的 Python 版本路径。
- `uv self update`: 将 uv 更新到最新版本。

## 后续步骤

阅读 [指南](../guides/index.md) 以了解每个功能的介绍，查看 [概念](../concepts/index.md) 页面以获取 uv 功能的深入细节，或者在遇到问题时学习如何 [获取帮助](./help.md)。