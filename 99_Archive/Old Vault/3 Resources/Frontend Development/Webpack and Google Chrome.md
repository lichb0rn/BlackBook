---
uuid: 20230725100940
created: 2023-07-25T10:09:40
alias:
- open chrome with dev server
- запустить dev server и chrome
---

# [[Webpack and Google Chrome]]

Чтобы запускать [[Google Chrome]] совместно с development server [[Webpack]], нужно:
1. Добавить в `webpack.config.js`:
```javascript
devServer: {
        port: 3000,
        hot: isDev,
        open: {
            app: {
                name: 'Google Chrome',
            },
        },
    },
```
2. В `package.json`:
```javascript
"scripts": {
	"start": "cross-env NODE_ENV=development webpack-dev-server",
	"build": "cross-env NODE_ENV=production webpack --mode production"
},
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
- 🏷️ Tags:: [[Frontend Development]], [[Tools]], [[Configuration]]