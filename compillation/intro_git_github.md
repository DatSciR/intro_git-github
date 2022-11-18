Fundamentos de Git y GitHub y su aplicación en proyectos colaborativos y
reproducibles en R y RStudio
================
Julen AstigarragaVerónica Cruz-Alonso
2022-09-17

# Introducción

El principal objetivo de este documento es dar a conocer la estructura,
funcionalidad y potencialidad de Git (https://git-scm.com/), así como su
interacción con GitHub (<https://github.com/>), para el trabajo en
proyectos colaborativos. Ambas herramientas están ganando cada vez más
importancia en ecología a medida que el volumen de datos aumenta y los
análisis se hacen más complejos. Aprenderemos cómo Git puede usarse para
controlar la trazabilidad de los cambios realizados en proyectos o
archivos y veremos cómo este control de versiones es especialmente útil
en proyectos colaborativos mediante el uso de un servidor de alojamiento
en línea como GitHub. Aunque existen multitud de manuales disponibles
gratuitamente sobre cómo utilizar Git y GitHub, estas herramientas son
complejas y tienen una curva de aprendizaje pronunciada. Por ello, aquí
hemos intentado agrupar nuestra experiencia adquirida después de varios
años trabajando con estas herramientas para facilitar vuestra curva de
aprendizaje ¡Vamos a por ello!

Por ejemplo, Git y GitHub nos pueden ayudar a solucionar algunos
problemas comunes derivados de la creación de diferentes versiones que
pueden ser un poco molestos:

\- Sobreescritura de un archivo

\- Versiones finales infinitas

![“FINAL.doc”](images/FINALdoc.png)  

\- Trabajo por error en una versión que no era la final

\- Creación de copias “en conflicto” cuando dos personas trabajan a la
vez

\- Ediciones sin control de cambios

![Ediciones sin control de cambios](images/tracker.png)  

## Quiénes somos

![Quienes somos](images/quien.png)  

## [Qué es Git](https://git-scm.com/)

Git es un sistema avanzado de control de versiones (como el “control de
cambios” de Microsoft Word) distribuido (Blischak, Davenport, and Wilson
2016; Ram 2013). Git permite “rastrear” el progreso de un proyecto a lo
largo del tiempo ya que hace “capturas” del mismo a medida que
evoluciona y los cambios se van registrando. Esto permite ver qué
cambios se hicieron, quién los hizo y por qué, e incluso volver a
versiones anteriores. Además, Git facilita el trabajo en paralelo de
varios participantes. Mientras que en otros sistemas de control de
versiones (p. ej. Subversion (SVN, <https://subversion.apache.org/>) o
Concurrent Versions System (CVS, <http://cvs.nongnu.org/>)) hay un
servidor central y cualquier cambio hecho por un usuario se sincroniza
con este servidor y de ahí con el resto de usuarios, Git es un control
de versiones distribuido que permite a todos los usuarios trabajar en el
proyecto paralelamente e ir haciendo “capturas” del trabajo de cada uno
para luego unirlos. Otras alternativas de control de versiones
distribuido comparables a Git son Mercurial
(<https://www.mercurial-scm.org/>) o Bazaar
(<https://bazaar.canonical.com/>), pero Git es con diferencia el más
utilizado.

![Ejemplo de un proyecto rastreado por Git con indicaciones de cómo se
registran los cambios y la evolución del proyecto, el autor o autora de
los cambios (¿quién?), el momento en que se han registrado (¿cuándo?),
en qué documentos o líneas se han producido cambios (¿dónde?) y qué ha
cambiado (¿qué?)](images/git.jpg)

Para hacerse una idea de la curva de aprendizaje de Git, es importante
destacar que el propósito original de Git era ayudar a grupos de
desarrolladores informáticos a trabajar en colaboración en grandes
proyectos de software pero en este documento veremos que también se
puede utilizar para otros propósitos. En este sentido, veremos que hay
múltiples soluciones para un mismo problema.

## [Qué es GitHub](https://github.com/)

GitHub es un servidor de alojamiento en línea o repositorio remoto para
albergar proyectos basados en Git que permite la colaboración entre
diferentes usuarios o con uno mismo (Galeano 2018; Perez-Riverol et al.
2016). Un repositorio es un directorio donde desarrollar un proyecto que
contiene todos los archivos necesarios para el mismo. Aunque existen
distintos repositorios remotos (p. ej. GitLab, <https://gitlab.com/>, o
Bitbucket, <https://bitbucket.org/>) con funcionalidad similar, GitHub
es hoy en día el más utilizado. GitHub registra el desarrollo de los
proyectos de manera remota, permite compartir proyectos entre distintos
usuarios y proporciona la seguridad de la nube entre otras funciones.
Cuando se trabaja en proyectos colaborativos, la base de la interacción
entre Git y GitHub es que todos los colaboradores de un proyecto están
de acuerdo en que GitHub contiene la copia principal del proyecto, es
decir, GitHub contiene la copia centralizada del control de versiones
distribuido o descentralizado.

![Página inicial de GitHub](images/github_pag_ini.JPG)

![Perfil de GitHub](images/github_perfil.JPG)

![Interacción entre Git y GitHub. Git, al ser un control de versiones
distribuido, permite que todos los usuarios trabajen paralelamente sin
interferir en el trabajo de los demás. Luego cada usuario sincroniza su
trabajo con la copia principal del proyecto ubicado en
GitHub](images/conexiones.jpg)

# Instalación

En este punto es necesario que tengas instalada la versión más reciente
de R (<https://cloud.r-project.org/>), RStudio
(<https://www.rstudio.com/products/rstudio/download/>), Git
(<https://happygitwithr.com/install-git.html>) y una cuenta en GitHub
(<https://github.com/>) creada.

### Ejercicio 1

En el *shell*, preséntate a Git ([Chapter 7:
Git-Intro](https://happygitwithr.com/hello-git.html))

⚡ ¿Qué es el *shell*? El *shell* (o terminal) es un programa en tu
ordenador cuyo trabajo es ejecutar otros programas (ver
<https://happygitwithr.com/shell.html#shell>). En este documento
aprenderemos a trabajar principalmente desde la línea de comandos del
*shell* aunque también veremos cómo hacerlo a través de un cliente como
RStudio (<https://www.rstudio.com/>), que incorpora una pestaña llamada
“Git” que facilita la transición entre zonas de trabajo ya que contiene
funcionalidades básicas de Git. Usar un cliente como RStudio es
recomendable para usuarios noveles de Git (ver
<https://happygitwithr.com/rstudio-git-github.html>).

![Terminal](images/terminal.png)  

![Terminal de Git](images/terminal-2.png)

![A través de RStudio](images/RStudio.JPG)

*Tools* -\> *Shell*

`git config --global user.name 'Nombre Apellido'`

`git config --global user.email 'nombre@ejemplo.com'`

Compueba que has instalado Git correctamente:

`git --version`

Para ver el usuario utilizado para configurar Git:

`git config user.name`

Para ver a qué cuenta de correo está asociado Git:

`git config user.email`

Para ver tanto el usuario como el correo asociado:

`git config --global --list`

# Repositorios y proyectos

Un repositorio es como un “contenedor” donde desarrollar un proyecto.

Para crear un repositorio en GitHub damos a “*+ New repository*”. Aquí
se indica el nombre, una pequeña descripción, y si quieres que sea
público o privado. Se recomienda iniciar el repositorio con un archivo
“README” (*Initialize this repository with a README*) para recoger
cualquier información esencial para el uso del repositorio (estructura,
descripción más detallada del contenido, etc.).

![Repositorio en GitHub destacando algunas pestañas
importantes](images/github_repositorio.JPG)

En R, creamos un nuevo proyecto y lo conectamos al repositorio: File -\>
New project -\> Version control -\> Git -\> copiar el URL del
repositorio que hemos creado de GitHub (está en la página principal de
nuestro repositorio, en “*clone or download*”). Seleccionamos el
directorio donde queremos guardar el proyecto y pulsamos en “*Create
project*”.

Si vamos al directorio seleccionado, encontraremos la carpeta conectada
a Git y GitHub que hemos creado en nuestro ordenador. Podemos copiar
aquí todos los archivos que nos interesan para el proyecto (datos,
imágenes, etc).

Para más información sobre cómo clonar el repositorio en GitHub
(repositorio remoto) en nuestro ordenador (repositorio local) ver
<https://happygitwithr.com/rstudio-git-github.html> para hacerlo desde
RStudio; y ver Galeano (2018) para hacerlo mediante la línea de
comandos.

### Ejercicio 2

Trabajamos en equipos de 2-3 personas

1.  **Un integrante** del equipo crea un repositorio en GitHub y lo
    conecta a un nuevo proyecto de RStudio (esto generará un repositorio
    (carpeta) en tu ordenador en la ubicación que le hayas especificado)

2.  Crea un nuevo script de R en el directorio de trabajo (es decir,
    crea un script de R y guárdalo dentro del repositorio que has
    creado)

3.  En RStudio ve a la pestaña Git (donde está el *environment*) para
    ver todos los documentos que han sido identificados por Git

![Lo que esperamos que hayáis aprendido](images/git-2.png)  

# Flujo de trabajo en Git y GitHub

Git es capaz de rastrear todos los archivos contenidos en un
repositorio. Para comprender cómo Git registra los cambios y cómo
podemos compartir dichos cambios con nuestros colaboradores es
importante entender cómo se estructura Git y cómo se sincroniza con
GitHub. Hay cuatro “zonas” de trabajo:

1.  **Directorio de trabajo (*working directory*):** es donde se está
    trabajando. Esta zona se sincroniza con los archivos locales del
    ordenador.

2.  **Área de preparación (*staging area* o *Index*):** es la zona
    intermedia entre el directorio de trabajo y el repositorio local de
    Git. Es la zona de borradores. El usuario debe seleccionar los
    archivos que se van a registrar en la siguiente “captura” de Git.

3.  **Repositorio local (*local repository* o *HEAD*):** es donde se
    registran todos los cambios capturados por Git en tu ordenador.

4.  **Repositorio remoto (*remote repository*):** es donde se registran
    todos los cambios capturados por Git en la nube (GitHub).

![Graphical representation of the different working areas in Git and
GitHub: working directory, staging area or Index, local repository or
HEAD, and remote repository. Background image from Philip Brookes
(<https://creativecommons.org/licenses/by-nc-nd/2.0/legalcode>)](images/arboles.jpg)

## ¿Cómo moverse de una zona a otra?

Al principio todos los cambios realizados están en amarillo porque Git
no sabe que hacer con ellos. Estamos en el directorio de trabajo y puede
que no nos interese guardar todos los cambios para el futuro.

Para añadir un cambio del directorio de trabajo al área de preparación
hay que utilizar `git add`. Este comando indica a Git que se quieren
incluir las actualizaciones de algún archivo en la próxima “captura” del
proyecto y que Git las registre. Sin embargo, `git add` no afecta al
repositorio local.

-   `git add <nombre de archivo>`: añade una actualización de algún
    archivo del directorio de trabajo al área de preparación.

Para ver el estado del directorio de trabajo y del área de preparación
se utiliza `git status`. Este comando permite ver qué archivos están
siendo rastreados por Git, qué cambios han sido añadidos al área de
preparación (*staged*) y qué archivos están siendo registrados por Git.

Para registrar los cambios que nos interesen hay que utilizar
`git commit`. Al ejecutar `git commit` se hace una “captura” del estado
del proyecto. Junto con el *commit* se añade un mensaje con una pequeña
explicación de los cambios realizados y por qué (p. ej. “incluyo las
referencias en el formato de Ecosistemas”). Cada `git commit` tiene un
SHA (Secure Hash Algorithm) que es un código alfanumérico que identifica
inequívocamente ese *commit* (p. ej.
1d21fc3c33cxxc4aeb7823400b9c7c6bc2802be1). Parece difícil de entender,
pero no te preocupes, sólo tienes que recordar los siete primeros
dígitos 1d21fc3 😱 (es broma). Con el SHA siempre se pueden ver los
cambios que se hicieron en ese *commit* y volver a esa versión
fácilmente.

-   `git commit -m "mensaje corto y descriptivo"`

Por último, `git push` permite subir los cambios que hemos hecho a
GitHub y quedarán visibles para nuestros colaboradores. Básicamente,
`git commit` registra los cambios en el repositorio local y `git push`
actualiza el repositorio remoto con los cambios y archivos asociados.

Cuando se retoma un proyecto tras horas, días o incluso meses, con
`git pull` se descargan todas las actualizaciones que haya en GitHub
(nuestras o de nuestros colaboradores), que se fusionarán (*merge*) con
el último *commit* en nuestro repositorio local.

![Flujo de trabajo en Git y GitHub mostrando las diferentes zonas de
trabajo y los comandos utilizados para la transición de una zona de
trabajo a otra.](images/workflow_git_github.jpg)

### Ejercicio 3

1.  En el proyecto de cada equipo, guardad y subid a GitHub los cambios
    realizados en el Ejercicio 2 (`git add` + `git commit` + `git push`)

## Integración de colaboradores

Para dar acceso de edición a tus colaboradores, en la página principal
de nuestro proyecto en GitHub entramos en “*Settings -\> Manage Access
-\> Invite a collaborator*”. Los colaboradores crean un nuevo proyecto
de control de versiones clonando el repositorio remoto (esto se puede
hacer copiando el https del proyecto).

![Repositorio en GitHub destacando información
importante](images/github_repositorio2.JPG)

### Ejercicio 4

1.  El dueño del repositorio invita al resto de integrantes del equipo a
    su proyecto
2.  Los invitados clonan el repositorio al que han sido invitados (es
    decir, repite el paso 1 del ejercicio 2)
3.  Un integrante del equipo modifica el archivo README.txt, registra
    sus cambios y actualiza el repositorio remoto al que ha sido
    invitado (es decir, repite los pasos del ejercicio 3)
4.  Revisad vuestra cuenta de GitHub y comprobad los cambios que se han
    hecho, quién los ha hecho y las lineas que se han cambiado
5.  Todos los integrantes del equipo hacen `git pull`

# La he liado ¿cómo deshago los cambios?

Cuando hago un cambio que no quiero ¿cómo lo puedo resolver? Hay
múltiples opciones pero aquí detallamos tres: *restore*, *reset* y
*revert*. Restore se usa cuando no has llegado a hacer un commit con los
cambios que quieres añadir y reset/revert cuando si has hecho un commit
con los cambios.

-   `git restore`: deshace un `git add` y/o los cambios del directorio
    de trabajo.

    -   `git restore <nombre de archivo>`: descarta los cambios en un
        archivo al estado del último commit. ⚡ Esta opción es peligrosa
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
        cambios realizados en el directorio de trabajo. ☠️ Esta es la
        opción más PELIGROSA. Ten en cuenta que borra los cambios no
        commitidos de tu directorio de trabajo y apunta tu rama al
        commit especificado. Recomendamos ejecutar primero `git status`
        y ver si hay cambios no commitidos. Si los hay y no estás seguro
        de si los quieres conservar, guárdalos con `git stash` (más
        adelante explicaremos su utilidad).

    -   `git reset --soft HEAD~1`: deshace el último commit pero no el
        add y los cambios realizados en el directorio de trabajo.

![Diferencias entre git restore y distintos tipos de git
reset](images/git_restore_reset.png)

-   `git revert HEAD`: es la opción segura de `git reset` para deshacer
    un commit ya que no resetea un proyecto a su estado anterior
    eliminando todos los commits posteriores (es decir, no elimina el
    historial de commits). Recomendamos usar `git reset` en ramas que no
    hayan sido compartidas todavía (es decir, que no hayan sido
    commitidas a un repositorio remoto que otros estén usando). Resetear
    es cambiar el historial sin dejar rastro. Esto es siempre una mala
    práctica y puede causar problemas. Si queremos deshacer los cambios
    en las ramas que se comparten con otros, recomendamos utilizar el
    comando `git revert`. Con `git revert` quedará constancia de que se
    ha deshecho un cambio.

![Diferencias entre git revert y git reset](images/revert_reset.png)

### Ejercicio 5

El objetivo de este ejercicio es que veais las diferencias entre los
distintos tipos de `git reset`. Para ello, tendréis que utilizar un
comando para ver el estado de git después de cada `git reset`. ¿Os
acordáis cuál era?

Cada integrante del equipo independientemente:

1.  Realiza algunos cambios en el script que creaste en el ejercicio 2 o
    en el README.txt
2.  Realiza un commit de los cambios y prueba hacer
    `git reset --soft HEAD~1`
3.  Realiza otro commit y prueba hacer `git reset --mixed HEAD~1`
4.  Realiza un último commit y prueba hacer `git reset --hard HEAD~1` ☠️

# ¿Cómo se puede trabajar paralelamente?

Git permite crear una “rama” (*branch*) paralela al proyecto si se desea
seguir una línea independiente de trabajo, bien por ser diferente de la
principal (p. ej. probar un nuevo análisis) o bien para desarrollar
específicamente una parte del proyecto (p. ej. trabajar sólo en la
escritura de los métodos de un artículo mientras otros colaboradores
trabajan en otras secciones). Las ramas permiten trabajar en el proyecto
sin interferir con lo que están haciendo los compañeros. En Git, una
rama es un *commit* al que le se le da un nombre y que contiene un
“enlace” (puntero o *pointer*) a un SHA específico que es el origen de
la rama. La rama *main* es la rama por defecto cuando se crea un
repositorio. Las demás ramas se crean con `git checkout`.

-   `git checkout -b <branchname>`: crea una nueva rama y te cambia a
    ella.

-   `git checkout main`: para volver a la rama principal.

![Proceso de creación de la rama *PPP* y la rama
*monchi*](images/ramas.png)

## ¿Cómo se unen distintas ramas?

Cuando el trabajo desarrollado en una rama se da por finalizado y se
quiere unir a la rama principal (“*main*”) hay que hacer la unión
utilizando el comando `git merge`.

-   `git checkout <rama principal>`: posiciona el puntero de Git en el
    último commit de la rama principal a la que quiero unir la otra
    rama.

-   `git merge <rama a unir>`: fusiona los cambios hechos en las dos
    ramas.

Esto se puede hacer en el *shell* como acabamos de ver pero también se
puede hacer con el botón “*pull request*” en la página del proyecto en
GitHub (ver Galeano (2018)).

![Proceso de creación y unión de ramas. Ejemplo de unión (*merge*) de la
rama *monchi* a la rama *main*](images/merge.jpg)

Git puede encontrar conflictos al fusionar ramas que hay que arreglar
manualmente. Esto ocurrirá si en las dos ramas se han cambiado las
mismas líneas de un archivo. Git muestra dónde están los conflictos así
(imaginemos que estamos uniendo la rama analisis al main):

`<<<<<<código del main=======código de la rama a unir>>>>>>`

Para solucionarlo hay que escoger los cambios de la rama principal o de
la rama a unir según corresponda. Esto también se puede hacer a través
de un cliente de Git, como GitKraken (<https://www.gitkraken.com/>) o
SourceTree (<https://www.sourcetreeapp.com/>). Una vez solucionados, Git
permite completar el *merge* (es decir, un nuevo *commit* que contendrá
las ramas fusionadas). La mejor manera de evitar conflictos o por lo
menos reducir su dificultad es realizar cambios pequeños y sincronizar
frecuentemente con GitHub.

### Ejercicio 6

1.  Un integrante del equipo crea una rama en el proyecto en el que
    colabora
2.  Modifica la primera frase del archivo README.txt y sube los cambios
    al repositorio remoto (ejercicio 3). Nota: la primera vez que haces
    `git push` de una rama nueva en lugar de solamente utilizar
    `git push` utiliza
    `git push --set-upstream origin <nombre de la rama>`
3.  Otro integrante modifica también la primera frase del archivo
    README.txt en la rama principal y sube los cambios al repositorio
    remoto
4.  Un integrante combina la nueva rama que habéis creado con la rama
    principal del proyecto (Mirad el apartado ¿Cómo se unen distintas
    ramas?)
5.  Resuelve el conflicto (es decir, quédate con los cambios que sirvan
    y sube los cambios al repositorio remoto)

![](images/github_code.png)

# Otros comandos útiles

-   `git diff`: muestra los cambios no añadidos con `git add`

-   `git log`: muestra el historial de los commit

-   `git add .`: registra todos los cambios a la vez

-   `git rm --cached filename`: elimina un archivo del Index (dejaría de
    estar en el área de preparación). Muy útil si has añadido un archivo
    de 10GB 😉

-   `git branch -d <branchname>`: elimina la rama llamada branchname de
    tu pc

-   `git push origin --delete <branchname>`: elimina la rama remota
    llamada branchname (por ejemplo, desde GitHub). Ten en cuenta que la
    rama local y la remota no tienen nada que ver entre sí, por lo que
    deben eliminarse por separado

-   `git branch -a`: muestra todas las ramas locales y remotas. También
    te indica en qué rama te encuentras

-   `git stash`: cuando no quieres hacer un commit del trabajo a medio
    hacer pero quieres volver a este punto más tarde

-   `git stash list`: ver los stash que has guardado

-   `git stash apply`: recupera cualquier stash que has guardado en la
    stash list

-   `git commit --amend -m "message"`: cambiar el mensaje del último
    commit

-   `git checkout HEAD~X`: para inspeccionar una versión antigua del
    proyecto. Recomendamos crear una rama primero si se quiere añadir
    commits a partir de este punto temporal.

-   `gitk`: para visualizar la interfaz gráfica

-   `git push --force`: se utiliza para sobreescribir la historia de la
    rama en la que estás trabajando. En este sentido, por ejemplo, se
    puede utilizar después de `git reset --hard` . ☠️ 💀 Esta opción es
    DOBLEMENTE PELIGROSA. No solo borras los cambios no commitidos si no
    que modificas la historia de un archivo. Si algún colaborador ya he
    descargado el archivo con su historia anterior, tendrá problemas
    cuando quiera integrar sus cambios de nuevo. ¡Utilizar sólo en casos
    extremos! (p. ej. publico sin querer mis claves de acceso a alguna
    base de datos).

# Otras utilidades de GitHub

Al crear un repositorio se recomienda crear un archivo “*.gitignore*”.
Este archivo contendrá los nombres o extensiones de los archivos del
proyecto que por defecto no queremos compartir aunque estén en el
repositorio local. P. ej., el archivo “*.Rhistory*” que RStudio crea por
defecto. Es una buena práctica ignorar archivos que no sean útiles pare
el resto de colaboradores así como archivos muy pesados (p. ej., una
base de datos resultado de correr un script) para no subirlos y
descargarlos continuamente de GitHub. Para añadir archivos al
*gitignore* se puede utilizar el botón derecho del ratón sobre el
archivo en la pestaña Git de RStudio.

En la página principal de tu proyecto en GitHub encontrarás herramientas
útiles para colaborar.

-   “*Issues*”: en el ámbito de desarrolladores de software, los issues
    cumplen la función de rastreadores de errores. A nosotros nos
    interesa más utilizar los issues como una lista de tareas pendientes
    que permite incluir tareas para acordarte de lo que tienes que hacer
    o asignar tareas a los miembros del proyecto (escribiendo “@” antes
    del nombre del colaborador). Cuando completas una tarea, puedes
    conectar el issue con el commit correspondiente si en el mensaje del
    commit añades `git commit -m "Close #XX"` (p. ej., “Close \#1” para
    cerrar el “issue” número 1).

-   “*Fork*”: GitHub contiene multitud de proyectos públicos que todos
    los usuarios pueden clonar y desarrollar independientemente. Al
    hacer una clonación, se crea una ramificación o copia del proyecto
    (“*fork*”) que pasa a formar parte de tu cuenta de usuario en
    GitHub. En caso de que desees unir los cambios realizados al
    proyecto original, deberás solicitarlo (=“*pull request*”). El dueño
    del proyecto decide si acepta o no los cambios que propones.

# Algunos enlaces interasantes

**Ciencia reproducible**

-   [Ciencia reproducible: qué, por qué,
    cómo](https://github.com/ecoinfAEET/Reproducibilidad)

**Control de versiones (Git)**

-   [Manual de referencia de Git](https://git-scm.com/docs)

-   [Software Carpentry](http://swcarpentry.github.io/git-novice/)

-   [Atlassian Bitbucket](https://www.atlassian.com/git/tutorials)

-   [Oh Shit, Git!?!](https://ohshitgit.com/)

-   [git - la guía
    sencilla](https://rogerdudler.github.io/git-guide/index.es.html)

-   [Pro Git](https://git-scm.com/book/es/v2)

**Integrar Git, GitHub y RStudio**

-   [Happy Git and GitHub for the useR](https://happygitwithr.com/)

**Enseñar y aprender con GitHub**

-   [GitHub Education para profesores e
    investigadores](https://docs.github.com/en/education/explore-the-benefits-of-teaching-and-learning-with-github-education/use-github-in-your-classroom-and-research/about-github-education-for-educators-and-researchers)

# Referencias

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-blischak2016" class="csl-entry">

Blischak, John D., Emily R. Davenport, and Greg Wilson. 2016. “A Quick
Introduction to Version Control with Git and GitHub.” *PLOS
Computational Biology* 12 (1): e1004668.
<https://doi.org/10.1371/journal.pcbi.1004668>.

</div>

<div id="ref-galeano2018" class="csl-entry">

Galeano, Javier. 2018. “¿Por qué usar GitHub? Diez pasos para disfrutar
de GitHub y no morir en el intento.” *Ecosistemas* 27 (2): 140–41.
<https://doi.org/10.7818/ECOS.1604>.

</div>

<div id="ref-perez-riverol2016" class="csl-entry">

Perez-Riverol, Yasset, Laurent Gatto, Rui Wang, Timo Sachsenberg, Julian
Uszkoreit, Felipe da Veiga Leprevost, Christian Fufezan, et al. 2016.
“Ten Simple Rules for Taking Advantage of Git and GitHub.” *PLOS
Computational Biology* 12 (7): e1004947.
<https://doi.org/10.1371/journal.pcbi.1004947>.

</div>

<div id="ref-ram2013" class="csl-entry">

Ram, Karthik. 2013. “Git Can Facilitate Greater Reproducibility and
Increased Transparency in Science.” *Source Code for Biology and
Medicine* 8 (1): 7. <https://doi.org/10.1186/1751-0473-8-7>.

</div>

</div>

------------------------------------------------------------------------

![Fire emergency](images/in_case_of_fire.png)  

------------------------------------------------------------------------

<details>
<summary>
Session Info
</summary>

``` r
Sys.time()
```

    [1] "2022-09-17 12:37:51 CEST"

``` r
git2r::repository()
```

    Local:    main C:/Users/julen/OneDrive/Escritorio/GitHub-col/intro_git-github
    Remote:   main @ origin (https://github.com/Julenasti/intro_git-github.git)
    Head:     [a0f73bf] 2022-06-09: add ecosistemas article link

``` r
sessionInfo()
```

    R version 4.2.1 (2022-06-23 ucrt)
    Platform: x86_64-w64-mingw32/x64 (64-bit)
    Running under: Windows 10 x64 (build 19044)

    Matrix products: default

    locale:
    [1] LC_COLLATE=English_United Kingdom.utf8 
    [2] LC_CTYPE=English_United Kingdom.utf8   
    [3] LC_MONETARY=English_United Kingdom.utf8
    [4] LC_NUMERIC=C                           
    [5] LC_TIME=English_United Kingdom.utf8    

    attached base packages:
    [1] stats     graphics  grDevices utils     datasets  methods   base     

    loaded via a namespace (and not attached):
     [1] lubridate_1.8.0  emo_0.0.0.9000   crayon_1.5.1     assertthat_0.2.1
     [5] digest_0.6.29    jsonlite_1.8.0   git2r_0.30.1     magrittr_2.0.3  
     [9] evaluate_0.16    rlang_1.0.4      stringi_1.7.8    cli_3.3.0       
    [13] rstudioapi_0.13  generics_0.1.3   rmarkdown_2.16   tools_4.2.1     
    [17] stringr_1.4.1    glue_1.6.2       purrr_0.3.4      xfun_0.32       
    [21] yaml_2.3.5       fastmap_1.1.0    compiler_4.2.1   htmltools_0.5.3 
    [25] knitr_1.40.1    

</details>
