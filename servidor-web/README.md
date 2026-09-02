# Laboratorio 02 — Apache HTTP Server y VirtualHost con Docker

## Curso: Ingeniería Web

## 1. Objetivo

En este laboratorio se implementará un servidor web **Apache HTTP Server** utilizando Docker.

Partiendo de la página web desarrollada en el laboratorio anterior, se realizarán las siguientes actividades:

### Parte 1

Crear una imagen Docker denominada:

```text
iw_lab02_image_escobedo
```

La imagen deberá contener Apache HTTP Server configurado para atender en el puerto `8081`, con el `DocumentRoot`:

```text
/var/www/html
```

A partir de esta imagen se deberá crear el contenedor:

```text
iw_lab02_container_escobedo
```

### Parte 2

Crear dos sitios web:

1. **Sistema Académico**
2. **Sistema de Trámite Documentario**

Los archivos estarán ubicados en:

```text
/iw/webapps/sisacad/
```

y:

```text
/iw/webapps/sistradoc/
```

Los sitios deberán ser accesibles mediante:

```text
http://localhost:8081/sisacad/
```

y:

```text
http://localhost:8081/sistradoc/
```

Para ello se configurará Apache utilizando:

- `VirtualHost`
- `Alias`
- Directivas `<Directory>`

> **Material de apoyo:** consultar [HELP.md](HELP.md) para conocer los conceptos de Docker, Apache, VirtualHost, Alias y DocumentRoot antes de iniciar el laboratorio.

---

## 2. Requisitos previos

Verificar que Docker esté instalado:

```bash
docker --version
```

Verificar que Docker esté funcionando:

```bash
docker ps
```

---

## 3. Estructura del proyecto

Crear el directorio:

```bash
mkdir iw_lab02
cd iw_lab02
```

La estructura será:

```text
iw_lab02/
├── Dockerfile
├── apache/
│   └── 000-default.conf
├── web/
│   └── index.html
└── sites/
    ├── sisacad/
    │   └── index.html
    └── sistradoc/
        └── index.html
```

---

# PARTE UNO

## 4. Crear la página principal

Crear el directorio:

```bash
mkdir -p web
```

Crear:

```bash
vim web/index.html
```

Contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Ingeniería Web - Laboratorio 02</title>
</head>
<body>

    <h1>Ingeniería Web</h1>

    <h2>Laboratorio 02</h2>

    <p>
        Servidor Apache HTTP Server ejecutándose mediante Docker.
    </p>

    <p>
        DocumentRoot: /var/www/html
    </p>

</body>
</html>
```

> También se puede reutilizar la página HTML + CSS desarrollada en el laboratorio anterior.

---

## 5. Crear el Dockerfile

Crear:

```bash
vim Dockerfile
```

Contenido:

```dockerfile
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN sed -i 's/^Listen 80$/Listen 8081/' /etc/apache2/ports.conf

COPY web/ /var/www/html/

EXPOSE 8081

CMD ["apachectl", "-D", "FOREGROUND"]
```

### Explicación

- `FROM ubuntu:24.04`: utiliza Ubuntu como imagen base.
- `apt-get install -y apache2`: instala Apache.
- `Listen 8081`: configura Apache para escuchar en el puerto `8081`.
- `COPY web/ /var/www/html/`: copia la página al `DocumentRoot`.
- `EXPOSE 8081`: documenta el puerto utilizado.
- `CMD`: inicia Apache en primer plano, necesario para que el contenedor permanezca ejecutándose.

---

## 6. Construir la imagen Docker

Ejecutar:

```bash
docker build -t iw_lab02_image_escobedo .
```

Comprobar:

```bash
docker images
```

Debe aparecer una imagen similar a:

```text
REPOSITORY                 TAG       IMAGE ID       CREATED          SIZE
iw_lab02_image_escobedo   latest    xxxxxxxxxxxx   ...              ...
```

---

## 7. Crear el contenedor

Ejecutar:

```bash
docker run -d \
    --name iw_lab02_container_escobedo \
    -p 8081:8081 \
    iw_lab02_image_escobedo
```

La opción:

```text
-p 8081:8081
```

realiza el mapeo:

```text
PUERTO_HOST:PUERTO_CONTENEDOR
```

es decir:

```text
8081:8081
```

---

## 8. Verificar el contenedor

Ejecutar:

```bash
docker ps
```

Debe aparecer:

```text
iw_lab02_container_escobedo
```

Consultar el puerto:

```bash
docker port iw_lab02_container_escobedo
```

Se espera algo similar a:

```text
8081/tcp -> 0.0.0.0:8081
```

---

## 9. Probar Apache

Desde el navegador acceder a:

```text
http://localhost:8081/
```

También se puede utilizar:

```bash
curl http://localhost:8081/
```

Debe aparecer el contenido de:

```text
/var/www/html/index.html
```

---

## 10. Verificar el DocumentRoot

Ingresar al contenedor:

```bash
docker exec -it iw_lab02_container_escobedo bash
```

Ejecutar:

```bash
ls -la /var/www/html
```

Debe aparecer:

```text
index.html
```

Consultar la configuración de Apache:

```bash
apachectl -S
```

Revisar:

```bash
cat /etc/apache2/sites-available/000-default.conf
```

Salir:

```bash
exit
```

---

# PARTE DOS

## 11. Crear los dos sitios web

Crear:

```bash
mkdir -p sites/sisacad
mkdir -p sites/sistradoc
```

---

## 12. Crear el Sistema Académico

Crear:

```bash
vim sites/sisacad/index.html
```

Contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Sistema Académico</title>
</head>
<body>

    <h1>Sistema Académico</h1>

    <p>
        Bienvenido al Sistema Académico.
    </p>

    <p>
        Ingeniería Web - Laboratorio 02
    </p>

</body>
</html>
```

