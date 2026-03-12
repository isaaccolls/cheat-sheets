- [Diseñar un Architecture Blueprint profesional (paso a paso)](#diseñar-un-architecture-blueprint-profesional-paso-a-paso)
  - [1. Definir el problema y los requisitos](#1-definir-el-problema-y-los-requisitos)
  - [2. Domain Modeling](#2-domain-modeling)
  - [3. Definir System Context (nivel 1 del C4)](#3-definir-system-context-nivel-1-del-c4)
  - [4. Definir Containers (nivel 2 del C4)](#4-definir-containers-nivel-2-del-c4)
  - [5. Diseñar Componentes internos (nivel 3 del C4)](#5-diseñar-componentes-internos-nivel-3-del-c4)
  - [6. deberia venir por aca el code diagram? (nivel 4 del C4)](#6-deberia-venir-por-aca-el-code-diagram-nivel-4-del-c4)
  - [7. Event Driven Architecture](#7-event-driven-architecture)
  - [8. Diseñar los flujos críticos](#8-diseñar-los-flujos-críticos)
  - [9. Diseñar la arquitectura de datos](#9-diseñar-la-arquitectura-de-datos)
  - [10. Diseñar la infraestructura](#10-diseñar-la-infraestructura)
  - [11. Deployment diagram](#11-deployment-diagram)
  - [12. Definir decisiones arquitectónicas (ADR)](#12-definir-decisiones-arquitectónicas-adr)
  - [13. Definir observabilidad](#13-definir-observabilidad)
  - [14. Seguridad](#14-seguridad)
  - [15. File structure](#15-file-structure)

# Diseñar un Architecture Blueprint profesional (paso a paso)

## 1. Definir el problema y los requisitos

- Objetivo del sistema: Qué problema resuelve?
- Requisitos funcionales
  - Ejemplo eCommerce:
    - crear órdenes
    - pagar órdenes
    - consultar órdenes
    - administrar inventario
- Requisitos no funcionales
  - escalabilidad
  - disponibilidad
  - seguridad
  - latencia
  - observabilidad
  - resiliencia
- Ejemplo:

```md
- Soportar 10k órdenes por minuto
- Disponibilidad 99.9%
- Latencia < 200ms
```

## 2. Domain Modeling

Antes de hablar de microservicios se definen bounded contexts usando conceptos de Domain-Driven Design.

Un eCommerce típico se separa así:

```
Customer
Catalog
Cart
Order
Payment
Inventory
Shipping
Notification
```

Cada uno representa un **dominio independiente**.

Ejemplo:

| Dominio   | Responsabilidad |
| --------- | --------------- |
| Catalog   | productos       |
| Cart      | carrito         |
| Order     | órdenes         |
| Payment   | pagos           |
| Inventory | stock           |
| Shipping  | despacho        |

## 3. Definir System Context (nivel 1 del C4)

Aquí se identifican los **actores** y **sistemas externos**.

Ejemplo eCommerce:

```
Customer
   │
   ▼
Ecommerce Platform
   │
   ├── Payment Gateway
   ├── Shipping Provider
   ├── Email Service
   └── Analytics
```

Actores:

- clientes
- admins
- sistemas externos

Esto responde: 👉 ¿Quién usa el sistema y con qué otros sistemas interactúa?

## 4. Definir Containers (nivel 2 del C4)

Aquí se separa el sistema en **aplicaciones** o **servicios principales**.

Ejemplo:

- servicios principales:

  ```
  Frontend (Web / Mobile)

  API Gateway

  Services
  ├── Catalog Service
  ├── Cart Service
  ├── Order Service
  ├── Payment Service
  ├── Inventory Service
  └── Notification Service
  ```

- Infraestructura:
  ```
  PostgreSQL
  Redis
  Message Broker
  Object Storage
  ```
  Esto responde: 👉 ¿Cuáles son las piezas principales del sistema?

## 5. Diseñar Componentes internos (nivel 3 del C4)

Dentro de cada servicio se define la estructura.

Ejemplo para **Order Service** usando [Hexagonal Architecture](./hexagonal.md):

```
API Controller
     │
Application Layer
     │
Domain
 ├── Order
 ├── OrderItem
 └── OrderService
     │
Ports
     │
Adapters
 ├── PostgreSQL
 ├── Redis
 └── Event Publisher
```

Esto responde: 👉 ¿Cómo está estructurado el código internamente?

## 6. deberia venir por aca el code diagram? (nivel 4 del C4)

El **nivel 4 del C4 (Code)** es opcional y se usa solo para las partes **críticas o muy complejas** del sistema. No se diagrama todo el código, sino:

- clases principales
- módulos/paquetes
- relaciones relevantes entre ellos

Objetivo: 👉 que otro dev pueda entender **cómo se implementa un componente clave** sin tener que leer todo el repo.

Ejemplo para el dominio de **Order** dentro de `Order Service`:

```
order/
 ├── application/
 │   ├── CreateOrderHandler
 │   ├── CancelOrderHandler
 │   └── OrderFacade
 ├── domain/
 │   ├── Order
 │   ├── OrderItem
 │   ├── OrderStatus
 │   └── OrderDomainService
 └── infrastructure/
     ├── OrderRepositoryPostgres
     ├── OrderOutboxPublisher
     └── OrderReadModelProjection
```

Otro estilo (tipo diagrama de clases simplificado):

```
CreateOrderHandler ---> OrderDomainService ---> OrderRepository (interface)
                                           └--> EventPublisher    (interface)

OrderRepositoryPostgres implements OrderRepository
KafkaEventPublisher   implements EventPublisher
```

Buenas prácticas:

- documentar solo:
  - dominios core (Order, Payment, Inventory…)
  - piezas con lógica compleja o alto riesgo
- mantener el diagrama cerca del código:
  - `architecture/diagrams/order-code.md`
  - o en el README del paquete
- actualizar el diagrama cuando haya refactors grandes

Esto responde: 👉 ¿Cómo se organiza el código a nivel de clases/módulos en una parte crítica del sistema?

## 7. Event Driven Architecture

Para desacoplar servicios se usan eventos.

Ejemplo flujo:

```
Order Created
     │
     ├── Inventory Service → reserva stock
     ├── Payment Service → procesa pago
     └── Notification Service → envía email
```

Eventos típicos:

```
OrderCreated
PaymentCompleted
InventoryReserved
OrderShipped
```

Esto se implementa con:

- Kafka
- RabbitMQ
- SQS

## 8. Diseñar los flujos críticos

Definen los flujos más importantes del sistema.

Ejemplo: **crear orden**

```
Cliente
   │
   ▼
API Gateway
   │
   ▼
Order Service
   │
   ├── Validar inventario
   ├── Crear orden
   └── Publica OrderCreated event
                │
                ▼
          Inventory Service
                │
                ▼
          Payment Service
```

Esto responde: 👉 ¿Cómo fluye la información en el sistema?

## 9. Diseñar la arquitectura de datos

Se definen:

- bases de datos
- ownership
- replicación
- consistencia

Ejemplo:

```
Catalog Service → catalog_db
Order Service → orders_db
Payment Service → payments_db
Inventory Service → inventory_db
```

Patrón común en microservicios: 👉 **Database per service**

## 10. Diseñar la infraestructura

Aquí se agrega el deployment.
Ejemplo:

```
CDN
 │
 ▼
Load Balancer
 │
 ▼
Kubernetes Cluster
 │
 ├── API Gateway
 ├── Order Service
 ├── Payment Service
 └── Inventory Service
```

Infra adicional:

- PostgreSQL Cluster
- Redis
- Kafka
- Object Storage

Esto responde: 👉 ¿Dónde corre el sistema?

## 11. Deployment diagram

Aquí se detalla **cómo se despliegan los contenedores/servicios en la infraestructura real**, normalmente por:

- entorno (dev / staging / prod)
- región / zona de disponibilidad
- nodos / clusters

Mientras que en el punto 10 se ve la **infraestructura lógica**, aquí se ve la **asignación concreta** de servicios a recursos de infraestructura.

Ejemplo (prod, una región, Kubernetes):

```
Internet
   │
   ▼
Cloud Provider (ej. AWS)
   │
   └── VPC
        │
        ├── Public Subnet
        │     ├── ALB / NLB (Load Balancer)
        │     └── NAT Gateway
        │
        └── Private Subnet
              ├── EKS Nodes (Kubernetes Worker Nodes)
              │     ├── Pod: api-gateway
              │     ├── Pod: order-service
              │     ├── Pod: payment-service
              │     └── Pod: inventory-service
              │
              ├── PostgreSQL Cluster
              └── Kafka Cluster
```

Puedes refinarlo por entorno:

```
dev
 └── 1 nodo k8s, 1 réplica por servicio, DB single instance

staging
 └── 2 nodos k8s, 2 réplicas por servicio, DB HA (read replica)

prod
 └── 3+ nodos k8s, 3+ réplicas por servicio, DB cluster multi-AZ
```

Puntos que el deployment diagram debería dejar claros:

- **alta disponibilidad**: réplicas, zonas, fallover
- **escalabilidad**: HPA / auto-scaling por servicio
- **fronteras de red**: público vs privado, security groups / firewalls
- **dependencias compartidas**: clusters de DB, colas, brokers

Esto responde: 👉 ¿Cómo se despliegan concretamente los servicios en la infraestructura (por entorno, región y nodos)?

## 12. Definir decisiones arquitectónicas (ADR)

Cada decisión importante se documenta.

Ejemplo:

```
ADR-001: Usar arquitectura de microservicios

Contexto:
El sistema debe escalar independientemente.

Decisión:
Separar Order, Payment y Inventory.

Consecuencia:
Mayor complejidad operativa.
```

## 13. Definir observabilidad

- logs
- métricas
- tracing

Ejemplo stack:

- logs → ELK
- métricas → Prometheus
- tracing → OpenTelemetry

## 14. Seguridad

- Auth Service
- JWT
- API Gateway validation
- Rate limiting
- Secrets manager

## 15. File structure

La estructura de archivos debe ayudar a:

- encontrar rápido los **diagramas C4**
- localizar las **decisiones (ADR)**
- conectar la documentación con el **código real** del eCommerce

Idea general: separar **arquitectura** de **implementación**, pero mantener enlaces claros entre ambas.

Ejemplo de estructura para un eCommerce basado en microservicios:

```
architecture/
 ├── system-context.md          # C4 nivel 1
 ├── containers.md              # C4 nivel 2
 ├── components.md              # C4 nivel 3 (por servicio)
 ├── code-diagrams.md           # C4 nivel 4 (solo piezas críticas)
 ├── deployment.md              # Diagramas de infraestructura / deployment
 ├── data-architecture.md       # Bases de datos, ownership, replicación
 ├── event-architecture.md      # Eventos de dominio, contratos, canales
 ├── decisions/
 │    ├── adr-001-microservices.md
 │    ├── adr-002-postgresql.md
 │    ├── adr-003-kafka-vs-rabbitmq.md
 │    └── adr-004-outbox-pattern.md
 ├── runbooks/                  # Qué hacer ante incidentes
 │    ├── cart-inconsistency.md
 │    ├── payment-timeout.md
 │    └── inventory-desync.md
 └── diagrams/
      ├── c4-level1-system-context.drawio
      ├── c4-level2-containers.drawio
      ├── order-components-level3.drawio
      └── prod-deployment.drawio
```

Y cómo se conecta con el código del eCommerce:

```
src/
 ├── services/
 │    ├── catalog-service/
 │    │    ├── src/
 │    │    ├── tests/
 │    │    └── README.md              # link a secciones de architecture/
 │    ├── cart-service/
 │    ├── order-service/
 │    │    ├── src/
 │    │    │    ├── order/
 │    │    │    │    ├── application/
 │    │    │    │    ├── domain/
 │    │    │    │    └── infrastructure/
 │    │    ├── tests/
 │    │    └── README.md              # referencia a code-diagrams.md y ADRs
 │    └── payment-service/
 └── infra/
      ├── k8s/
      │    ├── dev/
      │    ├── staging/
      │    └── prod/
      └── terraform/
```

Casos de borde que la estructura debería contemplar:

- **multi-región / multi-tenant**:
  - `deployment.md` y `prod-deployment.drawio` deben mostrar regiones, tenants y aislamiento
  - posible subcarpeta `architecture/deployment/` para diagramas por región
- **servicios compartidos críticos** (ej. Payment, Auth):
  - ADRs específicos (`adr-010-shared-payment-service.md`)
  - diagramas de código dedicados en `code-diagrams.md` o archivos separados
- **compatibilidad hacia atrás de eventos**:
  - sección en `event-architecture.md` sobre versionado de eventos
  - ejemplos de payloads y políticas de deprecación
- **consistencia eventual vs fuerte**:
  - documentar en `data-architecture.md` qué operaciones son eventualmente consistentes (ej. stock, reporting)
  - runbooks para estados inconsistentes (ej. `inventory-desync.md`)

Regla práctica: 👉 si algo es **lo bastante complejo** como para romper producción o generar bugs sutiles (pagos, stock, envíos, multi-moneda, multi-tenant), merece:

- un ADR
- un diagrama asociado
- y, si aplica, un runbook de incidentes
```
