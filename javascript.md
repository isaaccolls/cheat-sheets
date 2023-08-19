- [Strings](#strings)
- [Arrays](#arrays)
- [Numbers](#numbers)
- [objects](#objects)
- [DOM](#dom)
  - [Direct access to the nodes](#direct-access-to-the-nodes)
  - [Create and delete Nodes](#create-and-delete-nodes)
- [Events](#events)
  - [Event type](#event-type)
  - [Event handlers as XHTML attributes](#event-handlers-as-xhtml-attributes)
  - [this](#this)
  - [Manejadores como funciones JavaScript externas.](#manejadores-como-funciones-javascript-externas)
  - [Manejadores "semánticos".](#manejadores-semánticos)
  - [Eventos del teclado](#eventos-del-teclado)
  - [Eventos del raton](#eventos-del-raton)
- [forms](#forms)
- [debugging](#debugging)
  - [debugger](#debugger)
  - [debug](#debug)

# Strings

- length: `str.length`
- concatenar: `'Tommy is ' + age + ' years old.'`
- concat(): `str1.concat(str2)`
- toUpperCase(): `str.toUpperCase()`
- toLowerCase(): `str.toLowerCase()`
- charAt(position): `char = str.charAt(index)`
- indexOf(character): `position = str.indexOf(char)`
- lastIndexOf(character): `position = str.lastIndexOf(char)`
- substring(start, end)
- split(separador, limit): `str.split(",")`

# Arrays

- length: `array.length`
- concat: `array3 = array1.concat(array2)`
- join(separator): `str = array.join(" ")`
- pop(): `last = array.pop()`
- push(): `array.push(value)`
- shift(): `first = array.shift()`
- unshift(): `array.unshift(value)`
- reverse(): `array.reverse()`
- remove duplicates: `uniqueValues = [...new Set(array)]`

# Numbers

- NaN (Not a Number): `alert(0 / 0)`
- isNaN(): `isNaN(value)`
- Infinity or -Infinity: `alert(10 / 0)`
- toFixed(digits): `numberVar.toFixed(2)`

# objects

- deep clone: `structuredClone(object)`

# DOM

Document Object Model

## Direct access to the nodes

- getElementsByTagName(tagName): `parrafos = document.getElementsByTagName("p")`
- getElementsByName(name): `parrafoEspecial = document.getElementsByName("especial")`
- getElementById(id): `cabecera = document.getElementById("cabecera")`

## Create and delete Nodes

- Create
  1. Create type _element_ node: `parrafo = document.createElement("p")`
  2. Create type _Text_ element for the node: `contenido = document.createTextNode("Hola Mundo!")`
  3. Add the _Text_ node as the child node of the _Element_ node: `parrafo.appendChild(contenido)`
  4. Add the _Element_ node to the page: `document.body.appendChild(parrafo)`
- Delete
  - removeChild(): `document.getElementById("provisional").parentNode.removeChild(parrafo)`

# Events

## Event type

| Evento      | Descripción                                                     | Elementos para los que está definido                       |
| ----------- | --------------------------------------------------------------- | ---------------------------------------------------------- |
| onblur      | Deseleccionar el elemento                                       | `<button>, <input>, <label>, <select>, <textarea>, <body>` |
| onchange    | Deseleccionar un elemento que se ha modificado                  | `<input>, <select>, <textarea>`                            |
| onclick     | Pinchar y soltar el ratón                                       | Todos los elementos                                        |
| ondblclick  | Pinchar dos veces seguidas con el ratón                         | Todos los elementos                                        |
| onfocus     | Seleccionar un elemento                                         | `<button>, <input>, <label>, <select>, <textarea>, <body>` |
| onkeydown   | Pulsar una tecla (sin soltar)                                   | Elementos de formulario y <body>                           |
| onkeypress  | Pulsar una tecla                                                | Elementos de formulario y <body>                           |
| onkeyup     | Soltar una tecla pulsada                                        | Elementos de formulario y <body>                           |
| onload      | La página se ha cargado completamente                           | `<body>`                                                   |
| onmousedown | Pulsar (sin soltar) un botón del ratón                          | Todos los elementos                                        |
| onmousemove | Mover el ratón                                                  | Todos los elementos                                        |
| onmouseout  | El ratón "sale" del elemento (pasa por encima de otro elemento) | Todos los elementos                                        |
| onmouseover | El ratón "entra" en el elemento (pasa por encima del elemento)  | Todos los elementos                                        |
| onmouseup   | Soltar el botón que estaba pulsado en el ratón                  | Todos los elementos                                        |
| onreset     | Inicializar el formulario (borrar todos sus datos)              | `<form>`                                                   |
| onresize    | Se ha modificado el tamaño de la ventana del navegador          | `<body>`                                                   |
| onselect    | Seleccionar un texto                                            | `<input>, <textarea>`                                      |
| onsubmit    | Enviar el formulario                                            | `<form>`                                                   |
| onunload    | Se abandona la página (por ejemplo al cerrar el navegador)      | `<body>`                                                   |

## Event handlers as XHTML attributes

```xml
<div onclick="alert('Has pinchado con el ratón');" onmouseover="alert('Acabas de pasar el ratón por encima');">
  Puedes pinchar sobre este elemento o simplemente pasar el ratón por encima
</div>
<body onload="alert('La página se ha cargado completamente');">
  ...
</body>
```

## this

```xml
<div id="contenidos" style="width:150px; height:60px; border:thin solid silver" onmouseover="document.getElementById('contenidos').style.borderColor='black';" onmouseout="document.getElementById('contenidos').style.borderColor='silver';">
  Sección de contenidos...
</div>
<div id="contenidos" style="width:150px; height:60px; border:thin solid silver" onmouseover="this.style.borderColor='black';" onmouseout="this.style.borderColor='silver';">
  Sección de contenidos...
</div>
```

## Manejadores como funciones JavaScript externas.

```js
function resalta(elemento) {
  switch (elemento.style.borderColor) {
    case "silver":
    case "silver silver silver silver":
    case "#c0c0c0":
      elemento.style.borderColor = "black";
      break;
    case "black":
    case "black black black black":
    case "#000000":
      elemento.style.borderColor = "silver";
      break;
  }
}
```

```xml
<div style="width:150px; height:60px; border:thin solid silver" onmouseover="resalta(this)" onmouseout="resalta(this)">
  Sección de contenidos...
</div>
```

## Manejadores "semánticos".

asignar la función externa al elemento:`document.getElementById("someId").onclick = someFunction;`

## Eventos del teclado

```js
window.onload = function () {
  document.onkeyup = muestraInformacion;
  document.onkeypress = muestraInformacion;
  document.onkeydown = muestraInformacion;
};

function muestraInformacion(elEvento) {
  var evento = window.event || elEvento;
  var mensaje =
    "Tipo de evento: " +
    evento.type +
    "<br>" +
    "Propiedad keyCode: " +
    evento.keyCode +
    "<br>" +
    "Propiedad charCode: " +
    evento.charCode +
    "<br>" +
    "Carácter pulsado: " +
    String.fromCharCode(evento.charCode);

  info.innerHTML += "<br>--------------------------------------<br>" + mensaje;
}
```

```xml
...
<div id="info"></div>
```

## Eventos del raton

```js
function muestraInformacion(elEvento) {
  var evento = elEvento || window.event;
  var coordenadaX = evento.clientX;
  var coordenadaY = evento.clientY;
  alert(
    "Has pulsado el ratón en la posición: " + coordenadaX + ", " + coordenadaY
  );
}
document.onclick = muestraInformacion;
```

# forms

- text: `<input type="text" id="texto" />` `valor = document.getElementById("texto").value`
- text area: `<textarea id="parrafo"></textarea>` `valor = document.getElementById("parrafo").value`
- radiobutton: `<input type="radio" value="si" name="pregunta" id="pregunta_si"/>`
- Checkbox: `<input type="checkbox" value="condiciones" name="condiciones" id="condiciones"/> He leído y acepto las condiciones`
- Focus: `document.getElementById("primero").focus()`
- Avoid duplicate forms: `<input type="button" value="Enviar" onclick="this.disabled=true; this.value='Enviando...'; this.form.submit()" />`

# debugging

## debugger

`debugger;`

## debug

1. in code: `debug('listening');`
2. run project like: `DEBUG=* node app.js`
