# GitHub 

Cosas que debes tener en cuenta desde ya **HEAD** es tu presente.

### Configurando GIT por primera vez

```
git config --global user.name "nombre completo"
git config --global user-email "correo-sin-comillas-dobles"
git --config core.editor subl
git config --list
```
### De la zona de trabajo al area de preparación

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
Si queremos ser más detallados utilizamos el comando:

```
	git diff --cached
```
Podemos ver la diferencia entre dos **commit** especificos utilizando

```
	git diff id-commit-1 id-commit-2
```
Esto nos mostrará en rojo lo eliminado y en verde lo agregado.
Es importante tener conocimiento de los ID o HASH para ir comparando el trabajo realizado.

### Creando el .gitignore
En este paso únicamente tienes que crear el archivo directamente desde sublime o su editor favorito el archivo **.gitignore** dentro del archivo escribe el nombre de su archivo a ignorar... por ejemplo:

```
	mi-archivo-javascript.js
	mi-style.css
	/node_modules
	index.html
```
Si utilizamos `git status` veremos que los archivos ignorados no aparecen.  :grin:
### Atajos

Si queremos agregar todos los archivos independiente de cual sea a la zona de **preparacion** utilizamos:

```	
	git add .
```
Si no queremos agregar los archivos uno a uno podemos agregar al area de **preparación** solo los archivos que tenemos bajo seguimiento con: 

```
	git add -A
``` 
Se agregaran todos los archivos que tengamos en seguimiento.
Cuando utilizamos el comando `git add nombre-archivo` es cuando damos seguimiento de un archivo con git.

Otro atajo rápido sería usar:

```
	`git commit -am "commit saltando la zona de preparacion"
	 git log --decorate --oneline
```

### Log personalizados


```
	git log --pretty=format:"%h - %an, %ar  : %s"

	git log --after="2016-11-25 00:00:00"

	git log --before="2016-08-08 00:00:00" 

	git log -n
``` 
donde la **n** determinara la cantidad de commits que quieres ver

Los before y after los podemos utilizar anidados para dar un rango especifico de tiempo.


### Deshacer cambios

En este apartado dejaré algunos comandos que nos sirven para deshacer los cambios realizos en los commit

Si por X motivo realizamos un commit y no agregamos todo lo que debíamos o queremos agregarle alguna modificación que pertenecerá al mismo commit podemos utilizar el siguiente comando para reemplazar el último commit por el que si querías realizar :wink: 

```
	git commit --amend
```

Esto abrira el editor que tengas para modificar el commit con los archivos que fueron cambiados y los que estan en el area de preparación.

Para sacar un archivo de la zona de **preparación** utilizamos el comando

```
	git reset HEAD nombre-del-archivo
```
### Etiquetas !important buenas practicas y versionado de tu proyecto.
Podemos listar las etiquetas que ya existen con:


`	git tag`

Creamos nuestra primera etiqueta, esta etiqueta se le agregará al **commit** mas reciente
	
```
	git tag etiqueta-nueva
	git log --decorate

```
Etiqueta anotada **-a**, se guardan en la bd de git como un objeto más completo que la etiqueta normal. Contiene el nombre del etiquetador, correo, fecha y tienen un **mensaje con -m**.
```
	git tag -a v1.0 -m "version 1.0 estable"
	git tag
	git log --decorate
	git show v1.0
	git show etiqueta-nueva
```
Si queremos versionar commit antiguos debemos copiar el hash pertinente y pegar el hash a continuación... por ejemplo:

```
	git tag etiqueta-normal hash-copiado
	git tag -a v0.1 -m "version primaria basica" hash-copiado
```
Cuando utilizamos un tag podremos ver todo el trabajo hasta esa etiqueta más no los que pertenecen despues de la etiqueta.

```
	git checkout mi-etiqueta
	git log --decorate --oneline
	git log --decorate --oneline --all y veremos los commits superiores al presente.
```
Para eliminar tags de nuestros commit lo hacemos con el siguiente comando:

```
	git tag --list
	git tag -d nombre-etiqueta
```

### Clonar repositorios
Para clonar sacamos la URL del repositorio a clonar y utilizamos el siguiente comando:

```
	git clone url-del-repo
```
Esto nos crea una nueva carpeta con el nombre del repo y todos sus archivos.
Si queremos dar nosotros el nombre a la carpeta utilizamos el mismo comando con el nombre que le indiquemos... ejemplo:

```	
	git clone url-del-repo nombre-carpeta
```

### Ramas en GIT

 Para crear una rama en git utilizamos el siguiente comando

 `	git branch nombre-rama`

 La rama estara en este caso apuntando al commit donde esta parado el master, **HEAD** nos dice donde estamos parados.
 Si queremos que **HEAD** apunte a la rama creada tenemos que utilizar el siguiente comando


 `	git checkout nombre-rama`

 Revisamos el log para ver la bifurcación

 `	git log --decorate --oneline --all --graph`

 El **HEAD** estará apuntando a la **rama** creada. Ahora tenemos que tener especial atención ya que si seguimos creando commits estaremos en la **rama** creada o mejor dicho en `Un mundo paralelo` :scream:

Para regresar el apuntador a la rama master utilizamos el mismo comando de `git checkout master`. Si creamos un commit en el universo paralelo y retrocedemos a donde dejamos el **master** y realizamos un nuevo commit estos se irán por mundos diferentes... piensa en la rama de un arbol que le salga una más pequeña, son de la misma rama pero crecerán por separado.

Para saber en que commit o en que universo estas utiliza el comando `git branch`

```
	git log --decorate --all --graph
```

### Fusionar una ***rama*** con la linea principal del proyecto

Para fusionar utilizamos el log para ver las lineas de las ramificaciones y fusionar las que tengan mas interdependencia, la más cercana para ir dando coherencia. Para fusionar una rama nos ubicamos en la rama principal a la que queramos agregarle la otra... por ejemplo:

```
	git merge nombre-rama
```
Una vez fusionada la rama podemos eliminar el apuntador de la rama que ya no utilizaremos:

```
	git branch -d nombre-rama
```
Los commit no se eliminan solo se elimina el apuntador a la **rama**

Para ver que ramos no han sido fusionadas y cuales si fusionamos, utilizamos los siguientes comando correspondientemente:

```
	git branch --no-merged
	git branch --merged
```
