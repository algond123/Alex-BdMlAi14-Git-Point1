# Práctica Git & GitHub, Punto 1

-------

## Preguntas Ejercicio 1

Se deberá crear un repositorio y realizar una serie de operaciones desde la consola de comandos sobre el mismo para posteriormente subir el repositorio a Github. Se deberá entregar a través del formulario de prácticas indicando la URL del repositorio. En el repositorio, deberá existir un archivo `readme.md` con las respuestas a las siguientes preguntas:

### 1. ¿Qué comando utilizaste en el paso 11? ¿Por qué?
**Paso 11:** Deshacer el último commit (perdiendo los cambios realizados en el working copy).

**Comandos:**
```bash
git reset --hard 423b964
```

**Aux Comandos:**
```bash
git reflog show --pretty=oneline
423b964 (main) HEAD@{2}: reset: moving to 423b964
a65c959 (HEAD -> styled) HEAD@{3}: commit: Modified git-nuestro.md
423b964 (main) HEAD@{4}: checkout: moving from main to styled
423b964 (main) HEAD@{5}: commit: Adding git-nuestro.md
3f6188a HEAD@{6}: commit: Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) HEAD@{7}: clone: from https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
```

**Explicación:**  
Con `reflog` vemos el hash del commit al que queremos llegar en este caso `423b964`, despues hacemos un `reset --hard` con el que perdemos los cambios en el staging y working area

### 2. ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?
**Paso 12:** Rehacer el último commit (el que acabamos de deshacer).

**Comandos:**
```bash
git reset --hard a65c959
```

**Aux Comandos:**
```bash
git reflog show --pretty=oneline
a65c959 (HEAD -> styled) HEAD@{0}: checkout: moving from styled to styled
a65c959 (HEAD -> styled) HEAD@{1}: reset: moving to a65c9598db386e3126ab0f5c2c319e5086cca26a
423b964 (main) HEAD@{2}: reset: moving to 423b964
a65c959 (HEAD -> styled) HEAD@{3}: commit: Modified git-nuestro.md
423b964 (main) HEAD@{4}: checkout: moving from main to styled
423b964 (main) HEAD@{5}: commit: Adding git-nuestro.md
3f6188a HEAD@{6}: commit: Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) HEAD@{7}: clone: from https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
```

**Explicación:**  
Con `reflog` vemos el hash del commit al que queremos llegar en este caso `a65c959`, despues hacemos un `reset --hard` con el que perdemos los cambios en el staging and working area

### 3. ¿El merge del paso 13 causó algún conflicto? ¿Por qué?
**Paso 13:** Hacer un merge con `main` (styled absorbe a main).

**Comandos:**
```bash
$ git merge --ff main (styled)
Already up to date.
```
**Aux Comandos:**
```bash
$ git log --oneline main (styled)
423b964 (main) Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit

$ git log --oneline styled (styled)
a65c959 (HEAD -> styled) Modified git-nuestro.md
423b964 (main) Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit
```

**Explicación:**  
No hubo nignun conflicto, pero el `styled` no pudo absorber al `main`, debido a que el ancestro comun de ambos branches era el hash `423b964`, entonces ya el branch `styled` ya tenia integrados todos los ultimos commit del `main`. Si el `main` hubiera tenido nuevos commits se hubiera podido hacer un merge de ambos branches.

### 4. ¿El merge del paso 19 causó algún conflicto? ¿Por qué?
**Paso 19:** Hacer un merge de “htmlify” en “styled” (styled absorbe a htmlify).

**Comandos:**
```bash
$ git merge --ff htmlify (styled)
Auto-merging git-nuestro.md
CONFLICT (content): Merge conflict in git-nuestro.md
Automatic merge failed; fix conflicts and then commit the result.
```

**Aux Comandos:**
```bash
$ git status (styled|MERGING)
On branch styled
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   git-nuestro.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git add git-nuestro.md
$ git commit
[styled d6a45e2] Merge branch 'htmlify' into styled
```

