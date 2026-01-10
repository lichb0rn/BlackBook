---
created: 2023-09-28T09:42:26
aliases:
  - setting up react project with typescript and webpack
tags:
  - type/note
topic: "[[Frontend Development]]"
source: "[[Learn React with TypeScript]]"
---
# [[Настройка React-проекта в связке с TypeScript и Webpack]]

## Структура каталога
	src

## Контейнер для React
В папке `src` создаем html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>My App</title>
</head>
<body>
	<div id="root"></div>
</body>
</html>
```
## Добавляем [[TypeScript]]
Устанавливаем: `npm install --save-dev typescript`
```json
// tsconfig.json
{
    "compilerOptions": {
        "noEmit": true,
        "lib": ["dom", "dom.iterable", "esnext"],
        "moduleResolution": "node",
        "allowSyntheticDefaultImports": true,
        "esModuleInterop": true,
        "jsx": "react",
        "forceConsistentCasingInFileNames": true,
        "strict": true
    },
    "include": ["src"],
    "exclude": ["node_modules", "dist"]
}
```
`allowSyntheticDefaultImports` и `esModuleInterop` позволяют импортировать react как `default`:
```ts
import React from 'react'
```
Без них пришлось бы писать так:
```ts
import * as React from 'react'
```

## Добавляем [[React]]
```bash
npm install react react-dom
npm install --save-dev @types/react @types/react-dom
```
`react` - основная библиотека
`react-dom` - версия для разработки web-приложений

В каталог `src` добавляем файл root-компонент `index.tsx`:
```ts
import React, { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root') as HTMLElement);

function App() {
    return %3Ch1%3EMy React and TypeScript App!</h1>;
}

root.render(
    <StrictMode>
        <App />
    </StrictMode>
);
```

## Добавляем [[Babel]]
[[Babel]] будет транспилировать код [[React]] и [[TypeScript]]
```bash
npm install --save-dev @babel/core
npm install --save-dev @babel/preset-env
npm install --save-dev @babel/preset-react
npm install --save-dev @babel/preset-typescript
npm install --save-dev @babel/plugin-transform-runtime @babel/runtime
```
`.babelrc.json`:
```json
{
    "presets": [
	    "@babel/preset-env", 
	    "@babel/preset-react", 
	    "@babel/preset-typescript"
	],
    "plugins": [
        [
            "@babel/plugin-transform-runtime",
            {
                "regenerator": true
            }
        ]
    ]
}
```

## Добавляем [[Webpack]]
```bash
npm i -D webpack webpack-cli
npm i -D webpack-dev-server
npm i -D html-webpack-plugin
```
### Настройка [[Webpack]]
Ставим `ts-node`, чтобы конфигурацию можно было задать в [[TypeScript]]-файле:
```bash
npm i -D ts-node
```

Создаем файл `webpack.dev.config.ts`:
```ts
import path from 'path';
import HtmlWebpackPlugin from 'html-webpack-plugin';
import {
  Configuration as WebpackConfig,
  HotModuleReplacementPlugin,
} from 'webpack';
import { 
  Configuration as WebpackDevServerConfig 
} from 'webpack-dev-server';

type Configuration = WebpackConfig & {
  devServer?: WebpackDevServerConfig;
}

const config: Configuration = {
  mode: 'development',
  output: {
    publicPath: '/',
  },
  entry: './src/index.tsx',
  module: {
    rules: [
      {
        test: /\.(ts|js)x?$/i,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
	            '@babel/preset-env', 
	            '@babel/preset-react', 
	            '@babel/preset-typescript'
	        ],
          },
        },
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: 'src/index.html',
    }),
    new HotModuleReplacementPlugin(),
  ],
  devtool: 'inline-source-map',
  devServer: {
    static: path.join(__dirname, 'dist'),
    historyApiFallback: true,
    port: 4000,
    open: true,
    hot: true,
  }
};

export default config;
```
В `package.json` добавляем:
```json
"scripts": {
	"start": "webpack serve --config webpack.dev.config.ts"
},
```
