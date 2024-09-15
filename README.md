# Pasos a seguir, Práctica Git & GitHub, Punto 1

## 1. Crear un repositorio en GitHub y clónalo en tu equipo

```bash
git clone https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
cd Alex-BdMlAi14-Git-Point1
touch .gitignore
touch .gitattributes
git add .
git commit -m "Adding Essential Git Files"
```

## 2. Crear un archivo `git-nuestro.md` con el contenido:

```
Git nuestro
Git nuestro que estas en los repos
Comprimidos sean tus commits
Venga a nosotros tu log
En el local como en el remote
Danos hoy nuestro pull de cada día
Perdona nuestros conflictos
Como también perdonamos los de otros geeks
No nos dejes caer en detached HEAD
y líbranos de SVN
git commit --amend
```

```bash
touch git-nuestro.md
# (File Modified in Text Editor)
```

## 3. Añadir `git-nuestro.md` al staging area

```bash
git add git-nuestro.md
```

## 4. Mover lo que hay en el staging area al repositorio

```bash
git commit -m "Adding git-nuestro.md"
```

## 5. Crear una rama llamada `styled`

```bash
git branch styled
```

## 6. Listar las ramas que hay en el repositorio

```bash
git branch
```

## 7. Moverse a la rama `styled`

```bash
git checkout styled
```

## 8. Comprobar que se está en la rama correcta

```bash
git branch
```

## 9. Modificar en el archivo `git-nuestro.md`:

```
*Git* nuestro que estás en los repos
Comprimidos sean tus *commits*
Venga a nosotros tu *log*
En el local como en el *remote*
Danos hoy nuestro *pull* de cada día
Perdona nuestros *conflictos*
Como también perdonamos los de otros geeks
No nos dejes caer en *detached HEAD*
y líbranos de *SVN*
`git commit --amend`
```

```bash
# (File Modified in Text Editor)
```

## 10. Añadir los cambios al staging area y luego pasarlos al repositorio

```bash
git add git-nuestro.md
git commit -m "Modified git-nuestro.md"
```

## 11. Deshacer el último commit (perdiendo los cambios realizados en el working copy)

```bash
git reflog show --pretty=oneline
git reset --hard 423b964
```

## 12. Rehacer el último commit (el que acabamos de deshacer)

```bash
git reflog show --pretty=oneline
git show HEAD@{1}
git reset --hard a65c9598db386e3126ab0f5c2c319e5086cca26a
```

## 13. Hacer un merge con `main` (styled absorbe a main)

```bash
git checkout styled
git diff main..styled
git merge --ff main
git status
git log --oneline --graph
```

## 14. Volver a la rama `main`

```bash
git checkout main
```

## 15. Crear una nueva rama llamada `htmlify`

```bash
git branch htmlify
```

## 16. Cambiar a la rama `htmlify`

```bash
git checkout htmlify
```

## 17. Modificar en el archivo `git-nuestro.md`:

```html
<p><em>Git</em> nuestro que estas en los repos<br />
Comprimidos sean tus <em>commits</em><br />
Venga a nosotros tu <em>log</em><br />
En el local como en el <em>remote</em><br />
Danos hoy nuestro <em>pull</em> de cada día<br />
Perdona nuestros <em>conflictos</em><br />
Como también perdonamos los de otros geeks<br />
No nos dejes caer en <em>detached HEAD</em><br />
y líbranos de <em>SVN</em><br />
<code>git commit --amend</code></p>
```

```bash
# (File Modified in Text Editor)
```

## 18. Hacer un commit

```bash
git add git-nuestro.md
git commit -m "Modified Again git-nuestro.md"
```

## 19. Hacer un merge de `htmlify` en `styled` (styled absorbe a htmlify)

```bash
git checkout styled
git diff htmlify..styled
git log --oneline styled
git log --oneline htmlify
git merge --ff htmlify
```

## 20. Si hay conflictos, deberemos resolverlos quedándonos con el contenido de la rama `styled`.

```bash
git add git-nuestro.md
git commit
```

## 21. Desde `main`, hacer un merge con `styled`

```bash
git checkout main
git merge --ff styled
```

## 22. Crear una rama `title` y cambiarse a esa rama

```bash
git branch title
git checkout title
```

## 23. Añadir un título (a tu gusto) al archivo `git-nuestro.md` y hacer un commit.

```markdown
# Oracion a Git - BDMLAI14 - Alex
*Git* nuestro que estás en los repos
Comprimidos sean tus *commits*
Venga a nosotros tu *log*
En el local como en el *remote*
Danos hoy nuestro *pull* de cada día
Perdona nuestros *conflictos*
Como también perdonamos los de otros geeks
No nos dejes caer en *detached HEAD*
y líbranos de *SVN*
`git commit --amend`
```

```bash
# (File Modified in Text Editor)
git add git-nuestro.md
git commit -m "Adding Title git-nuestro.md"
```

## 24. Volver a la rama `main`

```bash
git checkout main
```

## 25. Dibujar el diagrama

```bash
git log --all --decorate --oneline --graph
```

## 26. Hacer un merge “no fast-forward” de `title` en `main` (main absorbe a title)

```bash
git checkout main
git merge --no-ff title
```

## 27. Deshacer el merge (sin perder los cambios del working copy)

```bash
git diff d6a45e2 HEAD -- git-nuestro.md
git reset --soft d6a45e2
```

## 28. Descartar los cambios (volver sin title)

```bash
git diff --staged git-nuestro.md
git restore --staged git-nuestro.md
git restore git-nuestro.md
```

## 29. Eliminar la rama `title`

```bash
git branch -D title
```

## 30. Rehacer el merge que hemos deshecho

```bash
git reflog show --pretty=oneline
git diff 7c676cc HEAD -- git-nuestro.md
git reset --hard 7c676cc
```

## 31. Volver a `main` y eliminar el resto de ramas

```bash
git checkout main
git branch -D styled htmlify
```

## 32. Volver al commit inicial cuando se creó el poema

```bash
git reflog show --pretty=oneline
git reset --hard 423b964
```

## 33. Volver al estado final, cuando pusimos título al poema

```bash
git reflog show --pretty=oneline
git reset --hard 3389496
```

## 34. Crear los siguientes tags:

```bash
git log --pretty=oneline
git tag inicial 423b964eaf9aeb59aa4e0e788b7b052d1e538691
git tag styled a65c9598db386e3126ab0f5c2c319e5086cca26a
git tag htmlify 842b0492248b22108eff9b7d462fc14f7fcdfdc8
git tag title 3389496cfb40ea5d2c1e0d8ad9fd408731aa9671
```

## 35. Ir al tag `htmlify`

```bash
git checkout htmlify
```

## 36. Vuelve a la rama `main`

```bash
git checkout main
```

## 37. Subir a GitHub todas las ramas y todos los tags

```bash
git remote set-url origin git@github.com:algond123/Alex-BdMlAi14-Git-Point1.git
git remote -v
git push --all origin
git push --tags origin
```