**Explicación:**  
Hubo un conflicto debido a que ambos braches, habia modificado el archivo desde el commit `423b964`, entonces se tenia que decidir con que contenido del archivo quedarse con el de `styled` o el `htmlify`. Despues de decir el conteido del archivo se pocedia a agregaros del working al staging area, para depues proceder hacer un commit.

### 5. ¿El merge del paso 21 causó algún conflicto? ¿Por qué?
**Paso 21:** Desde `main`, hacer un merge con `styled`.

**Comandos:**
```bash
$ git merge --ff styled
Updating 423b964..d6a45e2
Fast-forward
 git-nuestro.md | 19 +++++++++----------
 1 file changed, 9 insertions(+), 10 deletions(-)
```

**Aux Comandos:**
```bash
$ git log --oneline styled
d6a45e2 (HEAD -> main, styled) Merge branch 'htmlify' into styled
842b049 (htmlify) Modified Again git-nuestro.md
a65c959 Modified git-nuestro.md
423b964 Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit

$ git log --oneline main
d6a45e2 (HEAD -> main, styled) Merge branch 'htmlify' into styled
842b049 (htmlify) Modified Again git-nuestro.md
a65c959 Modified git-nuestro.md
423b964 Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit
```

**Explicación:**  
No hubo ningun conflicto e hizo directamete el `merge fast-forward`, debido a que main tenia un ancestro comun con `styled` el hash `423b964`, entonces como todas los nuevos commits de `main` estaban integrados en `styled`, cuando se hizo el merge lo uico que paso es que se copiaron los nuevos commits de `styled` en `main`.

### 6. ¿Qué comando o comandos utilizaste en el paso 25?
**Paso 25:** Dibujar el diagrama.

**Comandos:**
```bash
$ git log --all --decorate --oneline --graph
* 3389496 (title) Adding Title git-nuestro.md
*   d6a45e2 (HEAD -> main, styled) Merge branch 'htmlify' into styled
|\
| * 842b049 (htmlify) Modified Again git-nuestro.md
* | a65c959 Modified git-nuestro.md
|/
* 423b964 Adding git-nuestro.md
* 3f6188a Adding Essential Git Files
* 255e6a5 (origin/main, origin/HEAD) Initial commit
```

### 7. ¿El merge del paso 26 podría ser fast forward? ¿Por qué?
**Paso 26:** Hacer un merge “no fast-forward” de `title` en `main`.

**Comandos:**
```bash
$ git merge --no-ff title
Merge made by the 'ort' strategy.
 git-nuestro.md | 1 +
 1 file changed, 1 insertion(+)
```

**Aux Comandos:**
```bash
$ git log --oneline main
7c676cc (HEAD -> main) Merge branch 'title'
3389496 (title) Adding Title git-nuestro.md
d6a45e2 (styled) Merge branch 'htmlify' into styled
842b049 (htmlify) Modified Again git-nuestro.md
a65c959 Modified git-nuestro.md
423b964 Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit

$ git log --oneline title
3389496 (title) Adding Title git-nuestro.md
d6a45e2 (styled) Merge branch 'htmlify' into styled
842b049 (htmlify) Modified Again git-nuestro.md
a65c959 Modified git-nuestro.md
423b964 Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit
```

**Explicación:**  
Si hubiera podido ser `fast-forward` debdo a que ambos branch tenian un ancestro en comun `3389496`, y ya `title` tenia todas las actulizaciones del `main`, entonces en el `merge` solo eran copiar las ultimas modificaciones de `title` en `main`.

### 8. ¿Qué comando o comandos utilizaste en el paso 27?
**Paso 27:** Deshacer el merge (sin perder los cambios del working copy).

**Comandos:**
```bash
git reset --soft d6a45e2
```

**Aux Comando:**
```bash
$ git diff d6a45e2 HEAD -- git-nuestro.md
diff --git a/git-nuestro.md b/git-nuestro.md
index a0cbbee..81b3b1d 100644
--- a/git-nuestro.md
+++ b/git-nuestro.md
@@ -1,3 +1,4 @@
+# Oracion a Git - BDMLAI14 - Alex
 *Git* nuestro que estás en los repos
 Comprimidos sean tus *commits*
 Venga a nosotros tu *log*

$ git log --oneline main
d6a45e2 (HEAD -> main, styled) Merge branch 'htmlify' into styled
842b049 (htmlify) Modified Again git-nuestro.md
a65c959 Modified git-nuestro.md
423b964 Adding git-nuestro.md
3f6188a Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) Initial commit
```

