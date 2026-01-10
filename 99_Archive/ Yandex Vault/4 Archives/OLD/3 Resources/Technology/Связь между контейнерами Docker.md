---
uuid: 20220804194826
created: 2022-08-04T19:48:26
alias: network between containers in Docker
---

# [[Связь между контейнерами Docker]]

Допустим, мы хотим, чтобы два наших [[Docker| контейнера]] имели доступ по сети друг к другу.
Для этого можно использовать **пользовательские сети**:

1. Создаём виртуальную сеть:
`docker network create my_network`
Все контейнеры в этой сети по-умолчанию будут видеть друг друга по именам.

2. Подключаем контейнер к сети:
`docker network connect my_network blog1`

3. После чего можем запустить ещё один контейнер в интерактивном режиме и проверить:

```bash
docker run -it --network my_network ubuntu:16.04 bash
root@06d6282d32a5:/ apt update && apt install -y curl
[...]
root@06d6282d32a5:/ curl -sSL blog1 | head -n5
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="en-US" xml:lang="en-US">
<head>
<meta name="viewport" content="width=device-width" />
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[Docker на практике]]