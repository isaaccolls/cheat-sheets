- [Capas de la Arquitectura Hexagonal](#capas-de-la-arquitectura-hexagonal)
  - [Dominio](#dominio)
  - [Aplicación](#aplicación)
  - [Infraestructura](#infraestructura)
- [Regla de dependencia](#regla-de-dependencia)
- [Puertos y adaptadores](#puertos-y-adaptadores)
- [Testing](#testing)
- [Estructura de directorios](#estructura-de-directorios)
  - [Módulos o sub-dominios](#módulos-o-sub-dominios)
  - [Infraestructura compartida](#infraestructura-compartida)
  - [Bounded Contexts](#bounded-contexts)
- [servicios](#servicios)
  - [Servicios de infraestructura](#servicios-de-infraestructura)
  - [Servicios de Aplicación](#servicios-de-aplicación)
  - [Servicios de dominio](#servicios-de-dominio)
  - [Diferencias entre usar Servicios de Dominio y de Infraestructura desde Aplicación](#diferencias-entre-usar-servicios-de-dominio-y-de-infraestructura-desde-aplicación)

# Capas de la Arquitectura Hexagonal

![Capas de la Arquitectura Hexagonal](./images/hexagonal/capas.png)

## Dominio

Conceptos que están en nuestro contexto (Usuario, Producto, Carrito, etc), y reglas de negocio que vienen determinadas en exclusiva por nosotros (servicios de dominio),

## Aplicación

La capa de aplicación es donde viven los casos de uso de nuestra aplicación (registrar usuario, publicar producto, añadir producto al carrito, etc).

## Infraestructura

Código que cambia en función de decisiones externas. En esta capa vivirán las implementaciones de las interfaces que definiremos a nivel de dominio. Es decir, nos apoyaremos en el DIP de SOLID para poder desacoplarnos de las dependencias externas.

# Regla de dependencia

Hay una regla de oro que deberemos tener en cuenta al tratar con código que respete una Arquitectura Hexagonal: La regla de dependencia.

Esta regla nos dice que el código que viva en cada una de nuestras capas sólo deberá conocer las clases que se ubican en la capa inmediatamente siguiente. Entendemos el orden de las capas desde fuera hacia dentro del círculo: Infraestructura -> Aplicación -> Dominio.

Esta regla lo que nos proporciona es la posibilidad de cambiar elementos de nuestras capas más externas sin que las internas se vean afectadas. Por esto adquiere más sentido que los aspectos que más variabilidad tienen ya que no dependen de nosotros estén en la capa más externa (infraestructura).

# Puertos y adaptadores

La Arquitectura Hexagonal también se denomina “Ports and adapters”. De hecho, en nuestra opinión este término es más acertado ya que tiene connotaciones más cercanas a lo que podríamos pensar al ver cómo queda el código, y no implica un número finito como sí lo hace la palabra hexágono.

En ese sentido, podemos pensar que:

- Los **puertos**: son las interfaces definidas en la capa de dominio para desacoplarnos de nuestra infraestructura. Ejemplo: UserRepository
- Los **adaptadores**: son las implementaciones posibles de esos puertos. Estas implementaciones traducirán esos contratos definidos en la interfaz a la lógica necesaria a ejecutar en base a un determinado proveedor. Ejemplo: MySqlUserRepository

# Testing

![testing](./images/hexagonal/testing.png)

- Test unitarios: Capa de Aplicación y Dominio
- Test de integración: Capa de Infraestructura
- Test de Aceptación: Todas las capas

# Estructura de directorios

dentro de cada módulo de nuestra aplicación (usuarios y vídeos) tenemos 3 carpetas, una para cada capa de nuestra arquitectura

```bash
$ tree -L 3
.
├── entry_point
│   ├── EntryPointDependencyContainer.scala
│   ├── Routes.scala
│   ├── ScalaHttpApi.scala
│   └── controller
│       ├── status
│       ├── user
│       └── video
└── module
    ├── shared
    │   └── infrastructure
    ├── user
    │   ├── application
    │   ├── domain
    │   └── infrastructure
    └── video
        ├── application
        ├── domain
        └── infrastructure
```

## Módulos o sub-dominios

Son agrupaciones de código en base a los conceptos principales de nuestra aplicación.

```bash
$ tree module/video
module/video
├── application
│   ├── create
│   │   └── VideoCreator.scala
│   └── search
│       └── VideosSearcher.scala
├── domain
│   ├── Video.scala
│   ├── VideoCategory.scala
│   ├── VideoDuration.scala
│   ├── VideoId.scala
│   ├── VideoRepository.scala
│   └── VideoTitle.scala
└── infrastructure
    ├── dependency_injection
    │   └── VideoModuleDependencyContainer.scala
    ├── marshaller
    │   └── VideoJsonFormatMarshaller.scala
    └── repository
        └── DoobieMySqlVideoRepository.scala
```

## Infraestructura compartida

Por ejemplo de la configuración de base de datos, conexión a ésta, y otras posibles cositas que tengamos. Lo que hacemos nosotros es ubicarla en un modulo “shared”:

```bash
$ tree module/shared/infrastructure
module/shared/infrastructure
├── config
│   └── DbConfig.scala
├── dependency_injection
│   └── SharedModuleDependencyContainer.scala
└── persistence
    └── doobie
        ├── DoobieDbConnection.scala
        └── TypesConversions.scala
```

## Bounded Contexts

Básicamente lo que establece este concepto es un nuevo nivel de separación en nuestro código. Es decir, de fuera hacia dentro nuestra aplicación tendrá N contextos donde cada uno de ellos tendrá N módulos.

Cabe destacar que a diferencia de los módulos, cada contexto tendrá su propia infraestructura. Para comunicarnos entre contextos usaremos el mismo método que para comunicarnos entre módulos: Commands o Queries a través del Bus correspondiente 🙂

La estructura de directorios que veríamos por tanto en este otro caso sería similar a:

```bash
$ tree src -L 5 -d // ℹ️ Output simplificando para ilustrar mejor el objeto de análisis de esta lección
src
├── Context
│   ├── Video
│   │    ├── Infrastructure
│   │    │   ├── Doctrine
│   │    │   └── Symfony
│   │    ├── Module
│   │    │   ├── Notification
│   │    │   │   ├── Application
│   │    │   │   ├── Domain
│   │    │   │   ├── Infrastructure
│   │    │   │   └── ...
│   │    │   └── ...
│   │    └── ...
│   └── ...
├── Infrastructure
│   ├── Bus
│   │   ├── Command
│   │   ├── Event
│   │   └── Query
│   └── ...
├── Shared
│   ├── Domain
│   │   └── Bus
│   │       ├── Command
│   │       ├── Event
│   │       └── Query
│   ├── Infrastructure
│   │   └── Persistence
│   │       └── Course
│   └── ...
└── ...
```

# servicios

## Servicios de infraestructura

Aspectos a tener en cuenta:

- Las particularidades de cada adaptador/implementación de nuestras interfaces las especificaremos a través de inyección vía constructor. Ejemplos:
  - Conexión con base de datos en repositorios
  - Sender y credenciales SMTP en servicio de notificación vía email
  - Canal y API Key en servicio de notificación vía Slack
- Evitaremos el acoplamiento estructural en nuestras interfaces no acoplando los contratos, lógica, o flujo de llamadas a conceptos relacionados con alguna de nuestras implementaciones.
- Usaremos implementaciones fake de servicios como el de envío de email para ejecutar nuestros tests.

#### Dominio compartido

A su vez, otro de los conceptos que compartiremos entre módulos serán nuestros pequeños Value Objects que modelan por ejemplo los identificadores de nuestras entidades.

Esto lo haremos ya que, por ejemplo, un Video podría contener el identificador del usuario que lo ha publicado. Con lo cuál, desde el momento en el que la forma de relacionar una entidad de un módulo con otra entidad de un módulo diferente es a través de este identificador y no una relación de asociación para evitar el acoplamiento, no nos queda otra que compartir el UserId entre los dos módulos.

## Servicios de Aplicación

- Son los puntos de entrada a nuestra aplicación. Es decir, como se ve en el gráfico, los controladores de línea de comandos o de nuestra API HTTP (¡como la del curso de Scala!) invocarán a los servicios de aplicación.
- Representan de forma atómica un caso de uso de nuestro sistema. En caso de modificaciones del estado de nuestra aplicación:
  - Podrán hacer las de barrera transaccional con el sistema de persistencia.
  - Publicarán los eventos de dominio respectivos.
- Coordinan las llamadas a los distintos elementos de nuestro sistema para ejecutar un determinado caso de uso.
- Les llamaremos indistintamente Servicio de Aplicación como caso de uso.

## Servicios de dominio

Los servicios de domino representan una agrupación de lógica de negocio que podremos reutilizar desde múltiples Servicios de Aplicación.

Vamos a poner un ejemplo para poder explicarnos mejor. Tenemos dos casos de uso en nuestra aplicación:

- Obtener un vídeo en base a su identificador
- Modificar el título de un determinado vídeo

En ambos casos de uso, necesitaremos la lógica de negocio para:

- Ir al repositorio de vídeos a buscar un vídeo determinado en base a su identificador
- Lanzar una excepción de dominio tipo VideoNotFound en caso de no encontrar el vídeo. Importante destacar que quien lanza esta excepción, como comentamos en el vídeo, no es la implementación del repositorio.
- Retornar el vídeo en caso de encontrarlo

Para evitar duplicar esta lógica de negocio en los 2 Servicios de Aplicación lo que solemos hacer es extraerla a un Servicio de Dominio que invocaremos desde ambos casos de uso.

Es importante destacar que los servicios de dominio **en ningún caso publicarán los eventos de dominio** que se puedan producir ni gestinonarán transacciones. Eso se lo dejamos al Application Service que nos invoca para evitar duplicidades ya que es realmente él quién establece la “atomicidad” del caso de uso.

## Diferencias entre usar Servicios de Dominio y de Infraestructura desde Aplicación

### Servicio de Aplicación -> Servicio de Infraestructura

Cuando interaccionamos con un servicio de infraestructura desde uno de aplicación, lo que hacemos como vimos en la lección anterior es hacer uso del Principio de Inversión de Dependencias.

Es decir, **el Servicio de Aplicación recibe por constructor el colaborador de infraestructura** que, para evitar acoplamiento, lo hace a través de una interface de dominio.

Esto es así para **aislarnos de los posibles cambios por terceros** en esas implementaciones, y poder **falsear esos colaboradores a la hora de ejecutar nuestros tests**. En test, en vez de inyectar el repositorio de MySQL, inyectaremos uno en memoria para que se ejecuten más rápido (por ejemplo).

### Servicio de Aplicación -> Servicio de Dominio

A la hora de invocar un Servicio de Dominio desde uno de Aplicación, nos encontramos una situación diferente y por lo tanto trataremos este caso de forma distinta.

Los servicios de dominio, por definición, sólo contendrán lógica de negocio. Con lo cuál, **no necesitaremos desacoplarnos de ellos** como sí necesitábamos desacoplarnos de los servicios de infraestructura.

Además, **al no tocar entrada/salida, tampoco nos interesará inyectar una implementación diferente** de nuestro servicio de dominio durante la ejecución de nuestros tests.

Es más, nos interesará que nuestros tests pasen por el servicio de dominio a la hora de testear el caso de uso para así poder cubrirlo de forma indirecta.

Con lo cuál, los servicios de dominio **no tendrán una interface por encima** ya que es totalmente innecesaria. No aportaría más que complejidad a través del nivel de indirección adicional que suponen en nuestro sistema.

Algo que es discutible es si la lógica de instanciación de ese Servicio de Dominio le pertenece al Servicio de Aplicación tal y como mostramos en el vídeo o, a pesar de no tener una interface por encima, lo inyectamos ya instanciado al Servicio de Aplicación. Esto lo dejamos al gusto del consumidor ya que cada alternativa tiene sus pros y sus contras como comentamos en el vídeo 🙂
