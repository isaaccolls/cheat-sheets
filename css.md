<!-- MarkdownTOC autolink="true" levels="1, 2" -->

* [naming](#naming)
* [selectors](#selectors)
* [flexbox](#flexbox)
* [grid](#grid)

<!-- /MarkdownTOC -->

# naming
* **double dash** means variation of the element
* **double underscore** means children of the element.

```xml
<button class='btn btn--warning'> <!-- .btn--warning one of the variation of .btn-->
  <div class="btn__text"></div> <!-- .btn__text one of the child of .btn-->
</button>
```

```css
.btn--warning {
    /* Yay ! By convention, I know that code here relate to the variation "warning" of a button, without event looking at the HMTL code. What a relief !*/
}

.btn__text {
    /* For same reason, I know that this style will target text in a button */
}
```

* use only one letter as a meaningful prefix
  + If it’s a visual component, start with c
  + If it’s an object (like layout), start with o

```xml
<button class='o-layout'>
  <div class='o-layout-item o-grid c-button'></div>
  <!-- When scanning HTML, the eye can quickly differentiate who does what-->
</button>
```

* Use a js- prefix if it is only used by JavaScript

```xml
<button class='js-click-me'>
  <!-- When scanning HTML, I understand that this button has no CSS selector to design it.
       But, JavaScript will use it, probably to catch some event.-->
</button>
```

# selectors
* `p { ... }`: selects all `<p>` elements
* `.intro { ... }`: selects all elements with `class="intro"`
* `#firstname { ... }`: selects the element with `id="firstname"`
* `* { ... }`: selects al elements
* `p.intro { ... }`: selects all `<p>` elements with `class="intro"`
* `div, p { ... }`: selects all `<div>` elements and all `<p>` elements
* `div p { ... }`: selects all `<p>` elements inside `<div>` elements
* `div + p { ... }`: selects all `<p>` elements that are placed immediately after `<div>`
* `div > p { ... }`: selects all `<p>` elements where the parent is a `<div>`
* `p ~ u { ... }`: selects every `<ul>` element tha is preceded by a `<p>` element
* `[target] { ...}`: selects all elements with a target attribute
* `[target=_blank] { ... }`: selects all elements with `target=_blank`
* `:root { ... }`: selects the document's root element
* `:not(p) { ... }`: selects every element that is not a `<p>` element
* `p:empty { ... }`: selects every `<p>` element that has no children
* `p:first-child { ... }`: selects every `<p>` element that is the first child
* `p:nth-child(2) { ... }`: selects every `<p>` element that is the second child of its parent
* `p:only-child { ... }`: selects every `<p>` element that is the only child
# flexbox

**container flex**

```css
.container {
    display: flex;
}
```

* `flex`: only one per line
* `flex-inline`: many per line

## `justify-content`

alinea elementos horizontalmente

* `flex-start`: alinea elementos al lado izquierdo del contenedor.
* `flex-end`: alinea elementos al lado derecho del contenedor.
* `center`: alinea elementos en el centro del contenedor.
* `space-between`: muestra elementos con la misma distancia entre ellos.
* `space-around`: muestra elementos con la misma separación alrededor de ellos.

## `align-items`

alinea elementos verticalmente

* `flex-start`: alinea elementos a la parte superior del contenedor.
* `flex-end`: alinea elementos a la parte inferior del contenedor.
* `center`: alinea elementos en el centro (verticalmente hablando) del contenedor.
* `baseline`: muestra elementos en la línea base del contenedor
* `stretch`: elementos se estiran para ajustarse al contenedor.

## `flex-direction`

define la dirección de los elementos en el contenedor (eje principal)

* `row`: elementos son colocados en la misma dirección del texto.
* `row-reverse`: elementos son colocados en la dirección opuesta al texto.
* `column`: elementos se colocan de arriba hacia abajo.
* `column-reverse`: elementos se colocan de abajo hacia arriba.

1. nota: cuando estableces la dirección a una fila invertida o columna, el inicio y el final también se invierten.
2. nota: cuando es una columna, justify-content cambia a vertical y align-items a horizontal.

## `order`

default: 0, admit +/- int. Ex: `order: 1`  `order: unset`

## `align-self`

aplica a elementos individuales. acepta los mismos valores de align-items.

* `flex-start`
* `flex-end`
* `center`
* `baseline`
* `stretch`

## `flex-wrap`

especifica si los elementos "hijos" son obligados a permanecer en una misma línea o pueden fluir en varias líneas.

* `nowrap`: cada elemento se ajusta en una sola línea.
* `wrap`: los elementos se envuelven alrededor de líneas adicionales.
* `wrap-reverse`: los elementos se envuelven alrededor de líneas adicionales en reversa.

## `flex-flow`

combina **flex-direction** y **flex-wrap**, acepta un valor de cada una separada por un espacio. Ex: `flex-flow: row wrap`

## `align-content`

**align-content** determina el espacio entre las líneas, mientras que **align-items** determina como los elementos en su conjunto están alineados dentro del contenedor. cuando hay solo una línea, **align-content** no tiene efecto.

* `flex-start`: las líneas se posicionan en la parte superior del contenedor.
* `flex-end`: las líneas se posicionan en la parte inferior del contenedor.
* `center`: las líneas se posicionan en el centro (verticalmente hablando) del contenedor.
* `space-between`: las líneas se muestran con la misma distancia entre ellas.
* `space-around`: las líneas se muestran con la misma separación alrededor de ellas.
* `stretch`: las líneas se estiran para ajustarse al contenedor.

## `flex`

shorthand property sets how a flex item will grow or shrink to fit the space available in its flex container. Ex: `flex: 1 0 auto`

* `flex-grow`: sets the flex grow factor of a flex item main size. Ex: `flex-grow: 1`
* `flex-shrink`: sets the flex shrink factor of a flex item. Ex: `flex-grow: 1; flex-shrink: 0; `
* `flex-basis`: sets the initial main size of a flex item. Ex: `flex-basis: 50%`  `flex-basis: 500px`
# grid

```css
.container {
    display: grid;
    grid-template-columns: 50% 25% 25%;
    grid-template-rows: 50% 50%;
    height: 200px;
}
```

## `grid-template-columns`

property specifies the number (and the widths) of columns in a grid layout

## `grid-template-rows`

property specifies the number (and the heights) of the rows in a grid layout

```css
.container {
    display: grid;
    grid-template-columns: 50% 50%;
    grid-template-rows: 50% 50%;
}
```

## shorthand `grid-template`

propiedad abreviada que combina **grid-template-rows** y **grid-template-columns**

```css
.container {
    grid-template: 50% 50% / 200px;
    grid-template: 60% / 200px;
}
```

## `grid-column-start`

valor entreo que define en qué línea de columna se iniciará el elemento

## `grid-column-end`

puede extender el elemento de **grid-column-start** varias columnas

```css
.box-1 {
    grid-column-start: 1;
    grid-column-end: 3;
}
```

## `grid-row-start`

funciona de manera semejante a **grid-column-start** pero a lo largo del eje vertical.

## `grid-row-end`

funciona de manera semejante a **grid-column-end** pero a lo largo del eje vertical.

```css
.box-1 {
    grid-row-start: 2;
    grid-row-start: 4;
}
```

## `grid-column`

acepta a la vez los valores de **grid-column-start** y **grid-column-end** separados por una barra oblicua

## `grid-row`

como lo haria **grid-column**

```css
.box-1 {
    grid-column: 1 / 3;
    grid-row: 2 / 4;
}
```

## `span`

definir un elemento basado en la longitud de columnas deseada. **span** solo funciona con valores positivos.

```css
.box-1 {
    grid-column-start: 2;
    grid-column-end: span 2;
}

.box-2 {
    grid-column-start: span 3;
    grid-column-end: 6;
}
```

## `grid-auto-flow`

controls how auto-placed items get inserted in the grid

```css
.container {
    display: grid;
    grid-autoflow: column;
}
```

## shorthand `grid`

row / columns: `none|grid-template-rows / grid-template-columns|grid-template-areas|grid-template-rows / [grid-auto-flow] grid-auto-columns|[grid-auto-flow] grid-auto-rows / grid-template-columns|initial|inherit; `

```css
.container {
    display: grid;
    grid: 50% 50% / 33% 33% 33%;
}
```

## repeat

sirve para abreviar

```css
.container {
    display: grid;
    grid-template-columns: 33.33% 33.33% 33.33%;
    grid-template-columns: repeat(3, 33.33%);
    grid-template-columns: 50% repeat(2, 25%);
    grid: repeat(2, 50%) / repeat(3, 33.33%);
}
```

## shorthand `grid-area`

admite cuatro valores separados por barras oblicuas: **grid-row-start**, **grid-column-start**, **grid-row-end** y **grid-column-end**.

```css
.container {
    grid-area: 1 / 1 / 3 / 3;
    grid-area: 1 / 2 / span 3 / span 4;
}
```

## `grid-template-areas`

specifies areas within the grid layout, vacion con un __"."__

```css
.conttainer {
    height: 100vh;
    width: 900px;
    margin: 0 auto;
    display: grid;
    grid: 100px auto 100px / repeat(4, 25%);
    grid-gap: 1rem;
    grid-template-areas:
        "header header header header"
        "principal principal principal sidebar"
        "footer footer footer footer"
}

.header {
    grid-area: header;
}

.contenido-principal {
    grid-area: principal;
}

.sidebar {
    grid-area: sidebar;
}

.footer {
    grid-area: footer;
}
```

## `grid-gap`

property defines the size of the gap between the rows and columns in a grid layout, and is a shorthand property for grid-row-gap and grid-column-gap

```css
.grid-container {
    grid-gap: 50px;
}
```

## fr

cada unidad fr asigna una porción del espacio disponible. por ejemplo, si dos elementos están establecidos a 1fr y 3fr respectivamente el espacio se divide en 4 porciones iguales; el primer elemento ocupa 1/4 del espacio y el segundo elemento los 3/4 restantes.

```css
.box {
    grid-template-columns: 33.33% 33.33% 33.33%;
    grid-template-columns: repeat(3, 1fr);
    grid-template-columns: 1fr 5fr;
    grid-template-columns: 50px 1fr 1fr 1fr 50px;
    grid-template-columns: 75px 3fr 2fr;
}
```

## order

si los elementos de la cuadrícula no se sitúan explícitamente con grid-area, grid-column, grid-row, etc., se sitúan automáticamente de acuerdo al orden en el código fuente. puedes sobrescribir esto usando la propiedad order.

```css
.box {
    order: 4;
    order: -1;
}
```

## `align-items`

alinea elementos verticalmente

* `start`: alinea elementos a la parte superior del contenedor.
* `end`: alinea elementos a la parte inferior del contenedor.
* `center`: alinea elementos en el centro (verticalmente hablando) del contenedor.
* `initial`
* `stretch`: elementos se estiran para ajustarse al contenedor.

## `align-content`

* `start`: las líneas se posicionan en la parte superior del contenedor.
* `end`: las líneas se posicionan en la parte inferior del contenedor.

## `justify-content`

alinea elementos horizontalmente

* `start`: alinea elementos al lado izquierdo del contenedor.
* `end`: alinea elementos al lado derecho del contenedor.
* `center`: alinea elementos en el centro del contenedor.
* `space-between`: muestra elementos con la misma distancia entre ellos.
* `space-around`: muestra elementos con la misma separación alrededor de ellos.

## `auto-fill`

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
}
```

## `auto-fit`

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}
```
