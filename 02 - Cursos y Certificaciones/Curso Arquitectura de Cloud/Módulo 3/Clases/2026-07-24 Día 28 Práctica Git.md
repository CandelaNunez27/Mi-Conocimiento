# Práctica: Git

### Primeros pasos

1. Seleccionar repositorio:
	 Nos vamos a Github y buscamos el repositorio, entramos y le damos al boton verde de code y copiamos el https. Si es nuestro el repo podemos hacerpo por ssh
	 
	 En la consola hacemos `git clone https://dasmdamsasda.git` así clonamos un repo
	
	 con ssh `git clone git@github.com:julian/repo.git ` si ya tenemos todo nuestro git logeado en nuestra consola
	 
	 para compartirles a otros y que puedan modificar el original hay que ir a ajustes > ssh and gpg keys > new ss key
	 
	 Nos paramos en el repo `ls -la` y `get status` o  `git branch` para ver donde estamos posicionados. 
	 
	 
	 
	 
	 
2.  Primeros Actions:
	 
	 en course_ing_cloud le damos crear una nueva carpeta llamada .get/workfows, entro de esta colocamos un archivo llamado hello-world-c1.yaml. volvemos a tirar `get status` si refrescamos la web aun no aparece por ende tiramos `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main` si aparece el delta es que si algo se cambio. por ende refrezcamos ahora y nos sale arriba actions y nos aparecera unos regitros / eventos de acciones.  nos sale que falta el o en el yaml
	 
	 
	 En el archivo  hello-world-c1.yaml escribimos name: Hello-word-Ipap, on: push, jobs:, hola:, run-on: ubuntu-latest
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  que el jobs le falta el step
	 
	 volvemos al yaml  y colocamos steps:. - name: Hello-world-Ipap, run: echo "Hello, world "
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  en verde y vemos el hello world
	 
	 volvemos al yaml  y colocamos  - name: touch file, run:  touch test.txt,   .- name: set test.txt, run: echo "Hello, world " >> test.txt,  , - name: show file, run: cat -n test.txt
	 
	 `git add .`,  `git commit -m "actions c1 1"` y ahora `git push origin main`y refrescamos sale  en verde y vemos el hello world mas el hola mundo en el archivo txt
	 
	 volvemos al yaml  y colocamos  otro jobs. otro;. runs-on: ubuntu-latest, steps;, - name: LS, run:  ls -la 
	 
	 `git add .`,  `git commit -m "actions c1 2"` y ahora `git push origin main`y refrescamos sale  en verde y vemos el hello world mas el hola mundo en el archivo txt
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/18uYo9cBEgIdKgOjMBoTIkTj3-xH7D7VX/view
