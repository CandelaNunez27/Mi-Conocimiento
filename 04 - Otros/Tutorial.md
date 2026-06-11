# titulo
## titulo
### titulo
#### titulo
##### titulo
###### titulo


---
línea

*de costado*

**negrita**

~~tachado~~

==resaltado amarillo

- viñeta
1. enumeración

- [ ] tags
- [x] Tareas

Acceso[^1]

| fecha | hora  |
| ----- | ----- |
| 22/03 | 18 hs |
> **Ejemplos




[1° Año] enlace dentro de obsidian

[Google](https://www.google.com/?hl=es&zx=1775787126621 )


![Tutorial](https://www.youtube.com/watch?v=8xgv8dy6w1I)


```bash
sudo apt upgrade
```

copiar y pegar imágenes con ctrl + p seleccionar link cosverter vault: links in Markdown para ser visibles en github
![194](04%20-%20Otros/Imagenes/icons%20tina.jpg)

[^1]: Nota 1

CTRL + P : para abrir barra de acciones.

# hacer otra bodega

### Guía: Conectar nueva bóveda de Obsidian a GitHub (CachyOS)

#### Paso 1: Crear la bóveda local

1. Abrí **Obsidian** y hacé clic en el ícono de la bóveda (abajo a la izquierda).

2. Seleccioná **Crear** (_Create new vault_).

3. Ponele el nombre de tu proyecto o materia.

4. En **Ubicación**, elegí una carpeta real de tu disco duro (por ejemplo, adentro de tu carpeta de `Documentos` o `Proyectos`). Nada de nubes ni discos virtuales.

5. Dale a **Crear**.


#### Paso 2: Crear el repositorio vacío

1. Entrá a tu cuenta de **GitHub** en el navegador.

2. Hacé clic en el botón **`+`** (arriba a la derecha) y elegí **New repository**.

3. Ponele el mismo nombre de tu bóveda.

4. **¡Paso clave!** Asegurate de dejar desmarcadas las opciones de README, .gitignore y licencia. El repo tiene que crearse 100% vacío.

5. Hacé clic en **Create repository** y copiá la URL HTTPS que te da la página (la que termina en `.git`).


#### Paso 3: Inicializar Git y ocultar la basura

1. Abrí tu **terminal** en CachyOS.

2. Navegá hasta la carpeta de tu nueva bóveda usando `cd`. Por ejemplo:
    
    Bash
    
    ```
    cd /home/cande/Documentos/TuNuevaBoveda
    ```
    
3. Inicializá el control de versiones:
    
    Bash
    
    ```
    git init
    ```
    
4. Creá el archivo mágico para que GitHub ignore las configuraciones de Obsidian y te quede el perfil impecable:
    
    Bash
    
    ```
    echo ".obsidian/" > .gitignore
    ```
    

#### Paso 4: El primer guardado manual

En esa misma terminal, ejecutá estos comandos uno por uno para subir los archivos base a GitHub:

1. Prepará los archivos (esto incluye tu nuevo `.gitignore`):
    
    Bash
    
    ```
    git add .
    ```
    
2. Creá el primer punto de guardado:
    
    Bash
    
    ```
    git commit -m "Primer inicio de la bóveda"
    ```
    
3. Asegurate de que la rama principal se llame `main`:
    
    Bash
    
    ```
    git branch -M main
    ```
    
4. Conectá tu carpeta local con el repositorio de GitHub (reemplazá la URL por la tuya):
    
    Bash
    
    ```
    git remote add origin https://github.com/CandelaNunez27/tu-nuevo-repo.git
    ```
    
5. Mandá los archivos a la nube:
    
    Bash
    
    ```
    git push -u origin main
    ```
    

#### Paso 5: Armar la portada (README)

1. Volvé a **Obsidian**.
    
2. Creá una nota nueva y ponele de título exactamente **`README`** (todo en mayúsculas).
    
3. Escribí ahí adentro de qué trata el proyecto. Esta nota va a ser la presentación visual de tu repositorio en GitHub.
    

#### Paso 6: Automatizar todo (Para no tocar más la terminal)

1. En Obsidian, andá a **Configuración** (el engranaje).
    
2. Entrá a **Community plugins** y desactiva el modo seguro (_Enable community plugins_).
    
3. Buscá, instalá y activá el plugin **`Obsidian Git`**.
    
4. Entrá a las opciones del plugin y configurá el piloto automático:
    
    - **Vault Backup Interval (minutes):** Poné cada cuánto tiempo querés que se guarde solo (ejemplo: `30` minutos).
        
    - **Auto push to remote on backup:** Asegurate de que esté **activado** para que lo suba a GitHub directamente.
        

¡Listo! 