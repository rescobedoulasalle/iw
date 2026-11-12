#  Investigación y Exposición: OWASP Top 10

## 1. Introducción

El objetivo de esta actividad es investigar, comprender y analizar las principales vulnerabilidades de seguridad que afectan a las aplicaciones web, tomando como referencia el estándar **OWASP Top 10:2025**.

Los estudiantes deberán investigar cada una de las diez categorías de vulnerabilidades, comprender cómo se producen los ataques, identificar antecedentes históricos, analizar sus mecanismos de mitigación y relacionar estas vulnerabilidades con las tecnologías que estamos estudiando durante el curso.

Las tecnologías que deberán considerar son:

- **Django:** Framework de desarrollo web con Python.
- **Node.js:** Entorno de ejecución de JavaScript.
- **Spring Boot:** Framework de desarrollo de aplicaciones con Java.
- **Angular:** Framework de desarrollo frontend.
- **Vue.js:** Framework progresivo de JavaScript.
- **React:** Biblioteca de JavaScript para interfaces de usuario.

La finalidad no es solamente conocer las vulnerabilidades desde una perspectiva teórica, sino comprender cómo pueden presentarse en proyectos reales y qué mecanismos ofrecen las tecnologías estudiadas para prevenirlas.

## 2. Objetivos

### Objetivo general

Analizar las diez principales categorías de riesgos de seguridad en aplicaciones web propuestas por OWASP, identificando sus características, antecedentes históricos, mecanismos de explotación, estrategias de mitigación y relación con las tecnologías de desarrollo estudiadas.

### Objetivos específicos

- Comprender el concepto y funcionamiento de cada vulnerabilidad.
- Investigar antecedentes históricos y ataques documentados.
- Identificar cómo se ejecutan los ataques y cuáles son sus consecuencias.
- Conocer las estrategias y buenas prácticas para mitigar cada vulnerabilidad.
- Investigar publicaciones científicas relacionadas con cada categoría.
- Analizar cómo se manifiestan estas vulnerabilidades en Django, Node.js, Spring Boot, Angular, Vue.js y React.
- Identificar herramientas y mecanismos de seguridad disponibles en cada tecnología.

## 3. OWASP Top 10:2025

Cada grupo deberá investigar y exponer las siguientes diez categorías:

| Código | Vulnerabilidad |
|---|---|
| A01:2025 | Broken Access Control (Pérdida de control de acceso) |
| A02:2025 | Security Misconfiguration (Configuración de seguridad incorrecta) |
| A03:2025 | Software Supply Chain Failures (Fallos en la cadena de suministro de software) |
| A04:2025 | Cryptographic Failures (Fallos criptográficos) |
| A05:2025 | Injection (Inyección) |
| A06:2025 | Insecure Design (Diseño inseguro) |
| A07:2025 | Authentication Failures (Fallos de autenticación) |
| A08:2025 | Software or Data Integrity Failures (Fallos en la integridad del software o de los datos) |
| A09:2025 | Security Logging and Alerting Failures (Fallos en el registro y alertas de seguridad) |
| A10:2025 | Mishandling of Exceptional Conditions (Manejo inadecuado de condiciones excepcionales) |

Referencia oficial: https://top10.owasp.org/2025/es/

---

## 4. Actividades obligatorias de investigación

Para cada vulnerabilidad del OWASP Top 10, los estudiantes deberán desarrollar los siguientes puntos:

### 4.1. Definición de la vulnerabilidad

Explicar:

- ¿Qué es la vulnerabilidad?
- ¿En qué consiste?
- ¿Cuáles son sus principales características?
- ¿Qué condiciones permiten que se presente?
- ¿Qué información, recursos o funcionalidades pueden verse comprometidos?
- ¿Cuál es su impacto en la confidencialidad, integridad y disponibilidad de la información?

### 4.2. Antecedentes históricos: primer ataque documentado

Investigar los antecedentes históricos de la vulnerabilidad.

Responder:

- ¿Cuándo se identificó o documentó por primera vez?
- ¿Cuál es el primer ataque o incidente conocido relacionado con esta vulnerabilidad?
- ¿Qué organización, sistema o aplicación fue afectada?
- ¿Quién o qué tipo de atacante estuvo involucrado, si se conoce?
- ¿Cómo se produjo el ataque?
- ¿Qué consecuencias tuvo?
- ¿Qué cambios produjo en la industria del desarrollo de software o en la seguridad informática?

**Importante:** Si no existe evidencia verificable de cuál fue el primer ataque, deberán presentar el caso histórico más antiguo que encuentren documentado, indicando la fuente y evitando afirmar que fue el primero de la historia.

