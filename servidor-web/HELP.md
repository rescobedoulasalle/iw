# HELP — Conceptos fundamentales del Laboratorio 02

## Curso: Ingeniería Web

Este documento sirve como material de apoyo para comprender los conceptos utilizados en el Laboratorio 02.

---

# 1. ¿Qué es Docker?

**Docker** es una plataforma que permite empaquetar y ejecutar aplicaciones dentro de **contenedores**.

Un contenedor proporciona un entorno aislado para ejecutar una aplicación junto con las dependencias y configuraciones necesarias.

En este laboratorio utilizaremos Docker para ejecutar Apache HTTP Server.

La relación básica será:

```text
+--------------------------------------+
|          Sistema operativo           |
|                                      |
|              Docker                  |
|                 |                    |
|                 v                    |
|        +-------------------+         |
|        |    Contenedor     |         |
|        |                   |         |
|        | Apache HTTP       |         |
|        | Server            |         |
|        |                   |         |
|        | /var/www/html     |         |
|        | /iw/webapps/      |         |
|        +-------------------+         |
|                                      |
+--------------------------------------+
```

## Imagen y contenedor

En Docker debemos diferenciar:

**Imagen:** plantilla utilizada para crear contenedores.

**Contenedor:** instancia creada a partir de una imagen.

En este laboratorio:

```text
Imagen
iw_lab02_image_escobedo
        |
        | docker run
        v
Contenedor
iw_lab02_container_escobedo
```

La imagen se construirá utilizando:

```text
Dockerfile
```

Por ejemplo:

```bash
docker build -t iw_lab02_image_escobedo .
```

Posteriormente se crea el contenedor:

```bash
docker run -d \
    --name iw_lab02_container_escobedo \
    -p 8081:8081 \
    iw_lab02_image_escobedo
```

---

# 2. ¿Qué es Apache HTTP Server?

**Apache HTTP Server** es un servidor web que permite atender solicitudes HTTP y entregar recursos web a clientes como los navegadores.

Cuando el usuario escribe:

```text
http://localhost:8081/
```

el navegador realiza una solicitud HTTP.

Apache recibe la solicitud, determina qué recurso corresponde y devuelve una respuesta HTTP.

El flujo básico es:

```text
Navegador
    |
    | HTTP Request
    v
localhost:8081
    |
    v
Apache HTTP Server
    |
    | busca el recurso
    v
Archivo HTML
    |
    | HTTP Response
    v
Navegador
```

En este laboratorio Apache estará ejecutándose dentro de un contenedor Docker.

---

# 3. Puerto de Apache

Un servidor web necesita escuchar en un **puerto** para recibir solicitudes.

Tradicionalmente HTTP utiliza:

```text
80
```

En este laboratorio utilizaremos:

```text
8081
```

La configuración:

```apache
Listen 8081
```

indica a Apache:

> Escucha las solicitudes HTTP que lleguen al puerto 8081.

Docker debe publicar ese puerto hacia el equipo anfitrión:

```bash
-p 8081:8081
```

La sintaxis es:

```text
-p PUERTO_HOST:PUERTO_CONTENEDOR
```

Por lo tanto:

```text
8081:8081
```

significa:

```text
Equipo anfitrión                 Contenedor
      |                               |
      |       puerto 8081             |
      +------------------------------>|
                                      |
                               Apache :8081
```

Cuando se accede a:

```text
http://localhost:8081/
```

Docker recibe la conexión en el puerto `8081` del equipo anfitrión y la envía al puerto `8081` del contenedor.

---

# 4. ¿Qué es DocumentRoot?

`DocumentRoot` es una directiva de Apache que define el **directorio principal desde donde Apache sirve los archivos web**.

En este laboratorio:

```apache
DocumentRoot /var/www/html
```

Esto significa que:

```text
http://localhost:8081/
```

se relaciona con:

```text
/var/www/html/
```

Por ejemplo:

```text
/var/www/html/
├── index.html
├── css/
│   └── estilos.css
└── images/
    └── logo.png
```

Las solicitudes podrían corresponder a:

```text
http://localhost:8081/
http://localhost:8081/css/estilos.css
http://localhost:8081/images/logo.png
```

Conceptualmente:

```text
URL
http://localhost:8081/
        |
        v
DocumentRoot
/var/www/html/
        |
        v
index.html
```

---

# 5. ¿Qué es VirtualHost?

Un **VirtualHost** permite definir la configuración de un sitio web dentro de Apache.

