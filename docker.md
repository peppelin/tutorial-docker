name: inverse
layout: true
class: center, middle, inverse
---
name: basic
layout: true
class: left, top, inverse
---
class: center, middle

# Docker en 3 minutos

.footnote[ Peppelin [github](https://github.com/peppelin/tutorial-docker)]

---
class: basic

# Docker en 3 minutos

## Agenda
1. Descargar una imagen
2. Ejecutar un contenedor
3. Parar un contenedor
4. Conectar al contenedor
5. Exponer puertos
6. Montar volumenes
7. Limpiar contenedores e imagenes
---
name: basic
# Docker en 3 minutos

## Descargar una imagen
Nos descargaremos una imagen de docker.
```terminal
docker pull nginx:latest
```
* **nginx** --> imagen a descargar
* **latest** --> version de la imagen

En la medida de lo posible, **nunca usar latest** y especificar la version que queremos.
```terminal
docker pull nginx:stable-alpine
```

.footnote[.red[ Este comando solo descarga una imagen, no ejecuta nada.]]


---
name: basic
# Docker en 3 minutos

## Ejecutar un contenedor
```terminal
docker run --name web -d nginx:stable-alpine 
```
Ejecutaremos el contenedor basado en la imagen **nginx:stable-alpine**.
Se le asignara el nombre de **web**.
**-d**: indica que el contenedor se ejecuta en segundo plano.

---
name: basic
# Docker en 3 minutos

## Parar un contenedor
```terminal
docker ps
CONTAINER ID    IMAGE                               COMMAND                   CREATED               STATUS                           PORTS                     NAMES                   SIZE
d4632291269b    docker.io/library/nginx:latest      "/docker-entrypoint.…"    2 minutes ago         up                                                         web                     8.0 KiB (virtual 142.5 MiB)
```
```terminal
docker stop 16dd4dfac175
docker stop web
```
**docker ps** nos indica los contenedores que tenemos corriendo.
Pararemos el contenedor por el **NAME** or por su **CONTAINER ID**.

---

name: basic
# Docker en 3 minutos

## Conectar al contenedor
```terminal
$ docker exec -ti web /bin/bash
root@d4632291269b:/#
```
Ejecutaremos el comando **/bin/bash** dentro del contenedor **web**.
* **--ti** indica que ejecutaremos una shell y que la atache al terminal.

---
name: basic
# Docker en 3 minutos

## Publicar puertos
Abrimeros un puerto para que nuestra aplicación sea accesible desde fuera.
```terminal
docker run --name web -d -p 8080:80 nginx:stable-alpine 
```
Ahora nuestro servidor es accesible desde nuestro pc mediante [http://localhost:8080](http://localhost:8080)

* **8080**: puerto de nuestro pc
* **80**: puerto que escucha nuestro contenedor

---
name: basic
# Docker en 3 minutos

## Montar volumenes
```terminal
docker run --name web -d -p 8080:80 -v html:/usr/share/nginx/html nginx:stable-alpine 
```
La carpeta local **html** contendra nuestra web y sera accesible desde [http://localhost:8080](http://localhost:8080)

.footnote[.red[Si da un error de puerto en uso, pararemos el contenedor que este usando el puerto 8080]]
---
name: basic
# Docker en 3 minutos

## Limpiar contenedores e imagenes

```terminal
docker system prune --all
```

Este comando elimina:
* Contenedores parados
* Imagenes sin contenedores asociados
* Volumenes que no estan asociados a contenedores