### 4.3. ¿Cómo funciona el ataque?

Explicar técnicamente el funcionamiento de la vulnerabilidad.

Deberán presentar:

- Descripción del escenario de ataque.
- Condiciones necesarias para explotar la vulnerabilidad.
- Secuencia de ejecución del ataque.
- Componentes de la aplicación involucrados.
- Ejemplo práctico o demostración controlada.
- Consecuencias que podría ocasionar en un sistema real.

Se recomienda utilizar diagramas, capturas de pantalla, fragmentos de código o demostraciones en un entorno de laboratorio.

### 4.4. ¿Cómo se mitiga la vulnerabilidad?

Investigar las medidas que permiten prevenir, detectar y corregir la vulnerabilidad.

Explicar:

- ¿Qué prácticas de programación segura se deben implementar?
- ¿Qué configuraciones permiten reducir el riesgo?
- ¿Qué herramientas pueden ayudar a detectar el problema?
- ¿Qué mecanismos de protección ofrecen los frameworks estudiados?
- ¿Cómo se puede comprobar que la vulnerabilidad fue corregida?

La mitigación debe explicarse tanto desde una perspectiva general como desde una perspectiva técnica.

### 4.5. Investigación de un artículo científico

Cada grupo deberá localizar y analizar **al menos un artículo científico** relacionado directamente con la vulnerabilidad asignada.

El artículo debe proceder preferentemente de una revista científica, conferencia académica o publicación indexada.

Se recomienda buscar en:

- Google Scholar: https://scholar.google.com/
- IEEE Xplore: https://ieeexplore.ieee.org/
- ACM Digital Library: https://dl.acm.org/
- ScienceDirect: https://www.sciencedirect.com/
- SpringerLink: https://link.springer.com/
- Scopus: https://www.scopus.com/

Deberán presentar:

1. Título del artículo.
2. Autores.
3. Año de publicación.
4. Revista o conferencia donde fue publicado.
5. DOI o enlace de acceso.
6. Problema de investigación.
7. Metodología utilizada.
8. Principales resultados y conclusiones.
9. ¿Qué aporta el artículo a la comprensión o mitigación de la vulnerabilidad?

**Importante:** No se aceptarán como artículo científico publicaciones de blogs, tutoriales, páginas comerciales o artículos de opinión. Estos recursos pueden utilizarse como material complementario, pero no sustituyen la publicación académica.

### 4.6. Antecedentes y aplicación en las tecnologías estudiadas

Este apartado es especialmente importante.

Los estudiantes deberán investigar cómo se presenta la vulnerabilidad en cada una de las tecnologías estudiadas durante el curso.

Se analizarán las siguientes:

| Tecnología | Aspectos que deben investigar |
|---|---|
| Django | Mecanismos de seguridad, configuraciones, middleware, ORM, autenticación y protección de aplicaciones. |
| Node.js | Seguridad de dependencias, Express, validación de datos, autenticación, gestión de sesiones y APIs. |
| Spring Boot | Spring Security, control de acceso, autenticación, autorización, configuración y protección de APIs. |
| Angular | Seguridad del frontend, sanitización, XSS, gestión de tokens y comunicación con APIs. |
| Vue.js | Seguridad de componentes, renderizado, sanitización, gestión de sesiones y comunicación con APIs. |
| React | Seguridad del renderizado, XSS, manejo de datos, dependencias y autenticación. |

Para cada tecnología deberán responder:

- ¿Cómo puede presentarse esta vulnerabilidad?
- ¿Existe algún antecedente, CVE o caso documentado relacionado con la tecnología?
- ¿Qué funcionalidades o componentes pueden verse afectados?
- ¿Qué mecanismos de protección proporciona la tecnología?
- ¿Qué configuraciones o prácticas de desarrollo seguro se deben implementar?
- ¿Qué limitaciones tiene el framework o biblioteca frente a esta vulnerabilidad?

**Consideración:** No todas las vulnerabilidades afectan de la misma manera al frontend y al backend. Cuando una categoría no sea directamente aplicable a una tecnología, deberán explicar por qué y analizar su relación indirecta con el ecosistema.

---

## 5. Demostración práctica

Cada grupo deberá desarrollar una demostración práctica de la vulnerabilidad asignada.

La demostración debe incluir:

1. Un escenario de aplicación web vulnerable.
2. Identificación de la debilidad de seguridad.
3. Explicación del procedimiento de explotación en un entorno controlado.
4. Evidencia del resultado obtenido.
5. Aplicación de una medida de mitigación.
6. Nueva prueba que demuestre que la vulnerabilidad fue corregida.

