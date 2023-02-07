- [basic commands](#basic-commands)
- [modules](#modules)
- [controllers](#controllers)
- [services](#services)
- [entities](#entities)
- [data transfer objects](#data-transfer-objects)
- [validation pipe](#validation-pipe)
- [migrations](#migrations)
- [building blocks](#building-blocks)
  - [Exception filters](#exception-filters)
  - [Pipes](#pipes)
  - [Guards](#guards)
  - [Interceptors](#interceptors)
- [Middleware](#middleware)
- [swagger module](#swagger-module)
- [testing](#testing)
  - [unit tests](#unit-tests)
  - [end-to-end (e2e) tests](#end-to-end-e2e-tests)
- [style guide of naming conventions](#style-guide-of-naming-conventions)

# basic commands

- install: `npm i -g @nestjs/cli`
- check version: `nest -v`
- help: `nest -h`
- create application: `nest new`
- start up application: `npm run start`
  - development mode: `npm run start:dev`

# modules

contain 4 main things:

- controllers: API Routes
- exports: ist providers within this current module that should be made available anywhere this module is imported
- imports: list OTHER modules that THIS module requires
- providers: list our services that need to be instantiated by the Nest injector. Any providers here will be available only within _"THIS"_ module itself, unless added to the exports array

commands:

- generate module: `nest generate module {name}` or `nest g mo {name}`

# controllers

handle requests

- generate controller: `nest generate controller` or `nest g co`
  - without test file: `nest g co --no-spec`
  - specify location: `nest g co modules/abc`
  - test before create: `nest g co modules/abc --dry-run`

# services

each service is a provider, it can inject dependencies

- generate service: `nest generate service` or `nest g s`

# entities

Entities may be part of a business domain. Thus, they can implement behavior and be applied to different use cases within the domain.

- generate class: `nest g class coffees/entities/coffee.entity.ts --no-spec`

```ts
@Entity()
export class Coffee {
  @PrimaryGeneratedColumn()
  id: number;
  @Column()
  name: string;
  @Column()
  brand: string;
  @Column()
  flavors: string[];
}
```

# data transfer objects

DTOs are used only to transfer data from one processor context to another. As such, they are without behavior - except for very basic and usually standardized storage and retrieval functions.

- generate dto: `nest g class coffees/dto/create-coffee.dto --no-spec`
- _example_: you want data for the _signup_ **route** which is _passed_ in _body_:
  ```ts
  export class CreateCoffeeDto {
    readonly name: string;
    readonly brand: string;
    readonly flavors: string[];
  }
  ```

# validation pipe

provides a convenient way of enforcing validation rules for all incoming client payloads

- install: `npm i class-validator class-transformer`
  - add: `app.useGlobalPipes(new ValidationPipe());` to `main.ts` file
  - install for using partial: `npm i @nestjs/mapped-types`

# migrations

- creating a typeorm migration: `npx typeorm migration:create src/migrations/CoffeeRefactor`
- compile project first: `npm run build`
- run migration(s): `npx typeorm migration:run -d dist/typeorm-cli.config`
  - revert migration(s): `npx typeorm migration:revert -d dist/typeorm-cli.config`
- let typeorm generate migrations (for you): `npx typeorm migration:generate src/migrations/SchemaSync -d dist/typeorm-cli.config`

# building blocks

- Globally-scoped
- Controller-scoped
- Method-scoped
- Param-scoped (is available to Pipes only)

## Exception filters

responsible for handling and processing unhandled exceptions that _might_ occur in the application

- generate: `nest g filter common/filters/http-exception`

## Pipes

- transformations: transform input data to the desired output
- validation: evaluate input data
- generate: `nest g pipe common/pipes/parse-int`

## Guards

determine whether a given request meets certain conditions, like authentication, authorization, roles, ACLs, etc. And if the conditions are met, the requests will be _allowed_ to access the route

- generate: `nest g guard common/guards/api-key`
- use: `app.useGlobalGuards(new ApiKeyGuard());` or as custon module

## Interceptors

- bind extra logic, before or after method execution
- tranform the result returned from a method
- extend basic method behavior
- _override_ a method, depending on specific conditions. Example: _caching responses_
- generate: `nest g interceptor common/interceptors/wrap-response`

# Middleware

Middleware is a function that is called _before_ the route handler and any other building blocks are processed. This includes Interceptors, Guards and Pipes.

Middleware functions have access to the request and response objects, and are not specifically tied to any method, but rather to a specified route **PATH**.

Middleware functions can perform the following tasks:

- executing code
- making changes to the request and the response objects.
- ending the request-response cycle.
- Or even calling the next middleware function in the call stack.

When working with middleware, if the current middleware function does not END the request-response cycle, it must call the next() method, which passes control to the next middleware function. Otherwise, the request will be left hanging - and never complete.

- generate: `nest g middleware common/middleware/logging`

# swagger module

- install dependencies: `npm install --save @nestjs/swagger swagger-ui-express`
- Add the _@nestjs/swagger_ plugin to our application _nest-cli.json_:
  ```json
  "compilerOptions": {
    "deleteOutDir": true,
    "plugins": ["@nestjs/swagger/plugin"] // 👈
  }
  ```

# testing

built-in integration with _Jest_

## unit tests

focus on individual classes and functions

- Each controller, provider, service, etc. should have it
- Extension must be: `(dot).spec.ts`
- run unit tests: `npm run test`
  - for _specific_ file pattern: `npm run test:watch -- coffees.service`
- run unit tests + collecting testing coverage: `npm run test:cov`

## end-to-end (e2e) tests

great for high-level validation of the entire system.
Closer to the kind of interaction that end-users will have with the production system

- located in a dedicated `test` directory by default
- typically grouped into separate files by the feature or functionality
- extension must be: `(dot).e2e-spec.ts`
- run e2e tests: `npm run test:e2e`
  - for _specific_ file pattern: `npm run test:e2e -- coffees`
- package.json pre & post hook additions: `"pretest:e2e"` and `"posttest:e2e"`

# style guide of naming conventions

- controller: `user.controller.ts` 👉 `@Controller() export class UserController { ... }`
- service: `user.service.ts` 👉 `@Injectable() export class UserService { ...  }`
- module: `user.module.ts` 👉 `@Module() export class UserModule { ... }`
- middleware: `authentication.middleware.ts` 👉 `@Injectable() export class AuthenticationMiddleware { ... }`
- exception filter: `forbidden.exception.ts` 👉 `export class ForbiddenException { ... }`
- pipe: `validation.pipe.ts` 👉 `@Injectable() export class ValidationPipe { ... }`
- guard: `roles.guard.ts` 👉 `@Injectable() export class RolesGuard { ... }`
- interceptor: `logging.interceptor.ts` 👉 `@Injectable() export class LoggingInterceptor { ... }`
- custom decorator: `comment.decorator.ts` 👉 `export const Comment...`
- gateway `comment.gateway.ts` 👉 `@WebSocketGateway() export class CommentGateway { ... }`
- adapter: `ws.adapter.ts` 👉 `export class WsAdapter { ... }`
- unit test: `user.service.spec.ts`
- E2E test: `user.e2e-spec.ts`
