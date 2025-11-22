# 第三方服务

## 使用替代包索引进行认证

有关与流行的替代 Python 包索引进行认证的详细信息，请参阅[替代索引集成指南](../../guides/integration/alternative-indexes.md)。

## Hugging Face 支持

uv 支持对 Hugging Face Hub 进行自动认证。具体来说，如果设置了 `HF_TOKEN` 环境变量，uv 会将其传播到向 `huggingface.co` 发起的请求中。

这对于访问 Hugging Face Datasets 中的私有脚本特别有用。例如，您可以运行以下命令来执行来自私有数据集的脚本 `main.py`：

```console
$ HF_TOKEN=hf_... uv run https://huggingface.co/datasets/<user>/<name>/resolve/<branch>/main.py
```

您可以通过设置 `UV_NO_HF_TOKEN=1` 环境变量来禁用自动 Hugging Face 认证。