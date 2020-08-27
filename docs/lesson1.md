## Application bureau 1 : electron

## Installation globale

```console
## installation de nodejs avant
$ npm i -g electron
```

## creation manuelle

```console
$ mkdir mon-app && cd mon-app
$ npm init -Y
$ npm i electron -S
$ touch index.js index.html

```

contenu de index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Salamalekoum</title>
  </head>
  <body>
    <h1>Lalekou GrayTchad</h1>
  </body>
</html>
```

contenu de index.js

```javascript
const { app, BrowserWindow } = require("electron");
app.whenReady().then(function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
  });
  // et charger le fichier index.html de l'application.
  win.loadFile("index.html");
});
```

contenu de package.json

```json
{
  "name": "testappbureau",
  "version": "1.0.0",
  "description": "mini Application pour tester electron",
  "main": "index.js",
  "scripts": {
    "test": "test",
    "start": "electron ."
  },
  "author": "graytchad",
  "license": "ISC",
  "dependencies": {
    "electron": "^10.0.1"
  }
}
```

## Génération automatique (électron forge)

```console
$ npx create-electron-app my-app --template=webpack
```

## A partir de angular cli

```console
$ ng new my-app && cd my-app && code .
$ npm i electron -S

```

modifier index.html

```html
<base href="./" />
```

modifier package.json

```json
{
	...
	"main": "main.js",
	"scripts": {
		...
		"start": "ng build && electron .",
	}
	...
}
```

créer un fichier main.js à la racine du projet. Voici son contenu

```javascript
const { app, BrowserWindow } = require("electron");
const url = require("url");
const path = require("path");
let mainWindow;
function createWindow() {
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
  });
  mainWindow.loadURL(
    url.format({
      pathname: path.join(__dirname, `/dist/angular-bureau/index.html`),
      protocol: "file:",
      slashes: true,
    })
  );
  mainWindow.on("closed", function () {
    mainWindow = null;
  });
}
app.on("ready", createWindow);
app.on("window-all-closed", function () {
  if (process.platform !== "darwin") app.quit();
});
app.on("activate", function () {
  if (mainWindow === null) createWindow();
});
```
