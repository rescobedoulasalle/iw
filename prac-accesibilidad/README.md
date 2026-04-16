# Práctica : Accesibilidad web
| Autores | Rol | Porcentaje |
| :--- | :--- | :---: |
| Richart Escobedo | Revisor y elaboración de toda la práctica. | 100% |

| Entregables | URL |
| :--- | :--- |
| Repositorio | https://github.com/rescobedoulasalle/iw.git |
| Laboratorio | https://github.com/rescobedoulasalle/iw/prac-accesibilidad |
| Informe | https://github.com/rescobedoulasalle/iw/prac-accesibilidad/IW_prac_accesibilidad.pdf |

# Descripción de la práctica
- Utilizar la herramienta [TAW](https://www.tawdis.net/) o similares para evaluar la accesibilidad web (Perceptible, Operable, Comprensible, Robusto).
- Utilizar la herramienta [Contrast Checker](https://webaim.org/resources/contrastchecker/) para realizar una prueba de contraste de color (para personas con baja visión y daltonismo).
- Desactivar JavaScript y probar la navegación y la funcionalidad.
- Probar la navegación sólo con el teclado (enlaces, botones, formularios). [Foco][Orden]
- Probar el acceso desde pantallas de dispositivos móviles (omisión de elementos del DOM).
- Realizar el análisis, detallar y proponer la corrección de errores (agregar anexos).

# Entregables
- Informe de práctica en formato Markdown y PDF (enviar en la tarea de Classroom). [IW_prac_accesibilidad.pdf]
- Repositorio de GitHub que contenga los archivos anexos de su investigación.

## Crear PDF a partir del README.md
```bash
pandoc README.md -o DAW_lab01.pdf
```

## Referencias
- [TAW](https://www.tawdis.net/)
- [Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Herramientas automáticas para evaluar y mejorar la accesibilidad web
](https://www.youtube.com/watch?v=Xxleh0L55_o&t=340s)
- [Ejercicio del curso: análisis de la accesibilidad web con WAVE y de forma manual
](https://www.youtube.com/watch?v=7_5uN9gh-tU&t=616s)
- [Evaluación de la accesibilidad. Cuando los test automáticos son insuficientes
](https://www.youtube.com/watch?v=msJI4Z5Ra0E&t=457s)
- [Markup Validation Service](https://validator.w3.org/)
- [CSS Validation Service](https://jigsaw.w3.org/css-validator/)
- [Mobile Checker Report](https://www.w3.org/2016/11/mobile-checker-disabled/)
- [Link Checker](https://validator.w3.org/checklink)
- [Validator and tools](https://www.w3.org/developers/tools/)


## Pantallas
![image](sitio1.png)
![image](sitio2.png)

## Rúbrica de calificación
| ítem | Descripción | Puntaje |
| :--- | :--- | :---: |
| Informe | El informe está completo, utiliza la plantilla y tiene un acabado impecable. | 5 |
| Video | El video es preciso y muestra la ejecución del contenedor en la terminal y la navegación por la aplicación web. | 2 |
| GitHub | El repositorio contiene todos los archivos necesarios para el despliegue y muestra un orden y un manejo acordes con los estándares de codificación. | 10 |
| README | El laboratorio tiene un README.md  necesario para desplegar la aplicación web. | 3 |
| Prueba[^2] | Se tomaron en cuenta todas las consideraciones y recomendaciones, lo que evidencia un trabajo en equipo. | -0 |

[^1]: Un video debe cargarse en Youtube o Drive y sólo debe entregarse la URL pública, sin que se solicite login alguno. Es recomendable incluir la URL tanto en el README.md como en el informe.
[^2]: El docente debe comprobar el cumplimiento de todas las consideraciones y recomendaciones, evidenciando el trabajo en equipo con responsabilidad y la práctica de la ética profesional, a fin de no aplicar ninguna penalidad.