### 9. ¿Qué comando o comandos utilizaste en el paso 28?
**Paso 28:** Descartar los cambios.

**Comandos:**
```bash
git restore --staged git-nuestro.md
git restore git-nuestro.md
```

**Aux Comandos:**
```bash
$ git diff --staged git-nuestro.md
diff --git a/git-nuestro.md b/git-nuestro.md
index a0cbbee..81b3b1d 100644
--- a/git-nuestro.md
+++ b/git-nuestro.md
@@ -1,3 +1,4 @@
+# Oracion a Git - BDMLAI14 - Alex
 *Git* nuestro que estás en los repos
 Comprimidos sean tus *commits*
 Venga a nosotros tu *log*

$ git status
On branch main
Your branch is ahead of 'origin/main' by 5 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git-nuestro.md

$ git status
On branch main
Your branch is ahead of 'origin/main' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-nuestro.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git status
On branch main
Your branch is ahead of 'origin/main' by 5 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

### 10. ¿Qué comando o comandos utilizaste en el paso 29?
**Paso 29:** Eliminar la rama “title”.

**Comandos:**
```bash
git branch -D title
```

**Aux Comandos:**
```bash
$ git branch
  htmlify
* main
  styled
  title

$ git branch
  htmlify
* main
  styled
```

### 11. ¿Qué comando o comandos utilizaste en el paso 30?
**Paso 30:** Rehacer el merge que hemos deshecho.

**Comandos:**
```bash
git reset --hard 7c676cc
```

**Aux Comandos:**
```bash
$ git diff 7c676cc HEAD -- git-nuestro.md
diff --git a/git-nuestro.md b/git-nuestro.md
index 81b3b1d..a0cbbee 100644
--- a/git-nuestro.md
+++ b/git-nuestro.md
@@ -1,4 +1,3 @@
-# Oracion a Git - BDMLAI14 - Alex
 *Git* nuestro que estás en los repos
 Comprimidos sean tus *commits*
 Venga a nosotros tu *log*

$ git reset --hard 7c676cc
HEAD is now at 7c676cc Merge branch 'title'

$ git branch
  htmlify
* main
  styled