La demostración deberá realizarse en un entorno propio de laboratorio, con aplicaciones de prueba y datos ficticios. No se permite atacar sistemas de terceros ni utilizar información real de usuarios.

Se valorará especialmente que los estudiantes implementen ejemplos utilizando alguna de las tecnologías estudiadas.

---

## 6. Estructura obligatoria de la exposición

Cada grupo deberá organizar su presentación de la siguiente manera:

| N.º | Contenido | Descripción |
|---|---|---|
| 1 | Introducción | Presentación de la vulnerabilidad. |
| 2 | Definición | Concepto y características técnicas. |
| 3 | Antecedentes históricos | Primer ataque documentado o caso histórico conocido. |
| 4 | Funcionamiento | Explicación técnica de cómo se produce el ataque. |
| 5 | Impacto | Consecuencias para usuarios y organizaciones. |
| 6 | Mitigación | Estrategias de prevención y corrección. |
| 7 | Artículo científico | Análisis de una publicación académica. |
| 8 | Django | Análisis de la vulnerabilidad en Django. |
| 9 | Node.js | Análisis de la vulnerabilidad en Node.js. |
| 10 | Spring Boot | Análisis de la vulnerabilidad en Spring Boot. |
| 11 | Angular | Análisis de la vulnerabilidad en Angular. |
| 12 | Vue.js | Análisis de la vulnerabilidad en Vue.js. |
| 13 | React | Análisis de la vulnerabilidad en React. |
| 14 | Demostración | Ejemplo práctico de explotación y mitigación. |
| 15 | Conclusiones | Aprendizajes y recomendaciones. |
| 16 | Referencias | Fuentes bibliográficas y documentación consultada. |

---

## 7. Entregables

Cada grupo deberá presentar:

- [ ] Presentación de diapositivas.
- [ ] Investigación documental de la vulnerabilidad.
- [ ] Antecedentes históricos y caso documentado.
- [ ] Análisis de al menos un artículo científico.
- [ ] Análisis comparativo de las seis tecnologías.
- [ ] Demostración práctica.
- [ ] Evidencias de la vulnerabilidad y su mitigación.
- [ ] Referencias bibliográficas.

Los archivos de código de la demostración deberán estar organizados en un repositorio Git y acompañados de instrucciones para reproducir el laboratorio.

## 8. Criterios de evaluación

| Criterio | Porcentaje |
|---|---:|
| Definición y comprensión de la vulnerabilidad | 10 % |
| Antecedentes históricos y ataque documentado | 10 % |
| Explicación técnica del funcionamiento del ataque | 15 % |
| Estrategias de mitigación | 15 % |
| Investigación y análisis del artículo científico | 15 % |
| Relación con Django, Node.js, Spring Boot, Angular, Vue.js y React | 15 % |
| Demostración práctica y evidencias | 15 % |
| Calidad de la exposición y conclusiones | 5 % |
| **Total** | **100 %** |

## 9. Recomendaciones para la investigación

- Utilizar documentación oficial de OWASP.
- Consultar fuentes académicas y publicaciones científicas.
- Incorporar referencias bibliográficas verificables.
- Utilizar ejemplos técnicos que permitan comprender el funcionamiento de las vulnerabilidades.
- No limitarse a copiar definiciones: se espera análisis y comprensión.
- Comparar las estrategias de seguridad de las tecnologías estudiadas.
- Justificar técnicamente las recomendaciones de mitigación.
- Utilizar diagramas y ejemplos para facilitar la comprensión.
- Citar correctamente las fuentes utilizadas.

## 10. Referencias principales

- OWASP Top 10:2025: https://top10.owasp.org/2025/es/
- OWASP Foundation: https://owasp.org/
- OWASP Cheat Sheet Series: https://cheatsheetseries.owasp.org/
- Common Weakness Enumeration (CWE): https://cwe.mitre.org/
- Common Vulnerabilities and Exposures (CVE): https://www.cve.org/
- National Vulnerability Database (NVD): https://nvd.nist.gov/
- Google Scholar: https://scholar.google.com/

---

## 11. Consideración final

El propósito de esta actividad es que los estudiantes comprendan que la seguridad informática no es una característica adicional que se incorpora al finalizar un proyecto, sino una responsabilidad que debe considerarse durante todo el ciclo de vida del desarrollo de software.

Cada grupo deberá demostrar que comprende la vulnerabilidad asignada, que puede explicar cómo se produce, que conoce sus antecedentes, que identifica cómo puede afectar a las tecnologías estudiadas y que es capaz de proponer e implementar mecanismos para mitigarla.

**La exposición debe demostrar investigación, análisis crítico y aplicación práctica, no solamente conocimiento teórico.**
