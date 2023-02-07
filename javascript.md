# Functions

## Strings

- length()

```js
var mensaje = "Hola Mundo";
var numeroLetras = mensaje.length; // numeroLetras = 10
```

- concatenar **+**

```js
var variable1 = "Hola ";
var variable2 = 3;
var mensaje = variable1 + variable2; // mensaje = "Hola 3"
```

- concat()

```js
var mensaje1 = "Hola";
var mensaje2 = mensaje1.concat(" Mundo"); // mensaje2 = "Hola Mundo"
```

- toUpperCase()

```js
var mensaje1 = "Hola";
var mensaje2 = mensaje1.toUpperCase(); // mensaje2 = "HOLA"
```

- toLowerCase()

```js
var mensaje1 = "HolA";
var mensaje2 = mensaje1.toLowerCase(); // mensaje2 = "hola"
```

- charAt(position)

```js
var mensaje = "Hola";
var letra = mensaje.charAt(0); // letra = H
letra = mensaje.charAt(2); // letra = l
```

- indexOf(character)

```js
var mensaje = "Hola";
var posicion = mensaje.indexOf("a"); // posicion = 3
posicion = mensaje.indexOf("b"); // posicion = -1
```

- lastIndexOf(character)

```js
var mensaje = "Hola";
var posicion = mensaje.lastIndexOf("a"); // posicion = 3
posicion = mensaje.lastIndexOf("b"); // posicion = -1
```

- substring(start, end)

```js
var mensaje = "Hola Mundo";
var porcion = mensaje.substring(2); // porcion = "la Mundo"
var porcion = mensaje.substring(1, 8); // porcion = "ola Mun"
var porcion = mensaje.substring(-2); // porcion = "Hola Mundo"
```

- split(separador, limit)

```js
var mensaje = "Hola Mundo, soy una cadena de texto!";
var palabras = mensaje.split(" ");
// palabras = ["Hola", "Mundo,", "soy", "una", "cadena", "de", "texto!"];
```

## Arrays

- length()

```js
var vocales = ["a", "e", "i", "o", "u"];
var numeroVocales = vocales.length; // numeroVocales = 5
```

- concat()

```js
var array1 = [1, 2, 3];
array2 = array1.concat(4, 5, 6); // array2 = [1, 2, 3, 4, 5, 6]
array3 = array1.concat([4, 5, 6]); // array3 = [1, 2, 3, 4, 5, 6]
```

- join(separator)

```js
var array = ["hola", "mundo"];
var mensaje = array.join(""); // mensaje = "holamundo"
mensaje = array.join(" "); // mensaje = "hola mundo"
```

- pop()

```js
var array = [1, 2, 3];
var ultimo = array.pop();
// ahora array = [1, 2], ultimo = 3
```

- push()

```js
var array = [1, 2, 3];
array.push(4);
// ahora array = [1, 2, 3, 4]
```

- shift()

```js
var array = [1, 2, 3];
var primero = array.shift();
// ahora array = [2, 3], primero = 1
```

- unshift()

```js
var array = [1, 2, 3];
array.unshift(0);
// ahora array = [0, 1, 2, 3]
```

- reverse()

```js
var array = [1, 2, 3];
array.reverse();
// ahora array = [3, 2, 1]
```

- Remove duplicates from an array

```js
const values = [3, 1, 3, 5, 2, 4, 4, 4];
const uniqueValues = [...new Set(values)];
// uniqueValues is [3, 1, 5, 2, 4]
```

## Numbers

- NaN (Not a Number)

```js
var numero1 = 0;
var numero2 = 0;
alert(numero1 / numero2); // se muestra el valor NaN
```

- isNaN()

```js
var numero1 = 0;
var numero2 = 0;
if (isNaN(numero1 / numero2)) {
  alert("La división no está definida para los números indicados");
} else {
  alert("La división es igual a => " + numero1 / numero2);
}
```

- Infinity or -Infinity

```js
var numero1 = 10;
var numero2 = 0;
alert(numero1 / numero2); // se muestra el valor Infinity
```

- toFixed(digits)

