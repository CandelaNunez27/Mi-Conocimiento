# Práctica: Git

### Primeros pasos

1. Seleccionar repositorio:
	 Nos vamos a Github y buscamos el repositorio, entramos y le damos al boton verde de code y copiamos el https. Si es nuestro el repo podemos hacerpo por ssh
	 
	 En la consola hacemos `git clone https://dasmdamsasda.git` así clonamos un repo
	
	 con ssh `git clone git@github.com:julian/repo.git ` si ya tenemos todo nuestro git logeado en nuestra consola
	 
	 para compartirles a otros y que puedan modificar el original hay que ir a ajustes > ssh and gpg keys > new ss key
	 
	 Nos paramos en el repo `ls -la` y `get status` o  `git branch` para ver donde estamos posicionados. 
	 
	 
	 
	 

2.  Primeros Actions:
	 
	 en course_ing_cloud le damos crear una nueva carpeta llamada .get/workfows, entro de esta colocamos un archivo llamado primer-actions.yaml. volvemos a tirar `get status` si refrescamos la web aun no aparece por ende tiramos `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main` si aparece el delta es que si algo se cambio. por ende refrezcamos ahora y nos sale arriba actions y nos aparecera unos regitros / eventos de acciones.  nos sale que falta el o en el yaml
	 
	 
	 En el archivo  hello-world-c1.yaml escribimos name: Hello-word-Ipap, on: push, jobs:, hola:, run-on: ubuntu-latest
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  que el jobs le falta el step
	 
	 volvemos al yaml  y colocamos steps:. - name: Hello-world-Ipap, run: echo "Hello, world "
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  en verde y vemos el hello world
	 
	 volvemos al yaml  y colocamos  - name: touch file, run:  touch test.txt,   .- name: set test.txt, run: echo "Hello, world " >> test.txt,  , - name: show file, run: cat -n test.txt
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  en verde y vemos el hello world mas el hola mundo en el archivo txt
	 
	 volvemos al yaml  y colocamos  otro jobs. otro;. runs-on: ubuntu-latest, steps;, - name: LS, run:  ls -la 
	 
	 `git add .`,  `git commit -m "actions c1 2"` y ahora `git push origin main`y refrescamos sale  en verde y vemos los jobs en un bloque y vemos lo que agregamos
	 
	 volvemos al yaml  y colocamos  debajo del "Hello, world " >> test.txt .  - name: LS, run:  ls -la. Y debajo de otro:, runs-on: ubuntu-latest. needs: [hola]. y arriba del ls. - name: checkout repo, uses: actions/checkout@v4
	 
	 `git add .`,  `git commit -m "actions c1 3"` y ahora `git push origin main`y refrescamos sale  en verde y vemos los jobs divididos en dos bloques cada uno, siendo dependientes del otro. y dentro mostramos todo lo que agregamos. vemos el checkout que es un uses, donde nos muestra  run y syncing reposities. nos trajo como esa libreria, donde vemos que el ls se copio todo nuestro repo.
	 
	 volvemos al yaml  y colocamos  cambiamos el on. on:,   push,    braches: ["integration"], pull_request:,    braches:,   - main
	 
	 `git add .`,  `git commit -m "actions c1 4"` y ahora `git push origin main`y refrescamos y no nos aparece. porque no tenemos la rama integration. por ende nos vamos a code > main > ver braches > new branch > integration > origen main
	 Porque por lo general la barra main se suele usar como representar Produccion. que esta protegida,  ya que no sé deberia hacer cambio o borrar como venimos haciendo.  y integrations suele ser de desarrollo donde se trabaja los entornos de prueba, hasta que estemos seguro que lo que tenemos desarrollado va para produccion
	 
	 por ende, tiramos `git fetch` que nos trae la rama que creamos trae las cosas pero no trae las modificaciones de cofigo para eso esta pull , nos cambiamos de rama con `git checkout integration`
	 
	 `git add .`,  `git commit -m "actions c1 4"` y ahora `git push origin integration`y refrescamos sale  en verde y vemos que ahora ya nos aparece.
	 
	
 
3. Mas complicado:
	 nos vamos a la carpeta course_ing_cloud  > modulos > mod2 > class3 > demo > resiliencia > app-inventario > dockerfile y app.py. los copiamos y los pegamos en course_ing_cloud 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/18uYo9cBEgIdKgOjMBoTIkTj3-xH7D7VX/view