Apache puede atender diferentes sitios utilizando diferentes:

- nombres de dominio;
- puertos;
- direcciones IP;
- configuraciones.

La configuración básica utilizada en este laboratorio es:

```apache
<VirtualHost *:8081>

    ServerName localhost

    DocumentRoot /var/www/html

</VirtualHost>
```

La expresión:

```apache
<VirtualHost *:8081>
```

indica que esta configuración se aplicará a las solicitudes recibidas en el puerto `8081`.

El símbolo `*` representa las interfaces de red disponibles para ese puerto.

---

# 6. ¿Qué es Alias?

La directiva `Alias` permite asociar una **URL** con un **directorio físico**.

La sintaxis es:

```apache
Alias URL DIRECTORIO
```

Por ejemplo:

```apache
Alias /sisacad /iw/webapps/sisacad
```

significa:

```text
URL                         Directorio físico

/sisacad      ----------->  /iw/webapps/sisacad
```

Por lo tanto:

```text
http://localhost:8081/sisacad/
```

corresponde a:

```text
/iw/webapps/sisacad/
```

---

# 7. Ejemplo de Alias

Supongamos:

```text
/iw/webapps/sisacad/
└── index.html
```

y Apache tiene:

```apache
Alias /sisacad /iw/webapps/sisacad
```

Cuando el usuario solicita:

```text
http://localhost:8081/sisacad/
```

Apache busca:

```text
/iw/webapps/sisacad/index.html
```

El proceso puede visualizarse así:

```text
/sisacad/
     |
     v
/iw/webapps/sisacad/
     |
     v
index.html
```

Por lo tanto, `Alias` permite publicar un directorio que no necesariamente se encuentra debajo del `DocumentRoot`.

---

# 8. DocumentRoot vs Alias

Es importante distinguirlos.

## DocumentRoot

Define el directorio principal:

```apache
DocumentRoot /var/www/html
```

Por ejemplo:

```text
http://localhost:8081/
        |
        v
/var/www/html/
```

## Alias

Publica otro directorio mediante una URL:

```apache
Alias /sisacad /iw/webapps/sisacad
```

Por ejemplo:

```text
http://localhost:8081/sisacad/
        |
        v
/iw/webapps/sisacad/
```

La diferencia:

```text
                 Apache
                   |
              localhost:8081
                   |
        +----------+----------+
        |                     |
        v                     v
 DocumentRoot               Alias
        |                     |
        v                     v
/var/www/html        /iw/webapps/sisacad
        |                     |
        v                     v
 index.html              index.html
```

---

# 9. ¿Por qué necesitamos `<Directory>`?

Cuando se utiliza `Alias`, Apache necesita tener permisos para acceder al directorio correspondiente.

Por ejemplo:

```apache
<Directory /iw/webapps/sisacad>

    Options Indexes FollowSymLinks

    AllowOverride All

    Require all granted

</Directory>
```

La directiva:

```apache
Require all granted
```

permite que Apache entregue los recursos del directorio a los clientes.

Una configuración similar se utilizará para:

```text
/var/www/html
/iw/webapps/sisacad
/iw/webapps/sistradoc
```

---

# 10. Relación entre DocumentRoot, Alias y VirtualHost

Los tres conceptos trabajan conjuntamente.

La configuración principal será:

```apache
<VirtualHost *:8081>

    ServerName localhost

    DocumentRoot /var/www/html

    Alias /sisacad /iw/webapps/sisacad

    Alias /sistradoc /iw/webapps/sistradoc

    <Directory /var/www/html>
        Require all granted
    </Directory>

    <Directory /iw/webapps/sisacad>
        Require all granted
    </Directory>

    <Directory /iw/webapps/sistradoc>
        Require all granted
    </Directory>

</VirtualHost>
```

El funcionamiento será:

```text
                 Apache
                   |
                :8081
                   |
        +----------+----------+
        |          |          |
        v          v          v
       /       /sisacad   /sistradoc
        |          |          |
        v          v          v
/var/www/html /iw/webapps/ /iw/webapps/
               sisacad      sistradoc
        |          |          |
        v          v          v
   index.html index.html  index.html
```

---

# 11. Flujo completo de una solicitud

Cuando el usuario ingresa:

```text
http://localhost:8081/sisacad/
```

ocurre aproximadamente lo siguiente.

## Paso 1 — Navegador

El navegador genera una solicitud:

```text
GET /sisacad/ HTTP/1.1
```

