LABORATORIO DE INGENIERÍA WEB
Desarrollo de aplicaciones CRUD con Angular, Vue.js y React

Asignatura: Ingeniería Web
Modalidad: Trabajo práctico grupal
Tipo de laboratorio: Desarrollo comparativo de aplicaciones frontend
Nivel: Universitario
Tecnologías: Angular, Vue.js, React, Axios, Angular Router, Vue Router, React Router, Supabase y Neon.

1. Introducción

El presente laboratorio tiene como finalidad desarrollar competencias prácticas en la construcción de aplicaciones web modernas, utilizando diferentes frameworks frontend y mecanismos de comunicación HTTP para consumir servicios y gestionar información almacenada en una base de datos.

Los estudiantes desarrollarán una misma aplicación web CRUD (Create, Read, Update, Delete) utilizando tres frameworks:

Angular.
Vue.js.
React.

Cada grupo deberá implementar el mismo sistema en los tres frameworks, manteniendo los mismos requerimientos funcionales, estructura de datos y operaciones.

El laboratorio permitirá comprender las diferencias entre los frameworks, sus arquitecturas, mecanismos de navegación, gestión de componentes y consumo de servicios REST.

2. Objetivos
2.1. Objetivo general

Desarrollar aplicaciones web frontend utilizando Angular, Vue.js y React, implementando rutas personalizadas, consumo de servicios HTTP y operaciones CRUD conectadas a una base de datos PostgreSQL mediante Supabase o Neon.

2.2. Objetivos específicos
Instalar y configurar los entornos de desarrollo de Angular, Vue.js y React.
Crear proyectos desde cero utilizando las herramientas oficiales de cada framework.
Comprender la arquitectura y organización de directorios de cada proyecto.
Implementar rutas personalizadas para navegar entre diferentes vistas.
Comprender el funcionamiento de los métodos HTTP GET, POST, PUT y DELETE.
Utilizar Axios y HttpClient para consumir servicios REST.
Implementar componentes reutilizables.
Separar las responsabilidades entre componentes, páginas, servicios y modelos.
Configurar la conexión con Supabase o Neon.
Implementar formularios para registrar, consultar, modificar y eliminar información.
Aplicar estándares de nomenclatura, organización y buenas prácticas de programación.
Comparar las características y diferencias entre los tres frameworks.
3. Descripción del proyecto

Cada grupo desarrollará un pequeño sistema denominado:

Sistema de Gestión de Productos (Product Management System).

El sistema permitirá administrar un catálogo de productos mediante una interfaz web.

3.1. Funcionalidades

La aplicación deberá permitir:

Código	Funcionalidad	Método HTTP
RF01	Listar todos los productos	GET
RF02	Consultar un producto por su identificador	GET
RF03	Registrar un nuevo producto	POST
RF04	Actualizar un producto existente	PUT
RF05	Eliminar un producto	DELETE
3.2. Datos del producto

La entidad producto tendrá los siguientes atributos:

Campo	Tipo	Descripción
id	BIGINT	Identificador autogenerado
nombre	VARCHAR(120)	Nombre del producto
descripcion	TEXT	Descripción del producto
precio	DECIMAL(10,2)	Precio del producto
stock	INTEGER	Cantidad disponible
categoria	VARCHAR(80)	Categoría del producto
created_at	TIMESTAMP	Fecha de creación
3.3. Interfaz del sistema

El sistema deberá contar con las siguientes pantallas:

Pantalla	URL propuesta	Descripción
Inicio	/	Página principal
Listado	/productos	Visualización de productos
Nuevo producto	/productos/nuevo	Formulario de registro
Editar producto	/productos/editar/:id	Formulario de actualización
Detalle	/productos/:id	Información de un producto
No encontrado	/404	Página de error 404

Importante: Las rutas serán implementadas mediante el sistema de enrutamiento de cada framework. No se deberán crear enlaces que recarguen innecesariamente toda la aplicación.

4. Arquitectura general del proyecto

Los tres proyectos deberán implementar una arquitectura organizada por responsabilidades.

4.1. Arquitectura propuesta
text
                 USUARIO
                    |
                    v
             APLICACIÓN WEB
                    |
                    v
             SISTEMA DE RUTAS
                    |
                    v
              COMPONENTES
                    |
                    v
             SERVICIOS HTTP
                    |
                    v
              API / CLIENTE
                    |
                    v
             BASE DE DATOS
                    |
                    v
               POSTGRESQL


