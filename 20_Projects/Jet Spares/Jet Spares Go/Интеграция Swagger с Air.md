---
up:
  - "[[Jet Spares Go]]"
related: "[[Swagger]]"
created: 2025-03-30
---
Чтобы air умел обновлять доки [[swagger]],  можно в [[Makefile]] добавить:

```Makefile
.PHONY: gen-docs
gen-docs:
	@swag init -g ./api/main.go -d ./cmd && swag fmt
```

А потом в `.air.toml:`
```toml
 pre_cmd = ["make gen-docs"]
```