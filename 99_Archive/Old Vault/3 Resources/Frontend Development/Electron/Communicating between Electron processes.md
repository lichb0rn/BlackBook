---
uuid: 20220716164905
created: 2022-07-16T16:49:05
alias: pass data in electron
---

# [[Communicating between Electron processes]]

Electron's main and renderer process have distinct responsibilities and are not interchangeable. This means it is not possible to access the Node.js APIs directly from the renderer process, nor the HTML Document Object Model (DOM) from the main process.

The solution for this problem is to use Electron's `ipcMain` and `ipcRenderer` modules for inter-process communication (IPC). To send a message from your web page to the main process, you can set up a main process handler with `ipcMain.handle` and then expose a function that calls `ipcRenderer.invoke` to trigger the handler in your preload script.

```javascript
// preload.js
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('versions', {
	node: () => process.versions.node,
	chrome: () => process.versions.chrome,
	electron: () => process.versions.electron,
	ping: () => ipcRenderer.invoke('ping'),
});
```

>[!caution]
>Notice how we wrap the `ipcRenderer.invoke('ping')` call in a helper function rather than expose the `ipcRenderer`module directly via context bridge. You **never** want to directly expose the entire `ipcRenderer` module via preload. This would give your renderer the ability to send arbitrary IPC messages to the main process, which becomes a powerful attack vector for malicious code.>


```javascript
// main.js

```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note