```js
var numero1 = 4564.34567;
numero1.toFixed(2); // 4564.35
numero1.toFixed(6); // 4564.345670
numero1.toFixed(); // 4564
```

# DOM

Document Object Model

## Direct access to the nodes

- getElementsByTagName(tagName)

```js
var parrafos = document.getElementsByTagName("p");
var primerParrafo = parrafos[0];
for (var i = 0; i < parrafos.length; i++) {
  var parrafo = parrafos[i];
}
```

```js
var parrafos = document.getElementsByTagName("p");
var primerParrafo = parrafos[0];
var enlaces = primerParrafo.getElementsByTagName("a");
```

- getElementsByName(name)

```js
var parrafoEspecial = document.getElementsByName("especial");
```

- getElementById(id)

```js
var cabecera = document.getElementById("cabecera");
var enlace = document.getElementById("enlace");
alert(enlace.href); // muestra http://www...com
var imagen = document.getElementById("imagen");
alert(imagen.style.margin); //get css
```

## Create and delete Nodes

- Create
  1. Create type _element_ node

```js
var parrafo = document.createElement("p");
```

    2. Create type *Text* element for the node

```js
var contenido = document.createTextNode("Hola Mundo!");
```

    3. Add the *Text* node as the child node of the *Element* node.

```js
parrafo.appendChild(contenido);
```

    4. Add the *Element* node to the page.

```js
document.body.appendChild(parrafo);
```

- Delete
  - removeChild()

```js
var parrafo = document.getElementById("provisional");
parrafo.parentNode.removeChild(parrafo);
//must be invoke from parent node and it removes children
```

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
function muestraMensaje() {
  alert("Gracias por pinchar");
}
<input type="button" value="Pinchame y verás" onclick="muestraMensaje()" />;
```

El principal inconveniente de este método es que en las funciones externas no se puede seguir utilizando la variable this y por tanto, es necesario pasar esta variable como parámetro a la función:

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

1. Función externa

```js
function muestraMensaje() {
  alert("Gracias por pinchar");
}
```

2. Asignar la función externa al elemento

```js
document.getElementById("pinchable").onclick = muestraMensaje;
```

3. Elemento XHTML

```xml
<input id="pinchable" type="button" value="Pinchame y verás" />
```

- Se debe garantizar la carga completa de la pagina

```js
window.onload = function () {
  document.getElementById("pinchable").onclick = muestraMensaje;
};
```

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

## text

```xml
<input type="text" id="texto" />
```

```js
var valor = document.getElementById("texto").value;
```

## text area

```xml
<textarea id="parrafo"></textarea>
```

```js
var valor = document.getElementById("parrafo").value;
```

## Radiobutton

```xml
<input type="radio" value="si" name="pregunta" id="pregunta_si"/> SI
<input type="radio" value="no" name="pregunta" id="pregunta_no"/> NO
<input type="radio" value="nsnc" name="pregunta" id="pregunta_nsnc"/> NS/NC
```

```js
var elementos = document.getElementsByName("pregunta");

for (var i = 0; i < elementos.length; i++) {
  alert(
    " Elemento: " +
      elementos[i].value +
      "\n Seleccionado: " +
      elementos[i].checked
  );
}
```

## Checkbox

```xml
<input type="checkbox" value="condiciones" name="condiciones" id="condiciones"/> He leído y acepto las condiciones
<input type="checkbox" value="privacidad" name="privacidad" id="privacidad"/> He leído la política de privacidad
```

```js
var elemento = document.getElementById("condiciones");
alert(" Elemento: " + elemento.value + "\n Seleccionado: " + elemento.checked);

elemento = document.getElementById("privacidad");
alert(" Elemento: " + elemento.value + "\n Seleccionado: " + elemento.checked);
```

## Select

```xml
<select id="opciones" name="opciones">
  <option value="1">Primer valor</option>
  <option value="2">Segundo valor</option>
  <option value="3">Tercer valor</option>
  <option value="4">Cuarto valor</option>
</select>
```

```js
// Obtener la referencia a la lista
var lista = document.getElementById("opciones");