---

## 13. Crear el Sistema de Trámite Documentario

Crear:

```bash
vim sites/sistradoc/index.html
```

Contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Sistema de Trámite Documentario</title>
</head>
<body>

    <h1>Sistema de Trámite Documentario</h1>

    <p>
        Bienvenido al Sistema de Trámite Documentario.
    </p>

    <p>
        Ingeniería Web - Laboratorio 02
    </p>

</body>
</html>
```

---

## 14. Configurar Apache mediante VirtualHost

Crear:

```bash
mkdir -p apache
```

Crear:

```bash
vim apache/000-default.conf
```

Contenido:

```apache
<VirtualHost *:8081>

    ServerAdmin webmaster@localhost
    ServerName localhost

    DocumentRoot /var/www/html

    Alias /sisacad /iw/webapps/sisacad
    Alias /sistradoc /iw/webapps/sistradoc

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    <Directory /iw/webapps/sisacad>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    <Directory /iw/webapps/sistradoc>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

### Asociaciones importantes

```text
URL                                      Directorio

http://localhost:8081/             ->    /var/www/html/
http://localhost:8081/sisacad/     ->    /iw/webapps/sisacad/
http://localhost:8081/sistradoc/   ->    /iw/webapps/sistradoc/
```

---

## 15. Modificar el Dockerfile

Reemplazar el contenido del `Dockerfile` por:

```dockerfile
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN sed -i 's/^Listen 80$/Listen 8081/' /etc/apache2/ports.conf

COPY web/ /var/www/html/

COPY sites/sisacad/ /iw/webapps/sisacad/
COPY sites/sistradoc/ /iw/webapps/sistradoc/

COPY apache/000-default.conf \
     /etc/apache2/sites-available/000-default.conf

EXPOSE 8081

CMD ["apachectl", "-D", "FOREGROUND"]
```

---

## 16. Reconstruir la imagen

Detener el contenedor:

```bash
docker stop iw_lab02_container_escobedo
```

Eliminarlo:

```bash
docker rm iw_lab02_container_escobedo
```

Reconstruir la imagen:

```bash
docker build -t iw_lab02_image_escobedo .
```

---

## 17. Crear nuevamente el contenedor

```bash
docker run -d \
    --name iw_lab02_container_escobedo \
    -p 8081:8081 \
    iw_lab02_image_escobedo
```

Verificar:

```bash
docker ps
```

---

## 18. Verificar los sitios dentro del contenedor

Ingresar:

```bash
docker exec -it iw_lab02_container_escobedo bash
```

Comprobar:

```bash
ls -la /iw/webapps/
```

Debe aparecer:

```text
sisacad
sistradoc
```

Comprobar:

```bash
ls -la /iw/webapps/sisacad/
```

y:

```bash
ls -la /iw/webapps/sistradoc/
```

Cada directorio debe contener:

```text
index.html
```

---

## 19. Comprobar el VirtualHost

Dentro del contenedor:

```bash
apachectl -S
```

Debe observarse un `VirtualHost` asociado a:

```text
*:8081
```

También revisar:

```bash
cat /etc/apache2/sites-available/000-default.conf
```

Debe contener:

```apache
<VirtualHost *:8081>

    DocumentRoot /var/www/html

    Alias /sisacad /iw/webapps/sisacad

    Alias /sistradoc /iw/webapps/sistradoc

</VirtualHost>
```

Salir:

```bash
exit
```

---

## 20. Probar el Sistema Académico

Desde el navegador:

```text
http://localhost:8081/sisacad/
```

También:

```bash
curl http://localhost:8081/sisacad/
```

Debe aparecer:

```text
Sistema Académico
```

---

## 21. Probar el Sistema de Trámite Documentario

Desde el navegador:

```text
http://localhost:8081/sistradoc/
```

También:

```bash
curl http://localhost:8081/sistradoc/
```

Debe aparecer:

```text
Sistema de Trámite Documentario
```

---

## 22. Pruebas HTTP

Ejecutar:

```bash
curl -I http://localhost:8081/
```

Luego:

```bash
curl -I http://localhost:8081/sisacad/
```

Finalmente:

```bash
curl -I http://localhost:8081/sistradoc/
```

Las respuestas esperadas son similares a:

