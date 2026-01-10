---
uuid: 20220716154912
created: 2022-07-16T15:49:12
alias: electron entry point
---

# [[Electron main process]]

# The main process

The entry point of any Electron application is its `main` script. This script controls the **main process**, which runs in a full Node.js environment and is responsible for controlling your app's lifecycle, displaying native interfaces, performing privileged operations, and managing renderer processes (more on that later).

During execution, Electron will look for this script in the `main` field of the app's `package.json` config, which you should have configured during the [[Create electron app|app scaffolding]] step.

## Приложение на Electron

[[Electron]] -  фреймворк, который содержит в себе движок chromium и node.js.
Приложения состоят из двух частей:
- `app` - модуль, который управляет жизненным циклом приложения
- `BrowserWindow` - модуль, отвечающий за окна.


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
-  🏷️ Tags:: [[Node.js]]