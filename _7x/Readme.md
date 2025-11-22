# uv 中文网

# prompt
```
你是一个 python 和 rust 技术专家，你非常了解 python、rust 和 nodejs，帮我把该 uv 文档翻译成中文,注意 uv 是一个基于rust 开发的高性能 python 包管理和项目管理工具集，翻译要求：
- 保持 markdown 的格式不变，
- 不用翻译代码块
- Stability: 不翻译
- 不用翻译注释内容
- 不要翻译 yaml 块内容
- 不要翻译 ```包裹的 code 块中的内容
- 不要翻译 YAML Front Matter 部分

```

## 文档环境
To preview any changes to the documentation locally:

1. Install the [Rust toolchain](https://www.rust-lang.org/tools/install).

2. Run `cargo dev generate-all`, to update any auto-generated documentation.

3. Run the development server with:

   ```shell
   # For contributors.
   uvx --with-requirements docs/requirements.txt -- mkdocs serve -f mkdocs.public.yml

   # For members of the Astral org, which has access to MkDocs Insiders via sponsorship.
   uvx --with-requirements docs/requirements-insiders.txt -- mkdocs serve -f mkdocs.insiders.yml
   ```

The documentation should then be available locally at
[http://127.0.0.1:8000/uv/](http://127.0.0.1:8000/uv/).

4. 构建文档
   ```shell
     uvx --with-requirements docs/requirements.txt -- mkdocs build -f mkdocs.public.yml
   ```
   构建产物在 `site` 目录下


To update the documentation dependencies, edit `docs/requirements.in` and
`docs/requirements-insiders.in`, then run:

```shell
uv pip compile docs/requirements.in -o docs/requirements.txt --universal -p 3.12
uv pip compile docs/requirements-insiders.in -o docs/requirements-insiders.txt --universal -p 3.12
```


## 构建

serve
```
uvx --with-requirements docs/requirements.txt -- mkdocs serve  -f mkdocs.public.yml 
```

build
```
uvx --with-requirements docs/requirements.txt -- mkdocs build  -f mkdocs.public.yml 
```