---
created: 2023-11-05T14:55:35
aliases:
  - base setup vite with react
tags:
  - type/note
topic:
  - "[[React]]"
  - ViteJS
source: "[[Ultimate React Course]]"
---
# [[Базовая настройка Vite + React]]

1. ` npm create vite@latest`
2. `npm i -D eslint eslint-config-react-app @vitejs/plugin-react eslint-plugin-prettier prettier vite-plugin-eslint`
3. `.eslintrc.cjs`
```javascript
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended',
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  settings: { react: { version: '18.2' } },
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
  },
}```

4. `.prettierrc`:
```json
{
  "trailingComma": "all",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "bracketSpacing": true,
  "endOfLine": "lf"
}
```

