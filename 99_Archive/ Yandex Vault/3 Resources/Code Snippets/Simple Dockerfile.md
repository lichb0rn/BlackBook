---
uuid: 20220721094728
created: 2022-07-21T09:47:28
alias: simple dockerfile
---

# [[Simple Dockerfile]]

Простейший `Dockerfile`:
```Dockerfile
FROM node
LABEL maintainer mtaleiko@gmail.com
RUN git clone -q https://github.com/docker-in-practice/todo.git
WORKDIR todo
RUN npm install > /dev/null
EXPOSE 8000
CMD ["npm", "start"]
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[Docker на практике|Docker in Practice]]
- 🏷️ Tags:: [[Docker]]