- [generating SSH keys](#generating-ssh-keys)
- [config](#config)
  - [change user](#change-user)
- [Basic commands](#basic-commands)
  - [Versionar proyecto](#versionar-proyecto)
  - [diferencias entre un commit y otro](#diferencias-entre-un-commit-y-otro)
  - [Reset](#reset)
  - [Branches](#branches)
  - [Stash](#stash)
- [Change Git Commit Date](#change-git-commit-date)
- [Branch naming conventions](#branch-naming-conventions)
  - [Git branch prefixes](#git-branch-prefixes)
  - [Example of branch naming in action](#example-of-branch-naming-in-action)

# generating SSH keys

`ssh-keygen -t rsa -b 4096 -C "isaac.colls@2brains.cl" -f bitbucket2brains`

# config

- list: `git config --global --list`
- email: `git config -global user.email your@email.com`
- name: `git config -global user.name "Nombre Apellido"`
- .gitignore alternative: `.git/info/exclude`
- pull fast-forward only: `git config --global pull.rebase false`
- remove some entry: `git config --global --unset <property>`

## change user

- Change username and email global

```bash
git config --global user.name "Nanhe Kumar"
git config --global user.email "info@nanhekumar.com"
```

- Change username and email for current repo

```bash
git config user.name "Nanhe Kumar"
git config user.email "info@nanhekumar.com"
```

# Basic commands

- crear repositorio local: `git init`
- agrega el archivo al staging area(el limbo) -A nos agrega todos los archivos `git add [archivo]`
  - remover archivo del staging area: `git reset HEAD <file>`
- elimina el archivo por completo `git rm -f [file]`
- que no haga nada, solo para ver en donde se encuentran los archivos y que podemos hacer con él `git add -n [file]`
- para llevar del Staging Area al repository `git commit -m ["mensaje"]`
- concatena nuevos cambios al utimo commit realizado `git commit -amend`
- muestra la historia de todos los commits que hemos realizados `git log`
- stage only deleted files with git add `git ls-files --deleted | xargs git add`
- see the files changed in a commit `git show --name-only [sha]`
- change a remote git repository `git remote set-url origin git@your.git.repo.example.com:user/repository2.git`
- pull: `git pull <remote> <branch>`
  - accept all incoming: `git pull -X theirs`

## Versionar proyecto

- Etiquetas ligeras `git tag [version]`
- Etiquetas anotadas `git tag -a [version] -m ["mensaje"]`
- Para etiquetar veriones pasadas del proyecto se necesita el SHA-1 del commit `git tag [version] [SHA-1] (Del Tag ligero)`
- Borrar release `git tag -d [version]`
- Renombrar `git tag -f -a [version] -m ["mensaje"] [SHA-1]`
- Ver la lista de tags `git tag -l`
- alias `git config --global alias.superlog "log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"`

## diferencias entre un commit y otro

- Muestra los cambios del estado actual con el commit que dado `git diff [SHA1]`
- Mostrar los cambios del commit (1) con respecto al commit (2). El orden de los parametros importa `git diff [SHA1(1)] [SHA-1(2)]`

## Reset

- Quitar los cambios de un commit específico. Deja los archivos en el staging area, listos para hacer un commit `git reset --soft [SHA1]`
- Nos elimina los cambios, también del staging area `git reset --mixed [SHA1]`
- Elimina los cambios incluso del working directory, es el más peligroso de todos `git reset --hard [SHA1]`
- reset one file 👽 `git checkout -- [file]`
- extract file from staging `git reset [file]`
- rebase: `git rebase -i HEAD~9`

## Branches

- list all branches `git branch -a`
- Mover entre ramas y entre commits `git checkout [nombre/sha1]`
- Crear una nueva rama sin necesidad de usar branch `git checkout -b [nombre_rama]`
- download commits, refs, and files: `git fetch`
  - remote: `git fetch <remote>` ex: `git fetch origin`
  - specific branch: `git fetch <remote> <branch>`
  - all option: `git fetch --all`
- Merge. Ubicarse en la rama a partir de la cual se quiere absorber los cambios y ejecutar `git merge [nombre]`
  - prevents merging in a fast-forward way: `git merge --no-ff`
- Cambiar un commit a otra rama `git cherry-pick [SHA1]`
- Delete local branch `git branch -d the_local_branch`
- delete all local branches except the current one: `git branch | grep -v "$(git branch --show-current)" | xargs git branch -D`
- To remove a remote branch `git push origin :the_remote_branch`
- rename local branch `git branch -m <new_name>`

## Stash

is a temporary storage

- save a stash: `git stash`
- save a stash with a message: `git stash save <message>`
- list multiple stashes: `git stash list`
- remove stash last stash: `git stash drop`
  - remove particular stash: `git stash drop <stash_id>`
- reapply last stash and remove: `git stash pop`
  - reapply particular stash: `git stash apply <stash_id>`
- stashing untracked files: `git stash -u`
- create branch from stash: `git stash branch <branch_name> <stash_id>`

# Change Git Commit Date

- export next variables: `export GIT_AUTHOR_DATE="2022-05-03T16:21:12-04:00" ; export GIT_COMMITTER_DATE="2022-05-03T16:21:12-04:00"`
  - Revert back to wall clock time `unset GIT_AUTHOR_DATE && unset GIT_COMMITTER_DATE`
- change last commit date: `GIT_COMMITTER_DATE="2022-03-21T10:12:11-03:00" git commit --amend --no-edit --date "2022-03-21T10:12:11-03:00"`

# Branch naming conventions

## Git branch prefixes

Using prefixes in branch names is a popular strategy to categorize branches based on their purpose:

- Feature branches: Prefixed with `feature/`, these branches are used to develop new features.
- Bugfix branches: Prefixed with `bugfix/`, these branches are used to make fixes.
- Release branches: Prefixed with `release/`, these branches prepare a codebase for new releases.
- Hotfix branches: Prefixed with `hotfix/`, these branches address urgent issues in production.

## Example of branch naming in action

```bash
# Creating a new feature branch
git checkout -b feature/add-user-authentication
# Switching to a bugfix branch
git checkout -b bugfix/login-issue
# Creating new release branch
git checkout -b release/v2.0.0
# Preparing a hotfix
git checkout -b hotfix/reset-password-fix
```
