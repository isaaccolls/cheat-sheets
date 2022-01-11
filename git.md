# generating SSH keys

`ssh-keygen -t rsa -b 4096 -C "isaac.colls@2brains.cl" -f bitbucket2brains`

# Configuracion básica de Git

```bash
git config --global --list
git config -global user.email your@email.com
git config -global user.name "Nombre Apellido"
```

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

- Crear repositorio local: `git init`
- Agrega el archivo al staging area(el limbo) -A nos agrega todos los archivos `git add [archivo]`
- Nos devolvemos un paso

```bash
git rm --cached
git rm --cached <file>
git rm --cached <diretory/*>
```

- Elimina el archivo por completo `git rm -f [file]`
- Que no haga nada, solo para ver en donde se encuentran los archivos y que podemos hacer con él `git add -n [file]`
- Para llevar del Staging Area al repository `git commit -m ["mensaje"]`
- Concatena nuevos cambios al utimo commit realizado `git commit -amend`
- Muestra la historia de todos los commits que hemos realizados `git log`
- stage only deleted files with git add `git ls-files --deleted | xargs git add`
- see the files changed in a commit `git show --name-only [sha]`
- change a remote git repository `git remote set-url origin git@your.git.repo.example.com:user/repository2.git`

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

## Branches

- list all branches `git branch -a`
- Mover entre ramas y entre commits `git checkout [nombre/sha1]`
- Crear una nueva rama sin necesidad de usar branch `git checkout -b [nombre_rama]`
- Merge. Ubicersa en la rama a partir de la cual se quiere absorber los cambios y ejecutar `git merge [nombre]`
- Cambiar un commit a otra rama `git cherry-pick [SHA1]`
- Delete local branch `git branch -d the_local_branch`
- To remove a remote branch `git push origin :the_remote_branch`
- rename local branch `git branch -m <new_name>`

## Stash

Es otro de los limbos, como el staging area. Para agregar los cambios estos deben estar en el staging area.

- agregar al stash `git stash`
- Muestra la lista de stash que tengamos `git stash list`
- aplicar y borrar stash `git stash pop`
- Borrar un stash `git stash drop stash@{numero}`
- remove stash `git stash drop`
- Aplicamos el último cambio `git stash apply stash@{numero}`

# Change Git Commit Date

- export next variables

```bash
export GIT_AUTHOR_DATE="2021-11-24T14:27:10-03:00" ; export GIT_COMMITTER_DATE="2021-11-24T14:27:10-03:00"
```

- change last commit date

```bash
GIT_COMMITTER_DATE="2021-10-18T10:02:27-03:00" git commit --amend --no-edit --date "2021-10-18T10:02:27-03:00"
```

- Revert back to wall clock time

```bash
unset GIT_AUTHOR_DATE && unset GIT_COMMITTER_DATE
```
