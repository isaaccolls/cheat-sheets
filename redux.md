<!-- MarkdownTOC autolink="true" levels="1,2" -->

- [install](#install)
- [Create store & dispatch action](#create-store--dispatch-action)
  - [Higher-Order Components](#higher-order-components)
  - [Containers](#containers)
  - [Presentational Components](#presentational-components)
  - [reducers](#reducers)
  - [connect](#connect)
  - [middleware Thunk](#middleware-thunk)
  - [middleware redux-promise](#middleware-redux-promise)
  - [selectors](#selectors)
  - [reselect](#reselect)
- [Redux, Flux y SSOT \(architecture\)](#redux-flux-y-ssot-architecture)
  - [Conceptos Flux](#conceptos-flux)
  - [Store](#store)
  - [Data Flow](#data-flow)
  - [Single Source Of Truth: SSOT](#single-source-of-truth-ssot)
- [inmutable.js](#inmutablejs)
- [accion fetchCustomers](#accion-fetchcustomers)
- [redux forms](#redux-forms)

<!-- /MarkdownTOC -->
# install

```bash
npm install --save redux
npm install --save react-redux
```
```bash
yarn add redux
yarn add react-redux
```

# Create store & dispatch action

```js
import { createStore } from 'redux';

const store = createStore(() => {},
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());

const action = { type: 'setCity', value: city }
store.dispatch(action);
```

## Higher-Order Components

React Redux's *connect*
```js
const ConnectedComment = connect(commentSelector, commentActions)(CommentList);
```

## Containers

Componentes que tienen acceso al estado de la aplicacion (connect)

## Presentational Components

No llevan logica

## reducers

Deben ser Pure functions, No alteran estado!
- don't do
```js
state.prop = 'nuevo valor'
```
- hacer copia mediante spread operator!
```js
{ ...state, prop: 'nuevo valor' }
```
  - siempre debe retornar un state

## connect

```js
connect( 1, 2 )(Comp)
```
1. `MapStateToProps (values)`: Tiene como parametros el state de la aplicacion, retorna un objeto con las propiedades a utilizar para ser inyectadas por *connect* dentro del componente como Props, es decir se pueden acceder a estas con `this.props`
2. `MapDispatchToProps (func)`: Espera que le retorne un objeto con funciones. Estas funciones *connect* las inyecta como propiedades dentro del componente.

## middleware Thunk

`npm install --save redux-thunk`
`yarn add redux-thunk`

## middleware redux-promise

- Es un middleware, y como todo middleware "escucha" cada una de las acciones y detecta las acciones que le "interesan".
- Cuando encuentra actions en su payload que tienen una promise, entonces ejecuta la promise y retiene la accion (no invoca a next(action))
- Una vez que se resuelva la promise, genera una accion copia de la original pero con el resultado de la promise en el payload.
- Si la promise finaliza en error, genera una accion en el payload, y con la propiedad "error" como un boolean establecido en true.

## selectors

Recortan una porcion del state de la aplicacion, para trabajar solo sobre una parte del estado.
Aumentan su importancia al momento de utilizar filtros para Arrays.

## reselect

`npm install --save reselect`
`yarn add reselect`
```js
createSelector(...inputSelectors | [inputSelectors], resultFunc)
```

# Redux, Flux y SSOT (architecture)

## Conceptos Flux

- Dispatcher
- Store
- Action
- View

## Store

Los datos en el store solo deben modificarse en respuesta a una action
  
## Data Flow

Flujo de datos estrictamente unidireccional

## Single Source Of Truth: SSOT

Un unico Store
```
      +invocado desde container o
      |de una peticion http
      |
+-----v-----+        +-------------+
|           |        | Containers  |
|  Action   <--------+ UI          |
|  Creator  |        +-----^-------+
+----+------+              | connect (MapState to Props)
     |                     |
     |              +------+-------+  Estado +     +-----------------+
     |              |              |  action       | Reducers        |
     +-------------->    Store    +----------------> CombineReducers |
dispatch(action)    |              <---------------+                 |
                    +--------------+       nuevo   +-----------------+
                                           estado
```

# inmutable.js

libreria recomendada para trabajar con redux

# accion fetchCustomers

1. Instalar Redux
1. Instalar React-Redux
1. Crear un store
1. Vincular el store a la App mediante Provider
1. generar la accion
1. Conectar mediante connect al componente que va a acceder al estado
1. Crear el metodo mapDispatchToProps y vincularlo con la accion
1. Lanzar la accion desde "componentDidMount"
1. ...Hacer que efectivamente realice el fetch contra el server

# redux forms

`npm install --save redux-form` `yarn add redux-form`
