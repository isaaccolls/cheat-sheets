<!-- MarkdownTOC autolink="true" levels="1,2" -->

- [firebase cloud functions](#firebase-cloud-functions)
  - [create db](#create-db)
  - [create a function to show data](#create-a-function-to-show-data)
  - [deploy](#deploy)

<!-- /MarkdownTOC -->
# firebase cloud functions

1. prepare project `git init`
1. initialize project `npm init`
1. go to console and create a new project
1. install firebase `npm install -g firebase-tools`
1. login `firebase login`
1. execute inside project `firebase init`
  1. choose __Functions__
  1. choose project name
  1. other configs
    1. language: _js_
    1. ESLint: _Y_
    1. overwrite package.json: _y_
    1. install dependencies with npm now: _y_

## create db

1. create a _Realtime Database_ on firebase console
1. on project root `touch db.json`
1. edit it like [https://gist.github.com/gndx/b144979bbf51306c2bdb7e9febcb7bef](https://gist.github.com/gndx/b144979bbf51306c2bdb7e9febcb7bef)
1. upload db to firebase `firebase database:set /me db.json  -P dev-api`
  - __/me__: object where the information will live
  - _-P_: project name

## create a function to show data

1. download __firebase-config.json__
  - on project in `Configuración / Cuentas de servicio / Firebase Admin SDK / Generar nueva llave privada`
  - download and rename it as: _firebase-config.json_
1. edit project index as:
```js
// Importamos functions desde firebasebase-funcions
const functions = require('firebase-functions');
// Importamos firebase-admin para conectarnos con la base de datos
const firebase = require('firebase-admin');
// Importamos el archivo de configuración que descargamos
const config = require('./firebase-config.json');
// inicializamos nuestra aplicación
firebase.initializeApp({
  credential: firebase.credential.cert(config),
  databaseURL: 'https://arepa-dev-api.firebaseio.com' // URL de nuestro proyecto
});
// creamos la función que obtiene los recursos de nuestra firebase database 
exports.api = functions.https.onRequest((req, res) => {
  res.header('Content-Type', 'application/json');
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  if (req.method === 'GET') {
    const data = firebase.database().ref('/me') // Hacemos referencia a la base de datos
    data.on('value', (snapshot) => {
      res.json(snapshot.val()); // El elemento resultante lo exponemos en un archivo JSON
    });
  }
});
```

## deploy

`firebase deploy`