// Obtener el índice de la opción que se ha seleccionado
var indiceSeleccionado = lista.selectedIndex;
// Con el índice y el array "options", obtener la opción seleccionada
var opcionSeleccionada = lista.options[indiceSeleccionado];

// Obtener el valor y el texto de la opción seleccionada
var textoSeleccionado = opcionSeleccionada.text;
var valorSeleccionado = opcionSeleccionada.value;

alert(
  "Opción seleccionada: " +
    textoSeleccionado +
    "\n Valor de la opción: " +
    valorSeleccionado
);
```

- Otra forma mas rapida

```js
var lista = document.getElementById("opciones");
// Obtener el valor de la opción seleccionada
var valorSeleccionado = lista.options[lista.selectedIndex].value;
// Obtener el texto que muestra la opción seleccionada
var valorSeleccionado = lista.options[lista.selectedIndex].text;
```

## Focus

```js
document.getElementById("primero").focus();
```

```xml
<form id="formulario" action="#">
  <input type="text" id="primero" />
</form>
```

Asginar focus al primer elemento del primer formulario

```js
if (document.forms.length > 0) {
  for (var i = 0; i < document.forms[0].elements.length; i++) {
    var campo = document.forms[0].elements[i];
    if (campo.type != "hidden") {
      campo.focus();
      break;
    }
  }
}
```

## Avoid duplicate forms

```xml
<form id="formulario" action="#">
  ...
  <input type="button" value="Enviar" onclick="this.disabled=true; this.value='Enviando...'; this.form.submit()" />
</form>
```

## Max length textarea

```js
function limita(maximoCaracteres) {
  var elemento = document.getElementById("texto");
  if (elemento.value.length >= maximoCaracteres) {
    return false;
  } else {
    return true;
  }
}
<textarea id="texto" onkeypress="return limita(100);"></textarea>;
```

```js
function limita(elEvento, maximoCaracteres) {
  var elemento = document.getElementById("texto");

  // Obtener la tecla pulsada
  var evento = elEvento || window.event;
  var codigoCaracter = evento.charCode || evento.keyCode;
  // Permitir utilizar las teclas con flecha horizontal
  if (codigoCaracter == 37 || codigoCaracter == 39) {
    return true;
  }

  // Permitir borrar con la tecla Backspace y con la tecla Supr.
  if (codigoCaracter == 8 || codigoCaracter == 46) {
    return true;
  } else if (elemento.value.length >= maximoCaracteres) {
    return false;
  } else {
    return true;
  }
}

function actualizaInfo(maximoCaracteres) {
  var elemento = document.getElementById("texto");
  var info = document.getElementById("info");

  if (elemento.value.length >= maximoCaracteres) {
    info.innerHTML = "Máximo " + maximoCaracteres + " caracteres";
  } else {
    info.innerHTML =
      "Puedes escribir hasta " +
      (maximoCaracteres - elemento.value.length) +
      " caracteres adicionales";
  }
}
```

```xml
<div id="info">Máximo 100 caracteres</div>
<textarea id="texto" onkeypress="return limita(event, 100);" onkeyup="actualizaInfo(100)" rows="6" cols="30"></textarea>
```

## Restrict characters on input text

```js
function permite(elEvento, permitidos) {
  // Variables que definen los caracteres permitidos
  var numeros = "0123456789";
  var caracteres = " abcdefghijklmnñopqrstuvwxyzABCDEFGHIJKLMNÑOPQRSTUVWXYZ";
  var numeros_caracteres = numeros + caracteres;
  var teclas_especiales = [8, 37, 39, 46];
  // 8 = BackSpace, 46 = Supr, 37 = flecha izquierda, 39 = flecha derecha
  // Seleccionar los caracteres a partir del parámetro de la función
  switch (permitidos) {
    case "num":
      permitidos = numeros;
      break;
    case "car":
      permitidos = caracteres;
      break;
    case "num_car":
      permitidos = numeros_caracteres;
      break;
  }
  // Obtener la tecla pulsada
  var evento = elEvento || window.event;
  var codigoCaracter = evento.charCode || evento.keyCode;
  var caracter = String.fromCharCode(codigoCaracter);
  // Comprobar si la tecla pulsada es alguna de las teclas especiales
  // (teclas de borrado y flechas horizontales)
  var tecla_especial = false;
  for (var i in teclas_especiales) {
    if (codigoCaracter == teclas_especiales[i]) {
      tecla_especial = true;
      break;
    }
  }

  // Comprobar si la tecla pulsada se encuentra en los caracteres permitidos
  // o si es una tecla especial
  return permitidos.indexOf(caracter) != -1 || tecla_especial;
}
```

```xml
<!-- Sólo números -->
<input type="text" id="texto" onkeypress="return permite(event, 'num')" />

