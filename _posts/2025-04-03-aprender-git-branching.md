---
layout: post
title:  "Cómo funcionan los comandos de git"
date: 2025-04-03
categories: explicaciones
---
**Fecha**: 12 de marzo de 2025  
**Autor**: [odv717]  
En este post se explicarán los comandos más usados de Git. Cómo funcionan y cómo se usan (nos basaremos en la página "learn git branching").


## Comandos mínimos para el uso de git. 
[desconozco como será más visual en github, si indicando codigo java, sh o html en los bloques de código]: #


   ```html
  Git clone <url>
   ```
Descarga el repositorio git que se encuentre en la ruta indicada, solo se hace una vez.  


   ```html
  Git add <ruta>
   ```
Añade el archivo o carpeta indicados en \<ruta> al staging de git, es decir, serán incluidos en el próximo commit. Si se introduce "." como ruta todos los cambios serán añadidos incluso si git no lo estaba siguiendo.


```html
  Git commit
```
Guarda todo lo añadido con el comando add en un commit listo para compartir.
Generalmente se usa con la opción  ``` -m "<mensaje>" ``` para indicar información sobre que se ha aportado, recomendable textos cortos y descriptivos. Otra opción a usar es  ```--amend ```la cual añade los últimos cambios añadidos a el commit anterior, evitando crear uno nuevo si se nos olvidó añadir algún archivo. También es posible usar ```-a``` para que el commit añada automáticamente todos los cambios en archivos que previamente hayan sido añadidos en algún momento a otro commit.


```html
  Git push <repositorio remoto> <rama>
```  
Sube todos los cambios commiteados del repositorios local al repositorio original (el indicado en \<url> de Git clone), haciéndolos visibles para los demás programadores. \<repositorio remoto> generalmente es origin y es raro tener más de uno. \<rama> indica que rama del repositorio remoto será actualizada con los cambios. si se escribe ``` Git push``` a secas se infiere ``` Git push origin main``` si estamos en la rama main, en otro caso la rama será en la que nos encontremos.  
También es posible complicar este comando, por ejemplo con ``` Git push origin <que subir>:<a donde>>```. Con esto se podría subir, por ejemplo, un commit específico (usando su hash o referencia relativa como HEAD,main^1...) en lugar de  \<que subir> y el nombre de una rama remota en \<a donde>, pudiendo ser una nueva rama. También es posible eliminar una rama local dejando  \<que subir> vacío, es decir  ``` Git push origin :<a donde>>```.


```html
  Git pull <repositorio remoto>
```
Descarga todos los cambios publicados sobre la rama en la que nos encontremos en el repositorio remoto. equivale a ejecutar ```Git fetch``` (descarga el contenido remoto) y ``` Git merge``` (lo fusiona con nuestra rama local,creando un nuevo commit que indica la fusión). Tiene la opción ```--rebase``` lo cual no crea el nuevo commit  si no que coloca los commits remotos en línea con los locales (como si hubiesen ocurrido en la misma rama unos después de otros en lugar de en dos ramas y de forma paralela). Esto ocurre ya que se usa ``` Git rebase``` en lugar de ``` Git merge```. Hacer pull antes de trabajar es una buena práctica para reducir el riesgo de conflictos.


### Si el proyecto aun no es un repositorio git
```html
Git init
```
Si el proyecto únicamente existe en nuestro pc o aun no usa git podemos usar este comando para crear la carpeta oculta .git y comenzará a ser considerado como tal


```html
Git remote
```
Si queremos añadir un repositorio remoto a un repositorio usaremos ``` Git remote add <nombre> <url>```. Tras ello ya podremos trabajar como de costumbre, aunque probablemente lo primero que querramos hacer es un push para que el resto del equipo vea nuestro trabajo. Si queremos eliminar un repositorio remoto podemos usar ``` Git remote rm <nombre> ``` o podemos asignar una nueva url a un remote ya existente con ``` Git remote set-url <nombre> <url>```. Si no sabemos que remotes hay configurados se puede comprobar con la opción ```-v```
## Comandos para gestión


```html
Git fetch
```
El ejecutar este comando git descarga todos los commits del repositorio remoto a las ramas locales vinculada a el (o/main por ejemplo, pero esos commits aun NO están en main hasta que no se haga un merge o rebase). También permite ser muy especificos como ``` Git fetch <repositorio remoto> <origen>:<rama destino>``` de esta manera puedes seleccionar origin como \ <repositorio remoto> t traer un commit especificandolo en \<origen> a una rama local \<rama destino> omitiendo que este mismo pase por las ramas locales conectadas con las remotas, es algo que rara vez es útil, pero es posible. Si la rama de destino no existe se creara automáticamente desde donde estemos posicionados.


