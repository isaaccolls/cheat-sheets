# npx version

`npx -v`

# new project

```bash
npx create-react-app my-app
cd my-app
yarn start
```

# prop-types

- doc[https://www.npmjs.com/package/prop-types](https://www.npmjs.com/package/prop-types)
- install `yarn add prop-types`
- use

```js
import PropTypes from 'prop-types';
//
const WeatherTemperature = ({ temperature, weatherState }) => (
  <div>
    <whatever />
  </div>
);
//
WeatherTemperature.propTypes = {
  temperature: PropTypes.number.isRequired,
  weatherState: PropTypes.string,
};
export default WeatherTemperature;
```

# Include CSS

`import './styles.css';`

# Components

## functional component

```js
const WeatherLocation = () => (
  <div className="weatherLocationCont">
    <Location city={'Canada'} />
    <WeatherData data={data} />
  </div>
);
```

```js
// const AppFrame = props => {
const AppFrame = ({ header, body, footer }) => {
  return (
    <div>
      <div className="app-frame">
        <AppHeader title="{header}"></AppHeader>
        <div>{body}</div>
        <div>Aplicacion simple de Ejemplo</div>
      </div>
    </div>
  );
};
```

## Class Component

```js
class WeatherLocation extends Component {
  constructor() {
    super();
    this.state = {
      city: 'Buenos Aires',
      data: data1,
    };
  }
  //
  handleUpdateClick = () => {
    this.setState({
      city: 'Canada',
      data: data2,
    });
    console.log('actualizado');
  };
  //
  render = () => {
    const { city, data } = this.state;
    return (
      <div className="weatherLocationCont">
        <Location city={city} />
        <WeatherData data={data} />
        <button onClick={this.handleUpdateClick}>Actualizar</button>
      </div>
    );
  };
}
```

### life cycle

1. constructor
2. **UNSAFE** componentWillMount()

- Don't call any service here! 🐤

3. render()
4. componentDidMount()

#### update cycle

1. **UNSAFE** componentWillUpdate()
2. render()
3. componentDidUpdat()

#### others

- componentWillReceiveProps()
- shouldComponentUpdate()
- render()
- componentDidUpdate()

#### un compomente se renderiza cuando:

- Se actualiza el setState
- Cuando se establece nuevo estado
- Actualizar Props desde componente padre
- Llamar forceUpdate

# Resources

## json-server

1. [https://github.com/typicode/json-server](https://github.com/typicode/json-server)
1. `npm install -g json-server`
1. `json-server --watch db.json --port 3004`
1. Create a db.json file with some data

## materialize

[https://www.npmjs.com/package/react-materialize](https://www.npmjs.com/package/react-materialize)

## material-ui

- [https://material-ui.com](https://material-ui.com)
- this! [https://www.npmjs.com/package/material-ui](https://www.npmjs.com/package/material-ui)

## react bootstrap

[https://react-bootstrap.github.io](https://react-bootstrap.github.io)

## react flexbox grid

[https://roylee0704.github.io/react-flexbox-grid/](https://roylee0704.github.io/react-flexbox-grid/)

## eslint

[https://www.npmjs.com/package/eslint](https://www.npmjs.com/package/eslint)
`npm install eslint --save-dev`

- edit `.eslintrc`

```json
{
  "extends": ["react-app", "eslint:recommended"]
}
```

# router

## component link

- web version `yarn add react-router-dom`
- mobile version `yarn add react-router-native`

## Router

Siempre debe llamar un solo componente, por eso una tecnica es envolver multiples en un contenedor. Debe ser de maxima jerarquia (a nivel de aplicacion, en App.js)

```js
import React, { Component } from 'react';
import { BrowserRouter as Router } from 'react-router-dom';
import './App.css';

class App extends Component {
  renderHome = () => <h1>Home</h1>;
  renderCustomerContainer = () => <h1>Customer Container</h1>;
  renderCustomerListContainer = () => <h1>Customer List Container</h1>;
  renderCustomerNewContainer = () => <h1>Customer New Container</h1>;

  render() {
    return (
      <Router>
        <div>
          <Route exact path="/" component={this.renderHome} />
          <Route
            exact
            path="/customers"
            component={this.renderCustomerListContainer}
          />
          <Switch>
            <Route
              path="/customers/new"
              component={this.renderCustomerNewContainer}
            />
            <Route
              path="/customers/:dni"
              component={this.renderCustomerContainer}
            />
          </Switch>
        </div>
      </Router>
    );
  }
}

export default App;
```

## componentes que administran Router

- `<Router>` componente de alto nivel y base indiferente de la manera en la que se realiza el ruteo
- `<BrowserRouter>` permite modificar la url
- `<HashRouter>` utiliza la parte de la url despues del hash(#). no es recomendado en nuevas versiones
- `<MemoryRouter>` no modifica la url, es utilizado para testing y react native

## parametros de browserrouter

```js
<BrowserRouter
  basename={optionalString}
  forceRefresh={optionalBool}
  getUserConfirmation={optionalFunc}
>
  <App />
</BrowserRouter>
```

## Route

Este componente, cuando "location" se corresponde con el path, se encarga de renderizar el o los componentes visuales indicados.

### invocar a Route

1. `<Route path="/" component={customer} />`
1. `<Route path="/" render={() => (<Customer />)} />`
1. `<Route path="/" children=(({match, ...rest}) => (match ? <p>No</p> : <p>Si</p>)) />`

### parametros de Route

- `exact ("/customer" vs "/customer/new")`
- `strict ("/customer" vs "/customer/")`

### match

`/customers/:dni`

- Se pueden utilizar "wildcars" o "url params" que luego los podemos utilizar como parametros que le llegan al componente "match.params".
- Tambien podemos saber si la url es "exact", cual fue el "path" utilizado para evaluar la ruta, y la porcion de la ruta que coincidio con la evaluacion.
- Para el el ejemplo se puede acceder con: `match.parms.dni`

## Switch

Con rutas que pueden "ambiguos matches" o evaluaciones ambiguas, genera una estructura de desicion en la cual el primer "path" evaluado contra la ruta que genere un resultado positivo sera el que ejecute el renderizado de su componente, terminando el proceso de evaluacion sin buscar mas coincidencias.

## Link y NavLink

Componentes de navegacion

## Redirect

Realiza redirecciones para un flujo al cual un usuario no puede acceder

## withRouter

- Es un HOC (high order component)
- Agrega las propiedades **match**, **location**, **history** y re-renderiza al componente cuando estas propiedades se modifican.

## history

Es mutable (o alterable)

- `push`: agrega un nuevo elemento a la pila de history
- `replace`: modifica el ultimo elemento ingresado en history
- `go(n)`: `go(-1) == goBack()` **Y** `go(1) == goFoward()`
- `goBack()`: navega a la ultima navegacion conocida
- `goFoward()`: volver a adelante
- `block()`: cancela o evita la navegacion, para que el usuario no se desplace entre las URLs

# react js best practices

## folder structure

In Rails-style pattern, separate folders are used for “actions”, “constants”, “reducers”, “containers”, and “components”.

```bash
└── src
    ├── assets
    │   ├── css
    │   │   └── main.css
    │   │   └── package.json {main: main.css}
    │   ├── images
    │   └── fonts
    ├── components
    │   ├── App
    │   │   ├── App.css
    │   │   ├── App.test.js
    │   │   ├── App.js
    │   │   └── package.json {main: App.js}
    │   ├── Button
    │   │   ├── Button.css
    │   │   ├── Button.test.js
    │   │   ├── Button.js
    │   │   └── package.json {main: Button.js}
    ├── helpers
    │   ├── registerServiceWorket (by default CRA)
    │   └── aux files like capitalize a word and helper funtions
    └── index.js
```

## functional vs class components

Prefer functional components, class components only when ussing its life cycle 😉

## key indexes

Don't use an index as a key in a render, provide your own id instead

## unnecessary divs

Use only when necessary

## component crash testing

simple crash test to ensure your component will render without crashing

```js
import React from 'react';
import ReactDom from 'react-dom';
import App from '.';
//
it('renders without crashing', () => {
  const div = document.createElement('div');
  ReactDOM.render(<App />, div);
  ReactDOM.unmountComponentAtNode(div);
});
```

## unnecessary data in state

Data that is not being directly rendered can cause unnecessary re-renders

## Understand to handle 'this'

```js
class Message extends Components {
  constructor(props) {
    super(props);
    this.state = { message: 'Hello' };
  }
  logMessage = () => {
    const { message } = this.state;
    console.log(message);
  };
  render() {
    return <input type="button" value="Log" onClick={this.logMessage} />;
  }
}
```

## Use Upper Camel Case Names

## Utilize prop-types

# test

jestjs

# useful commands

- build and local test `yarn build && npx serve build -l 3000`
