docs-server:
	cd zh
	uvx --with-requirements docs/requirements.txt -- mkdocs serve -f mkdocs.public.yml

docs-build:
	cd zh
	uvx --with-requirements docs/requirements.txt -- mkdocs build  -f mkdocs.public.yml 

docker-build:
	docker build  . --no-cache -t chrissong1994/7x-uv-v0.9-doc:latest --platform linux/amd64,linux/arm64