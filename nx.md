# install

`npm i -g nx`

# nest

## app

- generate app: `nx generate @nrwl/nest:app my-nest-app`

## module

- help: `nx g module --help`
- generate module: `nx generate @nrwl/nest:module --name [some-cool-name] --project [some-cool-project]`

## controller

- generate controller: `nx generate @nrwl/nest:controller --name Health --project [some-cool-project]`

## service

- generate service: `nx generate @nrwl/nest:service --name status --project db-migrator`

## lib

- help: `nx g lib --help`
- generate lib: `nx g @nrwl/nest:lib {some-cool-name} --routing`
