Fundamentos de Git y GitHub y su aplicación en proyectos colaborativos y
reproducibles en R y RStudio
================
Julen AstigarragaVerónica Cruz-Alonso
2022-11-28

# Flujo de trabajo: repaso

Hay cuatro zonas en el flujo de trabajo de Git y GitHub: **directorio de
trabajo, área de preparación, repositorio local** y **repositorio
remoto**. Con `git pull` se descargan todas las actualizaciones del
repositorio remoto al repositorio local y al directorio de trabajo. Con
`git add` se añaden los cambios en el directorio de trabajo al área de
preparación. Para registrar los cambios en el repositorio local hay que
utilizar `git commit` y, después, para subirlos al repositorio remoto
`git push`.

⚡Usar `git commit` es para el proyecto como usar anclajes cuando
estamos escalando una pared de roca. Desarrollar un script sin commits
es como escalar sin asegurarse: puedes avanzar mucho más rápido a corto
plazo, pero a largo plazo las probabilidades de fallo catastrófico son
altas. Por otro lado, hacer muchos commits va a ralentizar tu progreso.
Lo mejor: usar más commits cuando estás en un territorio incierto o
peligroso.

![Lineas de trabajo (cuerdas) aseguradas con varios commits
(anclajes)](images/climbing.png)

### 📝Ejercicio 3.1

1.  Uno por uno y secuencialmente cada integrante del equipo (a)
    descarga la copia centralizada del proyecto compartido, (b) hace un
    cambio en algún archivo y (c) lo sube de nuevo a GitHub.

2.  Comprobad que el historial del proyecto tiene dos o tres nuevos
    commits, según el número de personas en el equipo

# Solución de errores comunes en el flujo de trabajo

Git y GitHub permiten resolver problemas comunes en el trabajo
colaborativo pero también pueden causarnos bastantes quebraderos de
cabeza. Es común que al intentar hacer `git push` no te deje porque, o
bien, alguno de tus colaboradores ya lo ha hecho antes (¡y sin avisar!)
y no tienes todos los cambios remotos integrados en tu repositorio
local, o bien, tú te has olvidado de hacer `git pull` al empezar a
trabajar y has guardado cambios importantes en el directorio de trabajo
sin tener actualizado el proyecto con la copia remota. En este ultimo
caso **haz un commit** con los cambios y antes de desesperar echa un ojo
a este apartado.

