---
created: 2025-11-16 21:03
up:
  - "[[JS NextJS Migration]]"
related:
aliases:
tags:
  - type/note
summary:
---
Пример настройки дебаггера для [[NextJS]] - [[JS NextJS Migration]]

```js
{
  // Save as .vscode/launch.json
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js: dev (Node server)",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "runtimeExecutable": "node",
      "runtimeArgs": [
        "--inspect=9229",
        "--enable-source-maps",
        "${workspaceFolder}/node_modules/next/dist/bin/next",
        "dev",
        "-p",
        "3000"
      ],
      "env": {
        "NODE_OPTIONS": "--enable-source-maps",
        "NEXT_TELEMETRY_DISABLED": "1"
      },
      "console": "integratedTerminal",
      "autoAttachChildProcesses": true,
      "skipFiles": ["<node_internals>/**", "**/node_modules/**"],
      "sourceMaps": true
    },

    {
      "name": "Next.js: attach (Node 9229)",
      "type": "node",
      "request": "attach",
      "port": 9229,
      "cwd": "${workspaceFolder}",
      "sourceMaps": true,
      "skipFiles": ["<node_internals>/**", "**/node_modules/**"]
    },

    {
      "name": "Browser: Chrome @ http://localhost:3000",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}",
      "sourceMaps": true,
      "runtimeExecutable": "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
    },

    {
      // Run production build under the debugger
      "name": "Next.js: start (prod, Node server)",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "runtimeExecutable": "node",
      "runtimeArgs": [
        "--inspect=9230",
        "--enable-source-maps",
        "${workspaceFolder}/node_modules/next/dist/bin/next",
        "start",
        "-p",
        "3000"
      ],
      "env": {
        "NODE_OPTIONS": "--enable-source-maps",
        "NEXT_TELEMETRY_DISABLED": "1"
      },
      "preLaunchTask": "npm: build",
      "console": "integratedTerminal",
      "autoAttachChildProcesses": true,
      "skipFiles": ["<node_internals>/**", "**/node_modules/**"],
      "sourceMaps": true
    }
  ],

  "compounds": [
    {
      "name": "Full-stack: Next.js dev (Node + Chrome)",
      "configurations": ["Next.js: dev (Node server)", "Browser: Chrome @ http://localhost:3000"]
    }
  ]
}
```