```text
HTTP/1.1 200 OK
```

El código HTTP `200` indica que Apache encontró correctamente el recurso solicitado.

---

## 23. Revisar los logs

Para observar las solicitudes:

```bash
docker exec -it iw_lab02_container_escobedo \
    tail -f /var/log/apache2/access.log
```

En otra terminal realizar:

```bash
curl http://localhost:8081/
curl http://localhost:8081/sisacad/
curl http://localhost:8081/sistradoc/
```

Para revisar errores:

```bash
docker exec -it iw_lab02_container_escobedo \
    cat /var/log/apache2/error.log
```

---

# 24. Verificación final

### Imagen

```bash
docker images | grep iw_lab02_image_escobedo
```

Debe existir:

```text
iw_lab02_image_escobedo
```

### Contenedor

```bash
docker ps | grep iw_lab02_container_escobedo
```

Debe existir:

```text
iw_lab02_container_escobedo
```

### Puerto

```text
8081
```

### DocumentRoot

```text
/var/www/html
```

### Sistema Académico

Directorio:

```text
/iw/webapps/sisacad/
```

URL:

```text
http://localhost:8081/sisacad/
```

### Sistema de Trámite Documentario

Directorio:

```text
/iw/webapps/sistradoc/
```

URL:

```text
http://localhost:8081/sistradoc/
```

### Alias

Debe existir:

```apache
Alias /sisacad /iw/webapps/sisacad
Alias /sistradoc /iw/webapps/sistradoc
```

### VirtualHost

Debe existir:

```apache
<VirtualHost *:8081>
```

---

# 25. Preguntas de comprobación

Responder:

1. ¿Qué función cumple Docker en este laboratorio?
2. ¿Cuál es la diferencia entre una imagen Docker y un contenedor?
3. ¿Qué función cumple Apache HTTP Server?
4. ¿Qué significa `Listen 8081`?
5. ¿Qué función cumple `DocumentRoot`?
6. ¿Qué función cumple `VirtualHost`?
7. ¿Qué función cumple `Alias`?
8. ¿Cuál es la diferencia entre `DocumentRoot` y `Alias`?
9. ¿Para qué se utiliza `<Directory>`?
10. ¿Qué diferencia existe entre `8081:8081` en Docker y `Listen 8081` en Apache?
11. ¿Qué sucedería si Apache escuchara en el puerto 80 pero Docker publicara solamente el puerto 8081 del contenedor?
12. ¿Por qué se utiliza `Require all granted` en los directorios publicados?

---

# 26. Evidencias a presentar

Presentar capturas de pantalla que demuestren:

1. Construcción de la imagen:

```bash
docker images
```

2. Contenedor ejecutándose:

```bash
docker ps
```

3. Contenido de `/var/www/html`.

4. Configuración del VirtualHost:

```bash
apachectl -S
```

5. Archivo:

```text
/etc/apache2/sites-available/000-default.conf
```

6. Sistema Académico funcionando:

```text
http://localhost:8081/sisacad/
```

7. Sistema de Trámite Documentario funcionando:

```text
http://localhost:8081/sistradoc/
```

8. Pruebas con `curl`:

```bash
curl http://localhost:8081/sisacad/
curl http://localhost:8081/sistradoc/
```

---

# 27. Arquitectura final

```text
                         NAVEGADOR
                             |
                             |
                     localhost:8081
                             |
                             v
              +---------------------------+
              |          DOCKER           |
              |                           |
              |  iw_lab02_container_     |
              |       escobedo            |
              |                           |
              |      Apache HTTP Server   |
              |          :8081            |
              |             |             |
              |       VirtualHost         |
              |             |             |
              |      +------+-------+     |
              |      |              |     |
              |      v              v     |
              |   /sisacad      /sistradoc|
              |      |              |     |
              |      v              v     |
              |  /iw/webapps/ /iw/webapps/|
              |    sisacad       sistradoc |
              |                           |
              |      /var/www/html        |
              |          |                |
              |       index.html          |
              +---------------------------+
```

---

# 28. Criterio de éxito

El laboratorio se considera correctamente realizado cuando:

- [ ] Existe la imagen `iw_lab02_image_escobedo`.
- [ ] Existe el contenedor `iw_lab02_container_escobedo`.
- [ ] Apache está instalado dentro del contenedor.
- [ ] Apache atiende en el puerto `8081`.
- [ ] El `DocumentRoot` es `/var/www/html`.
- [ ] Existe `/iw/webapps/sisacad/index.html`.
- [ ] Existe `/iw/webapps/sistradoc/index.html`.
- [ ] Existe un `VirtualHost` para el puerto `8081`.
- [ ] Está configurado `Alias /sisacad`.
- [ ] Está configurado `Alias /sistradoc`.
- [ ] Funciona `http://localhost:8081/`.
- [ ] Funciona `http://localhost:8081/sisacad/`.
- [ ] Funciona `http://localhost:8081/sistradoc/`.
- [ ] Las páginas pueden verificarse mediante `curl`.

---

## Fin del Laboratorio 02