```

### 12. ¿Qué comando o comandos usaste en el paso 32?
**Paso 32:** Volver al commit inicial cuando se creó el poema.

**Comandos:**
```bash
git reset --hard 423b964
```

**Aux Comandos:**
```bash
$ git reflog show --pretty=oneline
423b964 (HEAD -> main) HEAD@{0}: reset: moving to 423b964
7c676cc HEAD@{1}: checkout: moving from main to main
7c676cc HEAD@{2}: reset: moving to 7c676cc
d6a45e2 HEAD@{3}: reset: moving to d6a45e2
3389496 HEAD@{4}: reset: moving to 3389496
7c676cc HEAD@{5}: merge title: Merge made by the 'ort' strategy.
d6a45e2 HEAD@{6}: checkout: moving from main to main
d6a45e2 HEAD@{7}: checkout: moving from title to main
3389496 HEAD@{8}: commit: Adding Title git-nuestro.md
d6a45e2 HEAD@{9}: checkout: moving from main to title
d6a45e2 HEAD@{10}: merge styled: Fast-forward
423b964 (HEAD -> main) HEAD@{11}: checkout: moving from styled to main
d6a45e2 HEAD@{12}: commit (merge): Merge branch 'htmlify' into styled
a65c959 HEAD@{13}: checkout: moving from htmlify to styled
842b049 HEAD@{14}: commit: Modified Again git-nuestro.md
423b964 (HEAD -> main) HEAD@{15}: checkout: moving from main to htmlify
423b964 (HEAD -> main) HEAD@{16}: checkout: moving from styled to main
a65c959 HEAD@{17}: checkout: moving from styled to styled
a65c959 HEAD@{18}: reset: moving to a65c9598db386e3126ab0f5c2c319e5086cca26a
423b964 (HEAD -> main) HEAD@{19}: reset: moving to 423b964
a65c959 HEAD@{20}: commit: Modified git-nuestro.md
423b964 (HEAD -> main) HEAD@{21}: checkout: moving from main to styled
423b964 (HEAD -> main) HEAD@{22}: commit: Adding git-nuestro.md
3f6188a HEAD@{23}: commit: Adding Essential Git Files
255e6a5 (origin/main, origin/HEAD) HEAD@{24}: clone: from https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
```

### 13. ¿Qué comando o comandos usaste en el punto 33?
**Paso 33:** Volver al estado final, cuando pusimos título al poema.

**Comandos:**
```bash
git reset --hard 3389496
```

**Aux Comandos:**
```bash
		$ git reflog show --pretty=oneline
		3389496 (HEAD -> main) HEAD@{0}: reset: moving to 3389496
		423b964 HEAD@{1}: reset: moving to 423b964
		7c676cc HEAD@{2}: checkout: moving from main to main
		7c676cc HEAD@{3}: reset: moving to 7c676cc
		d6a45e2 HEAD@{4}: reset: moving to d6a45e2
		3389496 (HEAD -> main) HEAD@{5}: reset: moving to 3389496
		7c676cc HEAD@{6}: merge title: Merge made by the 'ort' strategy.
		d6a45e2 HEAD@{7}: checkout: moving from main to main
		d6a45e2 HEAD@{8}: checkout: moving from title to main
		3389496 (HEAD -> main) HEAD@{9}: commit: Adding Title git-nuestro.md
		d6a45e2 HEAD@{10}: checkout: moving from main to title
		d6a45e2 HEAD@{11}: merge styled: Fast-forward
		423b964 HEAD@{12}: checkout: moving from styled to main
		d6a45e2 HEAD@{13}: commit (merge): Merge branch 'htmlify' into styled
		a65c959 HEAD@{14}: checkout: moving from htmlify to styled
		842b049 HEAD@{15}: commit: Modified Again git-nuestro.md
		423b964 HEAD@{16}: checkout: moving from main to htmlify
		423b964 HEAD@{17}: checkout: moving from styled to main
		a65c959 HEAD@{18}: checkout: moving from styled to styled
		a65c959 HEAD@{19}: reset: moving to a65c9598db386e3126ab0f5c2c319e5086cca26a
		423b964 HEAD@{20}: reset: moving to 423b964
		a65c959 HEAD@{21}: commit: Modified git-nuestro.md
		423b964 HEAD@{22}: checkout: moving from main to styled
		423b964 HEAD@{23}: commit: Adding git-nuestro.md
		3f6188a HEAD@{24}: commit: Adding Essential Git Files
		255e6a5 (origin/main, origin/HEAD) HEAD@{25}: clone: from https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
