# Laboratorio : Django Admin
| Autores | Rol | Porcentaje |
| :--- | :--- | :---: |
| Richart Escobedo | Prueba de herramientas para evaluar accesibilidad | 100% |
| Richart Escobedo | Elaboración del informe | 100% |
| | **Total** | **100%** |

| Entregables | URL |
| :--- | :--- |
| Repositorio | https://github.com/rescobedoulasalle/iw.git |
| Laboratorio | https://github.com/rescobedoulasalle/iw/tree/main/lab04 |
| Informe | https://github.com/rescobedoulasalle/iw/blob/main/prac-accesibilidad/IW_lab04_django_admin.pdf |

# Descripción de la práctica
- Mostrar el modelo de datos resumido para su proyecto final.
- Crear virtual enviroment para un proyecto Python.
- Crear un proyecto Django y una aplicación (Utilizar siglas para su proyecto).
- Crear Modelos e interactuar con la base de datos.
- Redefinir el método **def save()** de los modelos para operaciones previas para guardar un registro.
- Redifinir el método **def __str__()** que muestra determinados atributos de los registros existentes.
- Crear las funciones necesarias para lanzar restricciones desde el Modelo (ejemplo: **validators=[validate_even])**).
- Capturar pantallas de los auto CRUDs generados por Django Admin.
- Elaborar README.md.
  
# Entregables
- Informe de práctica en formato Markdown y PDF (enviar en la tarea de Classroom). [IW_lab04_django_admin.pdf]
- Repositorio de GitHub que contenga los archivos, anexos e imágenes de su investigación.

# Recomendaciones
- La tablas deben estar en nomenclatura en inglés, nombre de tabla en plural, camelcase y todas deben tener los atributos id, status, created, modified, created_id, modified_id.
- Los atributos de relaciones deben tener el nombre de la tabla principal seguido del '_id'
- Las tablas producto de relaciones N:M deben estar ordenadas alfabeticamente (ejemplo: students_courses).

- **Ejemplo para una tabla llamada students:**
  
| **students** |
| :--- |
| **id** |
| names |
| fatherSurname |
| motherSurname |
| gender |
| address |
| phone |
| note |
| type_id |
| **status** |
| **created** |
| **modified** |
| **created_id** |
| **modified_id** |

## Rúbrica de calificación[^1]
| ítem | Descripción | Puntaje |
| :--- | :--- | :---: |
| **venv** | Uso de venv, envío de requirements.txt | 2 |
| **Step2step Django Admin** | Realiza detalladamente los pasos para crear el administrador de modelos mediante Django | 3 |
| **Restricciones** | Crear restricciones desde Modelos en Django. | 3 |
| **Modelo DER** | Utiliza una herramienta para crear el DER desde django | 3 |
| **SQlite** | Envía base de datos con datos existentes. | 3 |
| **Modelo** | Realiza configuraciones necesarias en los Modelos para respetar estándares y obtener funcionalidades solicitadas. | 3 |
| **Informe** | El laboratorio tiene un README.md que detalla toda la práctica | 3 |
| **Prueba[^2]** | Se tomaron en cuenta todas las consideraciones y recomendaciones, lo que evidencia un trabajo en equipo | -0 |
|  | **Total** | **20** |

Si el docente solicita un video, debe cargarse en Youtube o Drive y sólo debe entregarse la URL pública, sin que se solicite login alguno. Es recomendable incluir la URL tanto en el README.md como en el informe.

[^1]: La autocalificación es obligatoria.
[^2]: El docente debe comprobar el cumplimiento de todas las consideraciones y recomendaciones, evidenciando el trabajo en equipo con responsabilidad y la práctica de la ética profesional, a fin de no aplicar ninguna penalidad.

## Referencias
- https://developer.mozilla.org/es/docs/Learn_web_development/Extensions/Server-side/Django/Models
- https://www.w3schools.com/django/django_models.php
- https://docs.djangoproject.com/en/6.0/topics/db/models/
- https://www.wplogout.com/export-database-diagrams-erd-from-django/