## Paso 2 — Sistema operativo

La solicitud se dirige al puerto:

```text
8081
```

## Paso 3 — Docker

Docker recibe la solicitud en:

```text
HOST:8081
```

y la envía a:

```text
CONTAINER:8081
```

## Paso 4 — Apache

Apache recibe:

```text
/sisacad/
```

y consulta su configuración.

## Paso 5 — Alias

Apache encuentra:

```apache
Alias /sisacad /iw/webapps/sisacad
```

y realiza la asociación:

```text
/sisacad/
    |
    v
/iw/webapps/sisacad/
```

## Paso 6 — Archivo

Apache busca:

```text
/iw/webapps/sisacad/index.html
```

## Paso 7 — Respuesta

Apache devuelve el HTML al navegador.

```text
Apache
   |
   | HTTP Response
   v
Navegador
```

---

# 12. Ejemplo de las tres aplicaciones

Al finalizar el laboratorio tendremos:

```text
                         Apache :8081
                               |
                 +-------------+-------------+
                 |             |             |
                 v             v             v
                /         /sisacad     /sistradoc
                 |             |             |
                 v             v             v
          /var/www/html  /iw/webapps/  /iw/webapps/
                          sisacad       sistradoc
                 |             |             |
                 v             v             v
            index.html    index.html    index.html
```

Las URL serán:

```text
http://localhost:8081/
```

```text
http://localhost:8081/sisacad/
```

```text
http://localhost:8081/sistradoc/
```

---

# 13. Resumen de conceptos

| Concepto | Función |
|---|---|
| **Docker** | Permite ejecutar Apache dentro de un contenedor |
| **Imagen Docker** | Plantilla utilizada para crear contenedores |
| **Contenedor** | Instancia en ejecución de una imagen |
| **Apache HTTP Server** | Servidor que recibe solicitudes HTTP y entrega recursos web |
| **Puerto 8081** | Puerto utilizado por Apache en este laboratorio |
| **DocumentRoot** | Directorio principal desde donde Apache sirve archivos |
| **VirtualHost** | Define la configuración de un sitio o servidor virtual |
| **Alias** | Asocia una URL con un directorio físico |
| **`<Directory>`** | Define reglas de acceso y comportamiento de un directorio |

---

# 14. Comandos esenciales

### Construir una imagen

```bash
docker build -t iw_lab02_image_escobedo .
```

### Crear un contenedor

```bash
docker run -d \
    --name iw_lab02_container_escobedo \
    -p 8081:8081 \
    iw_lab02_image_escobedo
```

### Ver contenedores

```bash
docker ps
```

### Ver imágenes

```bash
docker images
```

### Entrar al contenedor

```bash
docker exec -it iw_lab02_container_escobedo bash
```

### Consultar la configuración de Apache

```bash
apachectl -S
```

### Probar el servidor

```bash
curl http://localhost:8081/
```

### Probar Sistema Académico

```bash
curl http://localhost:8081/sisacad/
```

### Probar Trámite Documentario

```bash
curl http://localhost:8081/sistradoc/
```

---

# 15. Arquitectura conceptual

```text
                         NAVEGADOR
                             |
                             |
                     localhost:8081
                             |
                             v
                  +-------------------+
                  |      DOCKER       |
                  |                   |
                  |    CONTENEDOR     |
                  |                   |
                  | Apache HTTP Server|
                  |       :8081       |
                  +---------+---------+
                            |
                     VirtualHost
                         *:8081
                            |
             +--------------+--------------+
             |              |              |
             v              v              v
            /          /sisacad       /sistradoc
             |              |              |
             v              v              v
      /var/www/html  /iw/webapps/    /iw/webapps/
                     sisacad         sistradoc
             |              |              |
             v              v              v
        index.html     index.html     index.html
```

## Idea fundamental

El laboratorio combina cuatro niveles:

```text
Docker
   ↓
Contenedor
   ↓
Apache
   ↓
VirtualHost + DocumentRoot + Alias
   ↓
Aplicaciones web
```

Cada nivel cumple una función diferente:

- **Docker** proporciona el entorno de ejecución.
- **El contenedor** contiene Apache y los archivos de las aplicaciones.
- **Apache** atiende las solicitudes HTTP.
- **VirtualHost** define la configuración del servidor.
- **DocumentRoot** define el directorio web principal.
- **Alias** permite publicar otros directorios mediante rutas URL.
- **`<Directory>`** controla el acceso a los directorios publicados.
