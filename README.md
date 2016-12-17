# GitHub 

Cosas que debes tener en cuenta desde ya **HEAD** es tu presente.

### Creación de repositorio gratis en la web **[github.com](https:/github.com "click ")** 

Ingresando al Link podrás crearte una cuenta de manera gratuita, para usarla debes confirmar tu correo como en cualquier típica página.
Al momento de crear un repositorio nuevo tenemos que tener presentes dos cosas que son de gran importancia y que debemos utilizar en nuestra consola al momento de querer trabajar de manera remota con git.

Lo Primero es crear un repositorio y **NO** marcar la opción de `agregar el README.md` (este lo creamos nosotros para hacer la presentación del contenido).

Lo segundo es ejecutar (continuación de la configuración de git por consola) las siguiente lineas de comandos:

```
	git remote add origin https://github.com/xxxxxxx/-xxxxxxx.git
	git push -u origin master
```
**Estas dos lineas de comando las ejecutaremos luego de haber realizado la configuración de git que viene a continuación**

### Configurando GIT por primera vez

Si como yo estás en window te recomiendo instalar git bash que es una consola que reconoce comandos de linux y te permite trabajar de manera cómoda git. **[descargar](https://git-scm.com/download/win "click ")**

El primer paso será configurar git en la consola `git bash` utilizando los siguientes comandos:

```
git init
git config --global user.name "nombre completo"
git config --global user-email "correo-sin-comillas-dobles"
git config --global core.editor subl
git config --list
```
### De la zona de trabajo al area de preparación

En Git tenemos un ciclo de trabajo (no detallaré mucho en esto). Lo primero es que Git debe estar al tanto de qué archivo estamos trabajando, tienen que agregarlo al area de preparación con: `git add nombre-del-archivo` (más adelante ahondaremos en las diferentes maneras de trabajar esta linea de comandos)

Una vez en el area de preparación podrán realizar el *commit* con su mensaje ` -m ` respectivo del hito que marcará un presedente en su historial de git.
Por ejemplo: `git commit -m "esta commit lleva mi index.html, mi style.css y mi javascript.js`.

Tienen que comprender que cada commit que se realice debe llevar una referencia de ¿qué contenido es el que se esta trabajando?.

A continuación les dejo una secuencia de líneas de código para que ejecuten ustedes mismos:

```
git status
git add "nombre-archivo"
git status
git commit -m "nombre del commit"
```
### Ver diferencias entre los archivos en el area de preparación con el area de trabajo
Utilizamos el siguiente comando

```
	git diff
```
Si queremos tener más detalle utilizamos el comando:

```
	git diff --cached
```
Tambien podemos ver las diferencias entre dos **commit** especificos utilizando:

```
	git diff id-commit-1 id-commit-2
```
Este comando nos mostrará en color rojo lo eliminado y en color verde lo agregado.
Es importante tener conocimiento de los ID o HASH para ir comparando las diferencias entre commits.

Para ver los id o hash utilicen el comando `git log --decorate --oneline`.

En el apartado de Logs explicare mejor esta linea de comando.


### Creando el .gitignore
En este paso únicamente tienes que crear un archivo .gitignore dentro de tu carpeta de poryecto, esto lo puedes crear directamente en tu editor favorito, en mi caso sublime text 3.

Un ejemplo de archivos a ignorar:

```
	mi-archivo-javascript.js
	mi-style.css
	/node_modules
	index.html
```
Si utilizamos `git status` veremos que los archivos ignorados no aparecen.  :grin:
### Atajos

Si queremos agregar todos los archivos independiente de cual sea a la zona de **preparacion** utilizamos el siguiente comando:

```	
	git add .
```
Si queremos agregar los archivos que tenemos en seguimiento al area de **preparación** utilizamos el siguiente comando:

```
	git add -A
``` 
Se agregaran solo los archivos que tengamos en seguimiento.

**Cuando utilizamos el comando `git add nombre-archivo` es cuando damos seguimiento de un archivo con git.**

Otro atajo rápido sería usar:

```
	`git commit -am "commit saltando la zona de preparacion"
	 git log --decorate --oneline
```
Este comando lo utilizaremos cuando hayamos modificado un commit.

### Log personalizados


```
	git log --pretty=format:"%h - %an, %ar  : %s"

	git log --after="2016-11-25 00:00:00"

	git log --before="2016-08-08 00:00:00" 

	git log -n
``` 
donde la **n** determinará la cantidad de commits que quieres ver.

Los before y after los podemos utilizar anidados para dar un rango especifico de tiempo.


### Deshacer cambios

En este apartado dejaré algunos comandos que sirven para deshacer los cambios realizados en los commit.

Si por X motivo realizamos un commit y no agregamos todo lo que debíamos o queremos agregarle alguna modificación que pertenecerá al mismo commit podemos utilizar el siguiente comando para reemplazar el último commit por el que sí querías realizar :wink: 

```
	git commit --amend
```

Esto abrira el editor que tengas para modificar el commit con los archivos que fueron cambiados y los que estan en el area de preparación.

Para sacar un archivo de la zona de **preparación** utilizamos el comando:

```
	git reset HEAD nombre-del-archivo
```
### Etiquetas !important buenas practicas y versionado de tu proyecto.
Podemos listar las etiquetas que ya existen con:

`	git tag`

Crearemos nuestra primera etiqueta, esta etiqueta se le agregará al **commit** mas reciente:
	
```
	git tag etiqueta-nueva
	git log --decorate

```
La etiqueta anotada **-a** guardará en la base de datos de git todo como un objeto (más completo que la etiqueta normal), que contiene el nombre del etiquetador, correo, fecha y tienen un **mensaje con -m**.

```
	git tag -a v1.0 -m "version 1.0 estable"
	git tag
	git log --decorate
	git show v1.0
	git show etiqueta-nueva
```
Si quisieramos versionar algún commit antiguo debemos copiar el hash pertinente del commit y pegar el hash a continuación.

Por ejemplo:

```
	git tag etiqueta-normal hash-copiado
	git tag -a v0.1 -m "version primaria basica" hash-copiado
```
Al utilizamos tag's podremos ver todo el trabajo hasta ese tag excluyendo todos sus commits sucesores.

```
	git checkout mi-etiqueta
	git log --decorate --oneline
	git log --decorate --oneline --all con esto vemos los commits superiores al presente **all**.
```
Para eliminar tags de algún commit utilizamos el siguiente comando:

```
	git tag --list
	git tag -d nombre-etiqueta
```

### Clonar repositorios
Para clonar algún repositorio copiamos la URL y utilizamos el siguiente comando:

```
	git clone url-del-repo
```
Este comando nos crea una nueva carpeta con el nombre del repositorio y todos sus archivos.

Si queremos asignarle un nombre particular a la carpeta utilizamos el mismo comando con el nombre pertinente

Por ejemplo:

```	
	git clone url-del-repo nombre-carpeta
```

### Ramas en GIT

 Para crear una rama en git utilizamos el siguiente comando:

 `	git branch nombre-rama`

 La rama estara en este caso apuntando al commit donde esta parado el master, **HEAD** nos dice donde estamos parados.
 Si queremos que **HEAD** apunte a la rama creada tenemos que utilizar el siguiente comando


 `	git checkout nombre-rama`

 Revisamos el log para ver la bifurcación

 `	git log --decorate --oneline --all --graph`

 El **HEAD** estará apuntando a la **rama** creada. Ahora tenemos que tener especial atención ya que si seguimos creando commits estaremos en la **rama** creada o mejor dicho en `Un mundo paralelo`. :scream:

Para regresar el apuntador a la rama master utilizamos el comando `git checkout master`. Si creamos un commit en el universo paralelo y retrocedemos a donde dejamos el **master** y realizamos un nuevo commit estos se irán por mundos diferentes, piensa en la rama de un arbol y que a esta le salga una rama más pequeña, son de la misma rama pero crecerán por separado.

Para saber en que commit o en que universo nos ubicamos utiliza el comando `git branch`.
```
	git log --decorate --all --graph
```

### Fusionar una ***rama*** con la línea principal del proyecto

Para fusionar las ramas debemos utilizar el log para ver las lineas de las ramificaciones y fusionar las que tengan mas interdependencia entre ellas, en este caso la más cercana para ir dando coherencia. Para fusionar una rama nos ubicamos en la rama principal a la que queramos agregarle la otra.

Por ejemplo:

```
	git merge nombre-rama
```
Una vez fusionada la rama podemos eliminar el apuntador de la rama que ya no utilizaremos:

```
	git branch -d nombre-rama
```
Los commit no se eliminan solo se elimina el apuntador a la **rama**

Para ver que ramos no han sido fusionadas y cuales si fusionamos utilizaremos los siguientes comando respectivamente:

```
	git branch --no-merged
	git branch --merged
```