La arquitectura contempla las siguientes responsabilidades:

Capa	Responsabilidad
Views / Pages	Representar las pantallas de la aplicación
Components	Construir elementos visuales reutilizables
Router	Administrar las URL y la navegación
Services	Centralizar las operaciones de acceso a datos
Models / Types	Definir la estructura de los datos
Config	Administrar las configuraciones del proyecto
Database / API	Gestionar el acceso a la información
4.2. Explicación de los conceptos

Framework: conjunto de herramientas y convenciones que facilita el desarrollo de aplicaciones.

Componente: unidad reutilizable que contiene una parte de la interfaz.

Ruta (Route): dirección URL que permite acceder a una vista determinada.

Router: mecanismo que interpreta las URL y determina qué componente debe visualizarse.

Servicio (Service): módulo encargado de realizar operaciones de comunicación con una API o fuente de datos.

HTTP Client: herramienta utilizada para realizar solicitudes HTTP.

Modelo (Model): definición de la estructura de información que utilizará la aplicación.

CRUD: conjunto de operaciones para crear, consultar, actualizar y eliminar registros.

5. Fundamentos de HTTP y consumo de servicios

Antes de desarrollar los proyectos, los estudiantes deberán comprender los principales métodos HTTP.

5.1. Método GET

Se utiliza para consultar información.

Ejemplo:

http
GET /api/productos


Respuesta esperada:

json
[
  {
    "id": 1,
    "nombre": "Laptop",
    "descripcion": "Laptop para desarrollo",
    "precio": 2500.00,
    "stock": 10,
    "categoria": "Tecnología"
  }
]

5.2. Método POST

Se utiliza para registrar información.

http
POST /api/productos
Content-Type: application/json


Cuerpo de la solicitud:

json
{
  "nombre": "Teclado mecánico",
  "descripcion": "Teclado para programación",
  "precio": 180.00,
  "stock": 15,
  "categoria": "Accesorios"
}

5.3. Método PUT

Se utiliza para actualizar un registro existente.

http
PUT /api/productos/1
Content-Type: application/json


Cuerpo de la solicitud:

json
{
  "nombre": "Laptop profesional",
  "descripcion": "Laptop actualizada",
  "precio": 3200.00,
  "stock": 8,
  "categoria": "Tecnología"
}

5.4. Método DELETE

Se utiliza para eliminar un registro.

http
DELETE /api/productos/1


Respuesta esperada:

json
{
  "mensaje": "Producto eliminado correctamente"
}

5.5. Códigos de respuesta HTTP

Los estudiantes deberán reconocer los siguientes códigos:

Código	Significado
200	Operación exitosa
201	Recurso creado
204	Operación exitosa sin contenido de respuesta
400	Solicitud incorrecta
401	No autorizado
403	Acceso prohibido
404	Recurso no encontrado
500	Error interno del servidor
6. Estándares de programación y nomenclatura

Todos los grupos deberán aplicar convenciones comunes.

Elemento	Convención	Ejemplo
Componentes	PascalCase	ProductList
Archivos de componentes	Según framework	ProductList.vue
Variables	camelCase	productName
Funciones	camelCase	getProducts()
Constantes	UPPER_SNAKE_CASE	API_BASE_URL
Interfaces	PascalCase	Product
Servicios	Nombre descriptivo	productService
Rutas	minúsculas y kebab-case	/productos/nuevo
Directorios	minúsculas	services
Base de datos	snake_case	created_at
6.1. Buenas prácticas obligatorias
No colocar toda la lógica de la aplicación en un único componente.
Separar la lógica de comunicación HTTP de la interfaz.
Utilizar componentes reutilizables.
Evitar duplicar código.
Implementar validaciones de formularios.
Gestionar los errores de comunicación.
Mostrar mensajes de confirmación al usuario.
Utilizar variables de entorno para las configuraciones.
Mantener una estructura organizada de directorios.
Utilizar Git para controlar las versiones del proyecto.
No almacenar contraseñas ni claves secretas en el frontend.
Documentar las funciones principales del proyecto.
