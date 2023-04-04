*Apuntes*

- init: crea el repo
- add x: agrega archivos al staging
- commit: agrega los archivos en el staging al repo
- status: meutras estado de archivos (rojo en working directory - verde en staging)
- show: muestra cambios historicos
- log: muestra historial de commits con distintos datos
- git push: enviar commits a github

(staging: en memoria, posteriormente pasa al repo)

_**Clase 12:**_
reset Y: vuelve a un estado Y
    --soft: Borramos todo el historial y los registros de Git pero guardamos los cambios que tengamos en Staging,
            así podemos aplicar las últimas actualizaciones a un nuevo commit.
    
    --hard: Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.
    
    HEAD: Este es el comando para sacar archivos del área de staging. No para borrarlos ni nada de eso,
            solo para que los últimos cambios de estos archivos no se envíen al último commit,
            a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.

    Es muy "peligroso" ya que borra todo lo hecho posteriormente desde el "commit" que se vuelve.
    Este comando nos ayuda a volver en el tiempo. Pero no como git checkout que nos deja ir, mirar, pasear y volver.
    Con git reset volvemos al pasado sin la posibilidad de volver al futuro. Borramos la historia y la debemos sobreescribir. No hay vuelta atrás.

- checkout Y: te mueves entre commits (checkout maseter: vuelve al ultimo commit hecho)

-pull: es igual que "fetch" + "merge". Trae los cambios del repositorio remoto al directorio y repositorio locales.
-push: envía los cambios al repositorio remoto.

- Ramas:
- branch: crea una rama a partir del lugar donde estoy parado (HEAD)
- checkout Z: me muevo a la rama Z

X: archivo
Y: directorio o commit
Z: nombre rama

Podemos usar un atajo para crear y movernos a esa nueva rama con el comando "checkout -b Z"

*merge* Z: el merge se debe realizar sobre la rama en la cual quiero traer los cambios a fusionar.
        por ejemplo, si estoy en master (rama principal), y quiero traer (fusionar) la "nueva_rama", solo hago un merge
        desde la rama donde estoy, y pongo la rama que quiero traer: "git merge nueva_rama" (con HEAD en master)

*Conflictos:*
cuando tengo conflictos durante el merge, debo solucionarlos, elijo la opcion de arriba (rama donde estoy parado) o la de abajo (los cambios de la otra rama),
que serian los q vienen.


- Push:
para subir a un repositorio lo primero a hacer es (aparte de tener el repositorio) introducir el comando

remote add origin "url": asi, vinculamos nuestro local al repositorio creado en github

para verificar q esta correcto usamos "remote -v", ahora solo queda subirlo con:
(antes de hacerlo, en este ejemplo cambio el nombre de "master" a "main" con el comando "branch -m main")
push origin main: esto subira el proyecto junto con todas las ramas creadas de manera local.

EN EL REMOTO CASO, de que ya haya contenido por primera vez, debemos traernos lo que haya con un pull con el comando:

- pull origin main: de esta manera nos traemos los cambios o lo q haya en el repo remoto al local
    origin: es el nombre del repositorio remoto
    main: la rama actual (la rama con la cual voy a fucionar lo q traiga de origin)


// Lo recomendado es traer siempre con un pull antes de hacer un push

*Rebase*
El rebase es basicamente: tengo una rama con errores, creo una rama a partir de esa para solucionar los errores.
el objetivo o lo que se busca es, solucionar esos errores, y una vez solcuionados se quiere agregar todos los
commits hechos en esa nueva rama a la rama de la cual partiste (NUNCA HACERLO EN LA RAMA PRINCIPAL, ES MALA PRACTICA).

para acer un rebase me tengo que colocar en la rama nueva, y ejecutar el comando
git rebase Z
donde Z es la rama a la cual le voy a pegar la historia de la nueva rama con los fixes.
si estoy en la rama "experimento" y ejecuto el rebase de master,
- ME TRAE TODO LO DE MASTER Y LO UBICA AL FINAL DE LA RAMA EXPERIMENTOS

El rebase, coloca los cambios realizados (o lo que tienes en la rama fix), al final de la rama de la cual partiste.
Entonces, podes tener en fix 3 commits, y en la rama de la cual partiste tenes 4 nuevos commits. Cuando realizas el rebase
los 3 commits de fix van a ir al final de la rama origen (de la cual partiste).

## PRIMERO SE LE HACE EL REBASE A LA RAMA QUE VA A DESAPARECER DE LA HISTORIA (FIX) Y DESPUES A LA RAMA PRINCIPAL
## REBASE PRIMERO A DND HUBO LOS CAMBIOS QUE QUEREMOS MODIFICAR Y LUEGO REBASE A LA RAMA FINAL.


_*Stach*_
- El stash sirve para guardar cambios que haya hecho sin hacer commits, cuando tengo cambios y no quiero
- commitear, hago un stash y me va a guardar esos cambios, y el archivo me va a mostrar todo como estaba
- antes de haber hecho esos cambios, como si nunca los hubiera hecho.

_* TIP-ASO *_
- SI YO QUIERO GUARDAR ALGO, EN UN STASH Y PONERLO EN OTRA ROMA, EL COMANDO A USAR ESO:
git stash branch z: donde z es el nombre de la NUEVA rama y con los cambios del stash.

- para borrar un stash:
git stash drop: borra todo lo que hay en el stash, TODO, no un stash

_* cherrypick*_
Con "cherry-pick", lo que haces es traerte a la rama, el commit que vos queres especificamente.
Si tenes una rama con 3 commits, y vos queres en la rama principal el segundo, solo basta con
- git cherry-pick "numero del commit"
tener en cuenta que para saber el numero del commite hay que verlo en la rama en la que lo trabajaste, o sea
estas en la rama x, te fijas con "log" el numero, copias, te mueves a la rama principal, y haces el cherry-pick con ese numero

mmmm