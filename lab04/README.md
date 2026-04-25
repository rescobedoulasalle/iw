# Laboratorio 04 : Django Admin
| Autores | Rol | Porcentaje |
| :--- | :--- | :---: |
| Richart Escobedo | Prueba de herramientas para evaluar accesibilidad | 100% |
| Richart Escobedo | Elaboración del informe | 100% |
| | **Total** | **100%** |

| Entregables | URL |
| :--- | :--- |
| Repositorio | https://github.com/rescobedoulasalle/iw.git |
| Laboratorio | https://github.com/rescobedoulasalle/iw/tree/main/lab06 |
| Informe | https://github.com/rescobedoulasalle/iw/blob/main/lab06/IW_lab06_django_admin.pdf |

# Descripción de la práctica
- Mostrar el modelo de datos resumido para su proyecto final. (Recomendación: 4-7 tablas)
- Utilizar un entorno virtual para el proyecto de Django en Python. (Crear y enviar requirements.txt)
- Crear un proyecto Django y una aplicación con las siglas del proyecto. (Ejemplo: para un sistema académico podría llamarse **sisacad**)
- Crear modelos en archivos independientes.
- Redefinir el método **def save()** de los modelos para realizar operaciones previas de guardado de registro.
- Redefinir el método **def __str__()** para seleccionar atributos específicos de los registros existentes.
- Crear las funciones necesarias para aplicar restricciones desde el Modelo. (Ejemplo: **validators=[validate_even])**)
- Capturar capturas de pantalla de los auto CRUDs generados por Django Admin. (Explique todo el proceso. Ejemplo: Crear profesor, crear curso, asignar curso a un profesor, ...)
- Elaborar README.md.
  
# Entregables
- Informe de práctica en formato PDF (enviar en la tarea de Classroom). [IW_lab06_django_admin.pdf]
- Repositorio de GitHub que contenga los archivos, anexos e imágenes de su investigación.

# Recomendaciones
- Las tablas deben tener nomenclatura en inglés, con el nombre de la tabla en plural y en camelcase, y todas deben incluir los atributos id, status, created, modified, created_id y modified_id.
- Los atributos de relaciones deben tener el nombre de la tabla principal seguido del '_id'
- Las tablas producto de relaciones N:M deben estar ordenadas alfabéticamente. (Ejemplo: students_courses)

- **Ejemplo para la tabla llamada estudiantes:**
  
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
| user_id |
| **status** |
| **created** |
| **modified** |
| **created_id** |
| **modified_id** |

## Rúbrica de calificación[^1]
| ítem | Descripción | Puntaje |
| :--- | :--- | :---: |
| **Entorno Virtual** | Uso correcto del entorno virtual en proyectos de Python. | 2 |
| **Step 2: Step Django Admin** | Detalla los pasos para crear el administrador de Django a partir de los modelos. | 3 |
| **Restricciones** | Crear restricciones de forma asertiva a partir de los modelos de Django. | 3 |
| **Modelo DER** | Utiliza una herramienta para crear el modelo entidad-relación en Django. | 3 |
| **BD** | Envía la base de datos con los registros existentes para su revisión. | 3 |
| **Modelos** | Realiza las configuraciones necesarias en los modelos para cumplir con los estándares y obtener las funcionalidades solicitadas. | 3 |
| **Informe** | El laboratorio tiene un README.md que detalla toda la práctica. | 3 |
| **Prueba[^2]** | Se tomaron en cuenta todas las consideraciones y recomendaciones, lo que evidencia un trabajo en equipo. | -0 |
|  | **Total** | **20** |

Si el docente solicita un video, debe cargarse en Youtube o Drive y sólo debe entregarse la URL pública, sin que se solicite login alguno. Es recomendable incluir la URL tanto en el README.md como en el informe.

[^1]: La autocalificación es obligatoria.
[^2]: El docente debe comprobar el cumplimiento de todas las consideraciones y recomendaciones, evidenciando el trabajo en equipo con responsabilidad y la práctica de la ética profesional, a fin de no aplicar ninguna penalidad.

## Referencias
- https://developer.mozilla.org/es/docs/Learn_web_development/Extensions/Server-side/Django/Models
- https://www.w3schools.com/django/django_models.php
- https://docs.djangoproject.com/en/6.0/topics/db/models/
- https://docs.djangoproject.com/en/6.0/ref/models/instances/#validating-objects
- https://www.wplogout.com/export-database-diagrams-erd-from-django/
- https://github.com/richarteq/django-enrollments