```

-------

## Pasos Ejercicio 1

### 1. Crear un repositorio en GitHub y clónalo en tu equipo

```bash
git clone https://github.com/algond123/Alex-BdMlAi14-Git-Point1.git
cd Alex-BdMlAi14-Git-Point1
touch .gitignore
touch .gitattributes
git add .
git commit -m "Adding Essential Git Files"
```

### 2. Crear un archivo `git-nuestro.md` con el contenido:

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

### 3. Añadir `git-nuestro.md` al staging area

```bash
git add git-nuestro.md
```

### 4. Mover lo que hay en el staging area al repositorio

```bash
git commit -m "Adding git-nuestro.md"
```

### 5. Crear una rama llamada `styled`

```bash
git branch styled
```

### 6. Listar las ramas que hay en el repositorio

```bash
git branch
```

### 7. Moverse a la rama `styled`

```bash
git checkout styled
```

### 8. Comprobar que se está en la rama correcta

```bash
git branch
```

### 9. Modificar en el archivo `git-nuestro.md`:

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

### 10. Añadir los cambios al staging area y luego pasarlos al repositorio

```bash
git add git-nuestro.md
git commit -m "Modified git-nuestro.md"
```

### 11. Deshacer el último commit (perdiendo los cambios realizados en el working copy)

```bash
git reflog show --pretty=oneline
git reset --hard 423b964
```

### 12. Rehacer el último commit (el que acabamos de deshacer)

```bash
git reflog show --pretty=oneline
git show HEAD@{1}
git reset --hard a65c9598db386e3126ab0f5c2c319e5086cca26a
```

### 13. Hacer un merge con `main` (styled absorbe a main)

```bash
git checkout styled
git diff main..styled
git merge --ff main
git status
git log --oneline --graph
```

### 14. Volver a la rama `main`

```bash
git checkout main
```

### 15. Crear una nueva rama llamada `htmlify`

```bash
git branch htmlify
```

### 16. Cambiar a la rama `htmlify`

```bash
git checkout htmlify
```

### 17. Modificar en el archivo `git-nuestro.md`:

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

### 18. Hacer un commit

```bash
git add git-nuestro.md
git commit -m "Modified Again git-nuestro.md"
```

### 19. Hacer un merge de `htmlify` en `styled` (styled absorbe a htmlify)

```bash
git checkout styled
git diff htmlify..styled
git log --oneline styled
git log --oneline htmlify
git merge --ff htmlify
```

### 20. Si hay conflictos, deberemos resolverlos quedándonos con el contenido de la rama `styled`.

```bash
git add git-nuestro.md
git commit
```

### 21. Desde `main`, hacer un merge con `styled`

```bash
git checkout main
git merge --ff styled
```

### 22. Crear una rama `title` y cambiarse a esa rama

```bash
git branch title
git checkout title
```

### 23. Añadir un título (a tu gusto) al archivo `git-nuestro.md` y hacer un commit.

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

### 24. Volver a la rama `main`

```bash
git checkout main
```

### 25. Dibujar el diagrama

```bash
git log --all --decorate --oneline --graph
```

### 26. Hacer un merge “no fast-forward” de `title` en `main` (main absorbe a title)

```bash
git checkout main
git merge --no-ff title
```

### 27. Deshacer el merge (sin perder los cambios del working copy)

```bash
git diff d6a45e2 HEAD -- git-nuestro.md
git reset --soft d6a45e2
```

### 28. Descartar los cambios (volver sin title)

```bash
git diff --staged git-nuestro.md
git restore --staged git-nuestro.md
git restore git-nuestro.md
```

### 29. Eliminar la rama `title`

```bash
git branch -D title
```

### 30. Rehacer el merge que hemos deshecho

```bash
git reflog show --pretty=oneline
git diff 7c676cc HEAD -- git-nuestro.md
git reset --hard 7c676cc
```

### 31. Volver a `main` y eliminar el resto de ramas

```bash
git checkout main
git branch -D styled htmlify
```

### 32. Volver al commit inicial cuando se creó el poema

```bash
git reflog show --pretty=oneline
git reset --hard 423b964
```

### 33. Volver al estado final, cuando pusimos título al poema

```bash
git reflog show --pretty=oneline
git reset --hard 3389496
```

### 34. Crear los siguientes tags:

```bash
git log --pretty=oneline
git tag inicial 423b964eaf9aeb59aa4e0e788b7b052d1e538691
git tag styled a65c9598db386e3126ab0f5c2c319e5086cca26a
git tag htmlify 842b0492248b22108eff9b7d462fc14f7fcdfdc8
git tag title 3389496cfb40ea5d2c1e0d8ad9fd408731aa9671
```

### 35. Ir al tag `htmlify`

```bash
git checkout htmlify
```

### 36. Vuelve a la rama `main`

```bash
git checkout main
```

### 37. Subir a GitHub todas las ramas y todos los tags

```bash
git remote set-url origin git@github.com:algond123/Alex-BdMlAi14-Git-Point1.git
git remote -v
git push --all origin
git push --tags origin
```