Como resultado, en ambos casos, el historial del repositorio remoto (A
-\> B -\> C) y el local (A -\> B -\> D) habrán divergido y no se pueden
juntar. Hay varias soluciones para este problema
(<https://happygitwithr.com/pull-tricky.html>) y aquí hemos recogido una
de ellas en la que el objetivo final es tener A -\> B -\> C+D. La
solución consiste en usar `git pull`. Como sabemos, este comando
descarga los cambios y el historial del repositorio remoto y los
incorpora en el repositorio local. Internamente `git pull` está
compuesto por dos comandos:

-   `git fetch`: “trae” los cambios del repositorio remoto al local,
    pero no cambia los archivos locales (directorio de trabajo).

-   `git merge`: fusiona el nuevo historial y los cambios con lo que
    había en el repositorio local. La idea es la misma que al fusionar
    ramas.

Al hacer `git pull` cuando los historiales no coinciden pueden ocurrir
dos cosas:

1.  No hay conflictos al fusionar ambos commits: ¡solucionado!

2.  Aparecen conflictos en `git merge` porque C y D tienen cambios en
    las mismas partes de los mismos archivos. En este caso, hay que
    resolver los conflictos como vimos en la fusión de ramas, es decir,
    buscar los puntos de conflicto
    (`<<<<<<código del main=======código de la rama a unir>>>>>>)`,
    elegir la versión que corresponda, guardar el archivo y hacer de
    nuevo `git add`, `git commit` y `git push`.

⚡¿Cómo prevenir que Git rechace `git push`?
(<https://happygitwithr.com/push-rejected.html>) 1. Haz `git push` de tu
trabajo con frecuencia. 2. Haz `git pull` del trabajo de otros tan
pronto como te des cuenta que el repositorio remoto se ha actualizado.
3. ¡Comunicate con tus colaboradores! 4. Usa ramas en lugar de trabajar
en *main*.

### 📝Ejercicio 3.2

Vamos a crear un conflicto en nuestro repositorio para después
solucionarlo.

1.  Un miembro del equipo cambia la primera línea del archivo README.txt
    y lo sube a GitHub

2.  **Sin hacer `git pull`**, un segundo miembro del equipo cambia la
    misma línea del mismo archivo y lo intenta después subir a GitHub.
    ¿Qué error obtenemos? ¿Cómo lo solucionamos?

3.  La segunda persona ejecuta `git pull` y entre todos resolveis el
    conflicto. ¿Cómo es el historial del archivo ahora?

# Comandos avanzados de Git

## La he liado ¿cómo deshago los cambios?

Cuando hago un cambio que no quiero ¿cómo lo puedo resolver? Hay
múltiples opciones pero aquí detallamos tres: *restore*, *reset* y
*revert*. Restore se usa cuando no has llegado a hacer un commit con los
cambios que quieres añadir y reset/revert cuando si has hecho un commit
con los cambios.

-   `git restore`: deshace un `git add` y/o los cambios del directorio
    de trabajo.

    -   `git restore <nombre de archivo>`: descarta los cambios en un
        archivo al estado del último commit. ⚠️Esta opción es peligrosa
        ya que borra los cambios no commitidos de tu directorio de
        trabajo.

    -   `git restore --staged <nombre de archivo>`: eliminará el archivo
        del área de preparación pero mantiene los cambios del directorio
        de trabajo.

-   `git reset`: deshace un `git commit` y/o un `git add` y/o los
    cambios del directorio de trabajo.

    -   `git reset --mixed HEAD~1`: deshace el add y el commit pero no
        los cambios realizados en el directorio de trabajo. Es
        equivalente a `git reset` (es decir, la opción por defecto). El
        HEAD\~1 significa el commit anterior al HEAD. Puedes ir un
        commit hacia atrás, dos, etc. También se puede utilizar el SHA
        en lugar del HEAD`~X` para ir a un commit específico.

    -   `git reset --hard HEAD~1`: deshace el add, el commit y todos los
        cambios realizados en el directorio de trabajo. ⚠️ Esta es la
        opción más PELIGROSA. Ten en cuenta que borra los cambios no
        commitidos de tu directorio de trabajo y apunta tu rama al
        commit especificado. Recomendamos ejecutar primero `git status`
        y ver si hay cambios no commitidos.

    -   `git reset --soft HEAD~1`: deshace el último commit pero no el
        add ni los cambios realizados en el directorio de trabajo.

![Diferencias entre `git restore` y distintos tipos de
`git reset`](images/git_restore_reset.png)

-   `git revert HEAD`: es la opción segura de `git reset` para deshacer
    un commit ya que no resetea un proyecto a su estado anterior
    eliminando todos los commits posteriores (es decir, no elimina el
    historial de commits). Recomendamos usar `git reset` sólo en ramas
    que no hayan sido compartidas todavía (es decir, que no hayan sido
    commitidas a un repositorio remoto que otros estén usando). Resetear
    es cambiar el historial sin dejar rastro. Esto es siempre una mala
    práctica y puede causar problemas al resto de colaboradores. Si
    queremos deshacer los cambios en las ramas que se comparten con
    otros, recomendamos utilizar el comando `git revert`. Con
    `git revert` quedará constancia de que se ha deshecho un cambio.

![Diferencias entre `git revert` y `git reset`](images/revert_reset.png)

### 📝Ejercicio 3.3

El objetivo de este ejercicio es que veais las diferencias entre los
distintos tipos de `git reset`. Para ello, tendréis que utilizar
`git status` para ver el estado de git después de cada `git reset`.

Cada integrante del equipo independientemente:

1.  Realiza algunos cambios en el repositorio y realiza un commit de los
    cambios y prueba hacer `git reset --soft HEAD~1`
2.  Realiza otro commit y prueba hacer `git reset --mixed HEAD~1`
3.  Realiza un último commit y prueba hacer `git reset --hard HEAD~1`

## Otros comandos útiles

**Para facilitar el flujo de trabajo**:

-   `git add .`: registra todos los cambios a la vez

-   `git rm --cached filename`: elimina un archivo del área de
    preparación. Muy útil si has añadido un archivo de 10GB que no lo
    quieres compartir cada vez ⚠️

-   `git stash`: cuando no quieres hacer un commit del trabajo a medio
    hacer o no estás seguro si lo quieres conservar pero quieres volver
    a este punto más tarde. Crea un commit fuera de la linea principal
    de trabajo

-   `git stash apply`: recupera cualquier stash que has guardado

**Para obtener información de Git**:

-   `git status`: muestra la rama en la que estamos y los cambios hechos
    y añadidos desde el último commit.

-   `git diff`: muestra los cambios no añadidos con `git add`. También
    se puede usar para ver diferencias entre ramas
    `git diff <branchname1>…<branchname2>`.

-   `git log`: muestra el historial de commit. Con `git log -n X`
    muestra sólo un número X de commits.

-   `git branch -a`: muestra todas las ramas locales y remotas. También
    te indica en qué rama te encuentras

-   `git stash list`: ver los stash que has guardado

-   `gitk`: para visualizar la interfaz gráfica de Git.

**Para mantener el orden en tu repositorio**:

-   `git branch -d <branchname>`: elimina la rama llamada “branchname”
    de tu pc

-   `git push origin --delete <branchname>`: elimina la rama remota
    llamada “branchname” (por ejemplo, desde GitHub). Ten en cuenta que
    la rama local y la remota no tienen nada que ver entre sí, por lo
    que deben eliminarse por separado

-   `git commit --amend -m "message"`: cambiar el mensaje del último
    commit

-   `git clean -f`: borra (⚠️ojo) archivos que no están siendo
    monitorizados por Git. Es útil para eliminar todos los productos
    creados al ejecutar algún script

-   `git push --force`: se utiliza para sobreescribir la historia de la
    rama en la que estás trabajando. En este sentido, por ejemplo, se
    puede utilizar después de `git reset --hard` . ⚠️⚠️Esta opción es
    DOBLEMENTE PELIGROSA. No solo borras los cambios no commitidos si no
    que modificas la historia de un archivo. Si algún colaborador ya he
    descargado el archivo con su historia anterior, tendrá problemas
    cuando quiera integrar sus cambios de nuevo. ¡Utilizar sólo en casos
    extremos! (p. ej. publico sin querer mis claves de acceso a alguna
    base de datos)

**Para integrar versiones anteriores**:

-   `git checkout HEAD~X`: para inspeccionar una versión (X) antigua del
    proyecto. Recomendamos crear una rama primero si se quiere añadir
    commits a partir de este punto temporal.

-   `git cherry-pick SHA`: permite coger cualquier commit de una rama y
    fusionarlo con otra. Es útil si, por ejemplo, has hecho un commit en
    la rama equivocada y lo quieres mover a la correcta. Sin embargo, en
    general, un merge tradicional suele ser la mejor práctica
    (<https://www.atlassian.com/git/tutorials/cherry-pick>).

![`git cherry-pick` por @girlie_mac](images/git_cherry_pick.jpeg)

### 📝Ejercicio 3.4

¿Qué comando o comandos utilizarías si…

1.  …llevas mucho sin trabajar en un proyecto y no te acuerdas de los
    últimos pasos que se habían dado?
2.  …haces un montón de pruebas para un análisis y no las quieres borrar
    pero tampoco dejar todas en la línea principal del proyecto?
3.  …has creado 10 plots con tus datos (archivos nuevos) pero no los
    quieres compartir porque se pueden crear con el script que vas a
    subir a GitHub?
4.  …un colaborador ha realizado un commit y un push mientras tú estabas
    trabajando en la misma rama?

<details>
<summary>
Session Info
</summary>

``` r
Sys.time()
```

    [1] "2022-11-28 16:03:22 CET"

``` r
git2r::repository()
```

    Local:    main C:/Users/veruk/Desktop/Disco/Curso GitHub/intro_git-github
    Remote:   main @ origin (https://github.com/Julenasti/intro_git-github.git)
    Head:     [7eca817] 2022-11-28: revision con Julen dia 3

``` r
sessionInfo()
```

    R version 4.1.3 (2022-03-10)
    Platform: x86_64-w64-mingw32/x64 (64-bit)
    Running under: Windows 10 x64 (build 22000)

    Matrix products: default

    locale:
    [1] LC_COLLATE=English_United States.1252 
    [2] LC_CTYPE=English_United States.1252   
    [3] LC_MONETARY=English_United States.1252
    [4] LC_NUMERIC=C                          
    [5] LC_TIME=English_United States.1252    

    attached base packages:
    [1] stats     graphics  grDevices utils     datasets  methods   base     

    loaded via a namespace (and not attached):
     [1] digest_0.6.29   jsonlite_1.8.0  git2r_0.30.1    magrittr_2.0.3 
     [5] evaluate_0.15   rlang_1.0.4     stringi_1.7.6   cli_3.3.0      
     [9] rstudioapi_0.13 rmarkdown_2.13  tools_4.1.3     stringr_1.4.1  
    [13] xfun_0.30       yaml_2.3.5      fastmap_1.1.0   compiler_4.1.3 
    [17] htmltools_0.5.2 knitr_1.38     

</details>
