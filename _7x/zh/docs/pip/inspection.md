# 环境检查

## 列出已安装的包

列出环境中所有的包：

```console
$ uv pip list
```

以 JSON 格式列出包：

```console
$ uv pip list --format json
```

以 `requirements.txt` 格式列出环境中所有的包：

```console
$ uv pip freeze
```

## 检查包信息

显示已安装包的信息，例如 `numpy`：

```console
$ uv pip show numpy
```

可以同时检查多个包。

## 验证环境

如果分多个步骤安装包，可能会将存在冲突要求的包安装到同一环境中。

检查环境中的依赖冲突或缺失问题：

```console
$ uv pip check
```