<!-- Sólo letras -->
<input type="text" id="texto" onkeypress="return permite(event, 'car')" />

<!-- Sólo letras o números -->
<input type="text" id="texto" onkeypress="return permite(event, 'num_car')" />
```

## Validation

```xml
<form action="" method="" id="" name="" onsubmit="return validacion()">
  ...
</form>
```

```js
function validacion() {
  if (condicion que debe cumplir el primer campo del formulario) {
    // Si no se cumple la condicion...
    alert('[ERROR] El campo debe tener un valor de...');
    return false;
  }
  else if (condicion que debe cumplir el segundo campo del formulario) {
    // Si no se cumple la condicion...
    alert('[ERROR] El campo debe tener un valor de...');
    return false;
  }
  ...
  else if (condicion que debe cumplir el último campo del formulario) {
    // Si no se cumple la condicion...
    alert('[ERROR] El campo debe tener un valor de...');
    return false;
  }

  // Si el script ha llegado a este punto, todas las condiciones
  // se han cumplido, por lo que se devuelve el valor true
  return true;
}
```

## Required text field

```js
valor = document.getElementById("campo").value;
if (valor == null || valor.length == 0 || /^\s+$/.test(valor)) {
  return false;
}
```

```js
valor = document.getElementById("campo").value;
if (isNaN(valor)) {
  return false;
}
```

## List

```js
indice = document.getElementById("opciones").selectedIndex;
if (indice == null || indice == 0) {
  return false;
}
```

```xml
<select id="opciones" name="opciones">
  <option value="">- Selecciona un valor -</option>
  <option value="1">Primer valor</option>
  <option value="2">Segundo valor</option>
  <option value="3">Tercer valor</option>
</select>
```

## Email

```js
valor = document.getElementById("campo").value;
if (!/\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)/.test(valor)) {
  return false;
}
```

## Date

```js
var ano = document.getElementById("ano").value;
var mes = document.getElementById("mes").value;
var dia = document.getElementById("dia").value;

valor = new Date(ano, mes, dia);

if (!isNaN(valor)) {
  return false;
}
```

## Checkbox

```js
elemento = document.getElementById("campo");
if (!elemento.checked) {
  return false;
}
formulario = document.getElementById("formulario");
for (var i = 0; i < formulario.elements.length; i++) {
  var elemento = formulario.elements[i];
  if (elemento.type == "checkbox") {
    if (!elemento.checked) {
      return false;
    }
  }
}
```

## Radiobutton

```js
opciones = document.getElementsByName("opciones");

var seleccionado = false;
for (var i = 0; i < opciones.length; i++) {
  if (opciones[i].checked) {
    seleccionado = true;
    break;
  }
}

if (!seleccionado) {
  return false;
}
```

# Utilities

## Date time

```js
function muestraReloj() {
  var fechaHora = new Date();
  var horas = fechaHora.getHours();
  var minutos = fechaHora.getMinutes();
  var segundos = fechaHora.getSeconds();

  if (horas < 10) {
    horas = "0" + horas;
  }
  if (minutos < 10) {
    minutos = "0" + minutos;
  }
  if (segundos < 10) {
    segundos = "0" + segundos;
  }

  document.getElementById("reloj").innerHTML =
    horas + ":" + minutos + ":" + segundos;
}