```html
Git checkout <rama>
```
Este comando permite cambiar la rama sobre la que se está trabajando introduciendo el nombre donde \<rama>. También es posible hacer checkot sobre un commit, pudiendo así ver el código en ese commit específico. se puede usar ```-b ``` para que en caso de que la rama de destino no exista la cree, usando la actual como base. NOTA: Al movernos sobre un commit podremos crear nuevos commits pero estos commits no estarán sobre una rama incluso si el commit al que nos hemos movido está siendo apuntado por una rama (el nuevo commit será apuntado únicamente por HEAD).


```html
Git merge <rama>
```
Merge unifica la rama sobre la que estamos con la que indicamos a través de \<rama> creando un commit nuevo.


```html
Git rebase <rama>
```
Con este comando la rama en la que nos encontramos se posicionará posteriormente a la indicada en \<rama> perdiendo la independencia en el historial por el camino. Será como si los comits de la rama en la que nos encontramos se hubiesen hecho después de la rama objetivo. Es compatible con la configuración ```-i``` que permite reordenar los commits movidos. Además si se le pasan dos ramas ``` Git rebase <ramaActual> <ramaObjetivo>``` la rama \<ramaObjetivo> será colocada posteriormente a \<ramaActual>, ahorrandonos asi hacer ``` Git checkout <rama>``` hacia \<ramaObjetivo> para luego hacer ``` Git rebase <rama>``` hacia \<ramaActual>.


```html
Git branch
```
Este comando lista las ramas actuales del repositorio git. Con ``` Git branch <rama>``` creamos una rama sobre donde estemos pero no nos moveremos a ella y con ``` Git branch <rama> <lugar>``` la rama \<rama> se creará sobre \<lugar>, ya sea un commit,rama,etiqueta... . Se le puede añadir la opción ```-f <rama> <lugar>``` para obligar a que la \<rama> existente actualiza su puntero al \<lugar> indicado. Tambien es compatible con ``` -d <rama>``` para eliminar la rama \<rama>.


```html
Git revert <commit>
```
Revert añade un nuevo commit a la historia  deshaciendo los cambios del commit indicado en \<commit>. Si se quieren eliminar los cambios añadidos por varios commits revert acepta que se le pasen múltiples commits ```
Git revert <commit1> <commit2> <commit3> ...```


```html
Git reset <commit>
```
Hace retroceder (o avanzar) la rama al commit indicado, para retroceder un commit se pondría HEAD~1 en el lugar de \<commint>. Este método es recomendado para ramas aun no subidas al repositorio remoto ya que al retroceder el otro commit sigue estando por delante en la historia y es donde apuntarían las ramas remotas. También ofrece la oportunidad de modificar ramas sobre las que no estamos con ``` Git reset <rama> <commit>``` usando el nombre la \<rama> que queremos modificar y el \<commit> al que queremos que apunte.Hay que tener cuidado con el uso de reset, pues puede hacer que una rama apunte a un comit que NO estaba en ella, actuando como ``` Git branch -f <rama> <lugar>``` siendo \<lugar> el commit.


```html
Git cherry-pick <commit>
```
Esta utilidad copia el \<commit> indicado a la rama sobre la que nos encontramos con otro hash(si estamos únicamente sobre HEAD también copiará el commit pero ninguna rama apuntará a él). al usar cherry pick no se pueden clonar commits que ya esten en esa rama. Si se quieren duplicar varios commits a la vez es posible hacer ```
Git cherry-pick <commit1> <commit2> <commit3>...```




```html
Git tag
```
Sirve para listar las etiquetas creadas, pero ``` Git tag <Nombre del tag> <Elemento etiquetado>``` sirve para crear una tag, la cual puede ser referenciada en el futuro por otros comandos, por ejemplo, podemos hacer un checkout poniendo el \<Nombre del tag>  del commit al que se la pusimos en lugar de buscar su hash. Se introduce únicamente  ``` Git tag <Nombre del tag> ``` la etiqueta se pondrá automáticamente sobre el commit en el que nos encontramos.


```html
Git describe
```
Este comando se basa en las etiquetas hechas con ``` Git tag ``` ya que emite por pantalla una salida tipo tag_numCommit_hash, tag es la etiqueta más cercana al commit sobre el que nos encontramos, numCommit_hash es el número de commits  a los que estamos (1 es padre o hijo,2 es abuelo o nieto...) y hash es el hash único del comit. en caso de ejecutar el comando en un commit cuyo padre e hijo tienen comit el comando únicamente mostrar la salida de la etiqueta del padre. En caso de describir un commmit que tiene una etiqueta simplemente se muestra la etiqueta. Para no tener que hacer checkut o similares es posible solicitar estos datos así ``` Git describe <commmit>```, siendo commit cualquier commit o forma de obtenerlo, como una rama, hash o incluso una propia etiqueta, pero hacer eso no aporta información pues la salida del comando es únicamente la etiqueta que ya conocías pues era necesario para el git describe.