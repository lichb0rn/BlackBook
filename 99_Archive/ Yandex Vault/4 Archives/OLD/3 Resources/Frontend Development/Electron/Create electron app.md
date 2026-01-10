---
uuid: 20220716154155
created: 2022-07-16T15:41:55
alias:
- Create electron project
- electron start
---

# [[Create electron app]]

# Установка приложения Electron

1. Создаем новый пакет npm `npm init`, в `package.json`:
```javascript
{  
"name": "my-electron-app",  
"version": "1.0.0",  
"description": "Hello World!",  
"main": "main.js",  
"author": "Jane Doe",  
"license": "MIT"  
}
```

2. Ставим electron
`npm install --save-dev electron`

Обновляем `package.json`:
```javascript
{
  "scripts": {
    "start": "electron ."
  }
}
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/snippet 
- ℹ️ Source:: 
-  🏷️ Tags:: [[Node.js]]