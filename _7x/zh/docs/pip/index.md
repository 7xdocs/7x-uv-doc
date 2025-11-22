# pip 接口

uv 为常见的 `pip`、`pip-tools` 和 `virtualenv` 命令提供了一个直接替代品。这些命令直接与虚拟环境交互，这与 uv 自动管理虚拟环境的主要接口形成对比。`uv pip` 接口将 uv 的速度和功能暴露给那些尚未准备好从 `pip` 和 `pip-tools` 迁移过来的高级用户和项目。

以下部分讨论了使用 `uv pip` 的基础知识：

- [创建和使用环境](./environments.md)
- [安装和管理包](./packages.md)
- [检查环境和包](./inspection.md)
- [声明包依赖项](./dependencies.md)
- [锁定和同步环境](./compile.md)

请注意，这些命令并不*完全*实现它们所基于工具的接口和行为。您偏离常见工作流程越远，就越有可能遇到差异。详情请参阅 [pip 兼容性指南](./compatibility.md)。

!!! important

    uv 不依赖也不调用 pip。将其命名为 pip 接口是为了突出其专门目的，即提供与 pip 接口匹配的低级命令，并将其与 uv 其他在更高抽象级别上操作的命令区分开来。