window.onload = function () {
  setInterval(muestraReloj, 1000);
};
```

```xml
<div id="reloj" />
```

# Ajax

## XMLHttpRequest properties

| Propertie    | Description                                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| readyState   | Valor numérico (entero) que almacena el estado de la petición                                                                                      |
| responseText | El contenido de la respuesta del servidor en forma de cadena de texto                                                                              |
| responseXML  | El contenido de la respuesta del servidor en formato XML. El objeto devuelto se puede procesar como un objeto DOM                                  |
| status       | El código de estado HTTP devuelto por el servidor (200 para una respuesta correcta, 404 para "No encontrado", 500 para un error de servidor, etc.) |
| statusText   | El código de estado HTTP devuelto por el servidor en forma de cadena de texto: "OK", "Not Found", "Internal Server Error", etc.                    |

## readyState properties

| Value | Description                                                                                       |
| ----- | ------------------------------------------------------------------------------------------------- |
| 0     | No inicializado (objeto creado, pero no se ha invocado el método open)                            |
| 1     | Cargando (objeto creado, pero no se ha invocado el método send)                                   |
| 2     | Cargado (se ha invocado el método send, pero el servidor aún no ha respondido)                    |
| 3     | Interactivo (se han recibido algunos datos, aunque no se puede emplear la propiedad responseText) |
| 4     | Completo (se han recibido todos los datos de la respuesta del servidor)                           |

## XMLHttpRequest methods

| Method                                                                                | Description                                                                                                                                                                               |
| ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| abort()                                                                               | Detiene la petición actual                                                                                                                                                                |
| getAllResponseHeaders()                                                               | Devuelve una cadena de texto con todas las cabeceras de la respuesta del servidor                                                                                                         |
| getResponseHeader("cabecera")                                                         | Devuelve una cadena de texto con el contenido de la cabecera solicitada                                                                                                                   |
| onreadystatechange                                                                    | Responsable de manejar los eventos que se producen. Se invoca cada vez que se produce un cambio en el estado de la petición HTTP. Normalmente es una referencia a una función JavaScript  |
| open(string metodo, string URL [,boolean asincrono, string usuario, string password]) | Establece los parámetros de la petición que se realiza al servidor. Los parámetros necesarios son el método HTTP empleado y la URL destino (puede indicarse de forma absoluta o relativa) |
| send(contenido)                                                                       | Realiza la petición HTTP al servidor                                                                                                                                                      |
| setRequestHeader("cabecera", "valor")                                                 | Permite establecer cabeceras personalizadas en la petición HTTP. Se debe invocar el método open() antes que setRequestHeader()                                                            |

## Get

- Simple

```js
function descargaArchivo() {
  // Obtener la instancia del objeto XMLHttpRequest
  if (window.XMLHttpRequest) {
    peticion_http = new XMLHttpRequest();
  } else if (window.ActiveXObject) {
    peticion_http = new ActiveXObject("Microsoft.XMLHTTP");
  }
  // Preparar la funcion de respuesta
  peticion_http.onreadystatechange = muestraContenido;
  // Realizar peticion HTTP
  peticion_http.open("GET", "http://localhost/holamundo.txt", true);
  peticion_http.send(null);
  function muestraContenido() {
    if (peticion_http.readyState == 4) {
      if (peticion_http.status == 200) {
        alert(peticion_http.responseText);
      }
    }
  }
}
window.onload = descargaArchivo;
```

- Reframed

```js
var READY_STATE_UNINITIALIZED = 0;
var READY_STATE_LOADING = 1;
var READY_STATE_LOADED = 2;
var READY_STATE_INTERACTIVE = 3;
var READY_STATE_COMPLETE = 4;
//
var peticion_http;
//
function cargaContenido(url, metodo, funcion) {
  peticion_http = inicializa_xhr();
  //
  if (peticion_http) {
    peticion_http.onreadystatechange = funcion;
    peticion_http.open(metodo, url, true);
    peticion_http.send(null);
  }
}
//
function inicializa_xhr() {
  if (window.XMLHttpRequest) {
    return new XMLHttpRequest();
  } else if (window.ActiveXObject) {
    return new ActiveXObject("Microsoft.XMLHTTP");
  }
}
//
function muestraContenido() {
  if (peticion_http.readyState == READY_STATE_COMPLETE) {
    if (peticion_http.status == 200) {
      alert(peticion_http.responseText);
    }
  }
}
//
function descargaArchivo() {
  cargaContenido("http://localhost/holamundo.txt", "GET", muestraContenido);
}
//
window.onload = descargaArchivo;
```

- Reframed

```js
var net = new Object();
//
net.READY_STATE_UNINITIALIZED = 0;
net.READY_STATE_LOADING = 1;
net.READY_STATE_LOADED = 2;
net.READY_STATE_INTERACTIVE = 3;
net.READY_STATE_COMPLETE = 4;
//
// Constructor
net.CargadorContenidos = function (
  url,
  funcion,
  funcionError,
  metodo,
  parametros,
  contentType
) {
  this.url = url;
  this.req = null;
  this.onload = funcion;
  this.onerror = funcionError ? funcionError : this.defaultError;
  this.cargaContenidoXML(url, metodo, parametros, contentType);
};
//
net.CargadorContenidos.prototype = {
  cargaContenidoXML: function (url, metodo, parametros, contentType) {
    if (window.XMLHttpRequest) {
      this.req = new XMLHttpRequest();
    } else if (window.ActiveXObject) {
      this.req = new ActiveXObject("Microsoft.XMLHTTP");
    }

    if (this.req) {
      try {
        var loader = this;
        this.req.onreadystatechange = function () {
          loader.onReadyState.call(loader);
        };
        this.req.open(metodo, url, true);
        if (contentType) {
          this.req.setRequestHeader("Content-Type", contentType);
        }
        this.req.send(parametros);
      } catch (err) {
        this.onerror.call(this);
      }
    }
  },
  //
  onReadyState: function () {
    var req = this.req;
    var ready = req.readyState;
    if (ready == net.READY_STATE_COMPLETE) {
      var httpStatus = req.status;
      if (httpStatus == 200 || httpStatus == 0) {
        this.onload.call(this);
      } else {
        this.onerror.call(this);
      }
    }
  },
  //
  defaultError: function () {
    alert(
      "Se ha producido un error al obtener los datos" +
        "\n\nreadyState:" +
        this.req.readyState +
        "\nstatus: " +
        this.req.status +
        "\nheaders: " +
        this.req.getAllResponseHeaders()
    );
  },
};
```

- Read Json

```js
function procesaRespuesta() {
  if (http_request.readyState == READY_STATE_COMPLETE) {
    if (http_request.status == 200) {
      var respuesta_json = http_request.responseText;
      var objeto_json = eval("(" + respuesta_json + ")");
      var mensaje = objeto_json.mensaje;
      var telefono = objeto_json.parametros.telefono;
      var fecha_nacimiento = objeto_json.parametros.fecha_nacimiento;
      var codigo_postal = objeto_json.parametros.codigo_postal;
      document.getElementById("respuesta").innerHTML =
        mensaje +
        "<br>" +
        "Fecha nacimiento = " +
        fecha_nacimiento +
        "<br>" +
        "Codigo postal = " +
        codigo_postal +
        "<br>" +
        "Telefono = " +
        telefono;
    }
  }
}
```

# debugging

## debugger

`debugger;`

## debug

1. in code: `debug('listening');`
2. run project like: `DEBUG=* node app.js`

# destructuring

- obj

```js
const obj = {
  prop1: "uno",
  prop2: "dos",
  prop3: 3,
};
const { prop1, prop2, prop6 } = obj;
```

- array

```js
const array = ["primero", "dos", "tercero"];
const [uno, dos, tres] = array;
```

# Computed property names, like on object literals

```js
let key = "z";
let { [key]: foo } = { z: "bar" };
console.log(foo); // "bar"
```

# TIPS

## Passing arguments to callback functions

```js
var alertText = function (text) {
  alert(text);
};

document
  .getElementById("someelem")
  .addEventListener("click", alertText.bind(this, "hello"));
```

## deep clone

- this is the way: `structuredClone(object)`
- old school:
  ```js
  import { serialize, deserialize } from "v8";
  const test = deserialize(serialize(sqsMessage));
  ```
