# LABORATORIO: Desarrollo de aplicaciones Front-End con Angular, Vue.js y React

## 1. Información general

| Campo | Descripción |
|---|---|
| Curso | Ingeniería Web |
| Laboratorio | Desarrollo de interfaces con frameworks Front-End |
| Duración | 180 minutos |
| Modalidad | Individual o grupal |
| Frameworks | Angular, Vue.js y React |
| Backend | Node.js + Express |
| API | REST |
| Herramientas | VS Code, Git, Node.js, npm y navegador web |

## 2. Objetivos

Al finalizar el laboratorio, el estudiante será capaz de:

- Instalar y configurar proyectos utilizando Angular, Vue.js y React.
- Identificar las principales características de cada framework.
- Implementar componentes reutilizables.
- Configurar rutas de navegación.
- Consumir servicios REST utilizando HTTP.
- Implementar operaciones CRUD básicas.
- Comparar las arquitecturas y características de los frameworks estudiados.

## 3. Descripción del laboratorio

Se desarrollará una aplicación web denominada **Gestión de Cursos**, que permitirá registrar, listar, actualizar y eliminar cursos.

La aplicación tendrá las siguientes funcionalidades:

- Listar cursos registrados.
- Visualizar el detalle de un curso.
- Registrar nuevos cursos.
- Actualizar cursos existentes.
- Eliminar cursos.
- Navegar entre diferentes vistas mediante rutas.

La misma aplicación será implementada utilizando tres frameworks:

1. Angular.
2. Vue.js.
3. React.

Todos los proyectos consumirán el mismo backend REST.

## 4. Arquitectura de la aplicación

```text
                    BACKEND REST
                  Node.js + Express
                         |
                 API REST /api/cursos
                         |
          +--------------+--------------+
          |              |              |
          v              v              v
      Angular          Vue.js         React
          |              |              |
     HttpClient       Axios          Axios
          |              |              |
     Angular          Vue Router     React Router
      Router
```

### API REST

| Método | Endpoint | Descripción |
|---|---|---|
| GET | /api/cursos | Listar cursos |
| GET | /api/cursos/:id | Obtener curso |
| POST | /api/cursos | Registrar curso |
| PUT | /api/cursos/:id | Actualizar curso |
| DELETE | /api/cursos/:id | Eliminar curso |

## 5. Preparación del entorno

Instalar previamente:

- Node.js LTS.
- npm.
- Visual Studio Code.
- Git.
- Navegador web.

Verificar la instalación:

```bash
node --version
npm --version
git --version
```

Crear un directorio para el laboratorio:

```bash
mkdir lab-frontend-frameworks
cd lab-frontend-frameworks
```

## 6. Backend común: API REST con Express

### 6.1 Crear el proyecto

```bash
mkdir backend
cd backend

npm init -y

npm install express cors

npm install -D nodemon
```

Crear el archivo `server.js`.

### 6.2 Implementar la API REST

```javascript
const express = require("express");
const cors = require("cors");

const app = express();

app.use(cors());
app.use(express.json());

let cursos = [
    { id: 1, nombre: "Ingeniería Web", creditos: 4 },
    { id: 2, nombre: "Programación I", creditos: 5 },
    { id: 3, nombre: "Base de Datos", creditos: 4 }
];

let siguienteId = 4;

// Listar cursos
app.get("/api/cursos", (req, res) => {
    res.json(cursos);
});

// Obtener curso
app.get("/api/cursos/:id", (req, res) => {
    const curso = cursos.find(
        c => c.id === Number(req.params.id)
    );

    if (!curso) {
        return res.status(404).json({
            mensaje: "Curso no encontrado"
        });
    }

    res.json(curso);
});

// Registrar curso
app.post("/api/cursos", (req, res) => {
    const { nombre, creditos } = req.body;

    if (!nombre || creditos == null) {
        return res.status(400).json({
            mensaje: "Nombre y créditos son obligatorios"
        });
    }

    const curso = {
        id: siguienteId++,
        nombre,
        creditos: Number(creditos)
    };

    cursos.push(curso);

    res.status(201).json(curso);
});

// Actualizar curso
app.put("/api/cursos/:id", (req, res) => {
    const id = Number(req.params.id);

    const curso = cursos.find(c => c.id === id);

    if (!curso) {
        return res.status(404).json({
            mensaje: "Curso no encontrado"
        });
    }

    curso.nombre = req.body.nombre;
    curso.creditos = Number(req.body.creditos);

    res.json(curso);
});

// Eliminar curso
app.delete("/api/cursos/:id", (req, res) => {
    const id = Number(req.params.id);

    const existe = cursos.some(c => c.id === id);

    if (!existe) {
        return res.status(404).json({
            mensaje: "Curso no encontrado"
        });
    }

    cursos = cursos.filter(c => c.id !== id);

    res.json({
        mensaje: "Curso eliminado"
    });
});

app.listen(3000, () => {
    console.log("API disponible en http://localhost:3000");
});
```

### 6.3 Configurar ejecución

Agregar al `package.json`:

```json
"scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
}
```

Ejecutar:

```bash
npm run dev
```

### 6.4 Verificar el backend

Abrir en el navegador:

http://localhost:3000/api/cursos

Resultado esperado:

```json
[
  {
    "id": 1,
    "nombre": "Ingeniería Web",
    "creditos": 4
  },
  {
    "id": 2,
    "nombre": "Programación I",
    "creditos": 5
  },
  {
    "id": 3,
    "nombre": "Base de Datos",
    "creditos": 4
  }
]
```

---

# PARTE I. DESARROLLO CON VUE.JS

## 7. Vue.js: creación del proyecto

Vue.js será implementado utilizando:

- Vue 3.
- Composition API.
- Vue Router.
- Axios.

### 7.1 Crear proyecto

Desde el directorio principal:

```bash
npm create vue@latest frontend-vue
```

Seleccionar las siguientes opciones:

| Opción | Selección |
|---|---|
| TypeScript | No |
| JSX | No |
| Vue Router | Sí |
| Pinia | No |
| Vitest | No |
| ESLint | Sí |
| Prettier | Opcional |

Instalar dependencias:

```bash
cd frontend-vue
npm install
npm install axios
```

## 8. Configurar Axios

Crear `src/services/api.js`.

```javascript
import axios from "axios";

const api = axios.create({
    baseURL: "http://localhost:3000/api",
    headers: {
        "Content-Type": "application/json"
    }
});

export default api;
```

## 9. Configurar Vue Router

El proyecto creado con Vue Router normalmente incluye un archivo `src/router/index.js`.

Configurar las rutas:

```javascript
import { createRouter, createWebHistory } from "vue-router";

import CursosView from "../views/CursosView.vue";
import NuevoCursoView from "../views/NuevoCursoView.vue";

const routes = [
    {
        path: "/",
        component: CursosView
    },
    {
        path: "/nuevo",
        component: NuevoCursoView
    }
];

const router = createRouter({
    history: createWebHistory(),
    routes
});

export default router;
```

## 10. Implementar el listado de cursos

Crear `src/views/CursosView.vue`.

```vue
<script setup>
import { ref, onMounted } from "vue";
import api from "../services/api";

const cursos = ref([]);

async function listarCursos() {
    const response = await api.get("/cursos");
    cursos.value = response.data;
}

async function eliminarCurso(id) {
    if (confirm("¿Eliminar curso?")) {
        await api.delete(`/cursos/${id}`);
        await listarCursos();
    }
}

onMounted(listarCursos);
</script>

<template>
    <h1>Gestión de Cursos</h1>

    <RouterLink to="/nuevo">
        Nuevo Curso
    </RouterLink>

    <table border="1">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Créditos</th>
                <th>Acciones</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="curso in cursos" :key="curso.id">
                <td>{{ curso.id }}</td>
                <td>{{ curso.nombre }}</td>
                <td>{{ curso.creditos }}</td>
                <td>
                    <button @click="eliminarCurso(curso.id)">
                        Eliminar
                    </button>
                </td>
            </tr>
        </tbody>
    </table>
</template>
```

## 11. Implementar registro de cursos

Crear `src/views/NuevoCursoView.vue`.

```vue
<script setup>
import { ref } from "vue";
import api from "../services/api";
import { useRouter } from "vue-router";

const router = useRouter();

const nombre = ref("");
const creditos = ref(4);

async function registrarCurso() {
    await api.post("/cursos", {
        nombre: nombre.value,
        creditos: Number(creditos.value)
    });

    router.push("/");
}
</script>

<template>
    <h1>Nuevo Curso</h1>

    <form @submit.prevent="registrarCurso">
        <label>Nombre:</label>
        <input v-model="nombre" required />

        <br />

        <label>Créditos:</label>
        <input
            type="number"
            v-model="creditos"
            min="1"
            required
        />

        <br />

        <button type="submit">
            Registrar
        </button>

        <RouterLink to="/">
            Cancelar
        </RouterLink>
    </form>
</template>
```

## 12. Ejecutar Vue.js

```bash
npm run dev
```

Abrir la URL mostrada por Vite, normalmente:

http://localhost:5173

### Actividad Vue.js

Implementar:

- Listado de cursos.
- Registro de cursos.
- Eliminación de cursos.
- Navegación entre vistas.
- Consumo de API utilizando Axios.

**Desafío:** implementar la actualización de cursos utilizando `PUT`.

---

# PARTE II. DESARROLLO CON ANGULAR

## 13. Angular: creación del proyecto

Angular utilizará:

- Angular Components.
- Angular Router.
- HttpClient.
- Formularios.

Crear proyecto:

```bash
cd ../

npx @angular/cli@latest frontend-angular
```

Seleccionar configuración con routing y CSS.

Ingresar al proyecto:

```bash
cd frontend-angular
```

## 14. Configurar HttpClient

En la configuración de Angular, habilitar HttpClient.

En `src/app/app.config.ts`:

```typescript
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { provideHttpClient } from '@angular/common/http';

import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),
    provideHttpClient()
  ]
};
```

## 15. Crear servicio de cursos

```bash
ng generate service services/curso
```

Editar `src/app/services/curso.service.ts`.

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class CursoService {

  private api = 'http://localhost:3000/api/cursos';

  constructor(private http: HttpClient) {}

  listar() {
    return this.http.get<any[]>(this.api);
  }

  registrar(curso: any) {
    return this.http.post(this.api, curso);
  }

  actualizar(id: number, curso: any) {
    return this.http.put(`${this.api}/${id}`, curso);
  }

  eliminar(id: number) {
    return this.http.delete(`${this.api}/${id}`);
  }
}
```

## 16. Crear componente de listado

```bash
ng generate component pages/cursos
```

En `src/app/pages/cursos/cursos.component.ts`:

```typescript
import { Component, OnInit } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RouterLink } from '@angular/router';

import { CursoService } from '../../services/curso.service';

@Component({
  selector: 'app-cursos',
  standalone: true,
  imports: [CommonModule, RouterLink],
  templateUrl: './cursos.component.html'
})
export class CursosComponent implements OnInit {

  cursos: any[] = [];

  constructor(private servicio: CursoService) {}

  ngOnInit() {
    this.listar();
  }

  listar() {
    this.servicio.listar().subscribe(data => {
      this.cursos = data;
    });
  }

  eliminar(id: number) {
    this.servicio.eliminar(id).subscribe(() => {
      this.listar();
    });
  }
}
```

En `src/app/pages/cursos/cursos.component.html`:

```html
<h1>Gestión de Cursos</h1>

<a routerLink="/nuevo">
    Nuevo Curso
</a>

<table border="1">
    <thead>
        <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Créditos</th>
            <th>Acciones</th>
        </tr>
    </thead>

    <tbody>
        <tr *ngFor="let curso of cursos">
            <td>{{ curso.id }}</td>
            <td>{{ curso.nombre }}</td>
            <td>{{ curso.creditos }}</td>
            <td>
                <button (click)="eliminar(curso.id)">
                    Eliminar
                </button>
            </td>
        </tr>
    </tbody>
</table>
```

## 17. Configurar Angular Router

Editar `src/app/app.routes.ts`.

```typescript
import { Routes } from '@angular/router';

import { CursosComponent } from './pages/cursos/cursos.component';

export const routes: Routes = [
  {
    path: '',
    component: CursosComponent
  }
];
```

En el componente principal debe existir:

```html
<router-outlet></router-outlet>
```

## 18. Ejecutar Angular

```bash
ng serve
```

Abrir:

http://localhost:4200

### Actividad Angular

Implementar:

- Listado de cursos.
- Registro de cursos.
- Eliminación de cursos.
- Actualización de cursos.
- Navegación con Angular Router.
- Consumo de API REST utilizando HttpClient.

---

# PARTE III. DESARROLLO CON REACT

## 19. React: creación del proyecto

React utilizará:

- React.
- React Router.
- Axios.
- Hooks.
- Componentes funcionales.

Crear proyecto:

```bash
cd ../

npm create vite@latest frontend-react -- --template react
```

Instalar dependencias:

```bash
cd frontend-react

npm install

npm install axios react-router
```

## 20. Configurar Axios

Crear `src/services/api.js`.

```javascript
import axios from "axios";

const api = axios.create({
    baseURL: "http://localhost:3000/api"
});

export default api;
```

## 21. Configurar React Router

Editar `src/main.jsx`.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

import {
    BrowserRouter,
    Routes,
    Route
} from "react-router";

import Cursos from "./pages/Cursos";
import NuevoCurso from "./pages/NuevoCurso";

ReactDOM.createRoot(
    document.getElementById("root")
).render(
    <BrowserRouter>
        <Routes>
            <Route path="/" element={<Cursos />} />
            <Route path="/nuevo" element={<NuevoCurso />} />
        </Routes>
    </BrowserRouter>
);
```

## 22. Implementar listado de cursos

Crear `src/pages/Cursos.jsx`.

```jsx
import { useEffect, useState } from "react";
import { Link } from "react-router";

import api from "../services/api";

export default function Cursos() {

    const [cursos, setCursos] = useState([]);

    async function listar() {
        const response = await api.get("/cursos");
        setCursos(response.data);
    }

    async function eliminar(id) {
        if (confirm("¿Eliminar curso?")) {
            await api.delete(`/cursos/${id}`);
            listar();
        }
    }

    useEffect(() => {
        listar();
    }, []);

    return (
        <>
            <h1>Gestión de Cursos</h1>

            <Link to="/nuevo">
                Nuevo Curso
            </Link>

            <table border="1">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Nombre</th>
                        <th>Créditos</th>
                        <th>Acciones</th>
                    </tr>
                </thead>

                <tbody>
                    {cursos.map(curso => (
                        <tr key={curso.id}>
                            <td>{curso.id}</td>
                            <td>{curso.nombre}</td>
                            <td>{curso.creditos}</td>
                            <td>
                                <button
                                    onClick={() => eliminar(curso.id)}
                                >
                                    Eliminar
                                </button>
                            </td>
                        </tr>
                    ))}
                </tbody>
            </table>
        </>
    );
}
```

## 23. Implementar registro de cursos

Crear `src/pages/NuevoCurso.jsx`.

```jsx
import { useState } from "react";
import { useNavigate, Link } from "react-router";

import api from "../services/api";

export default function NuevoCurso() {

    const navigate = useNavigate();

    const [nombre, setNombre] = useState("");
    const [creditos, setCreditos] = useState(4);

    async function registrar(e) {
        e.preventDefault();

        await api.post("/cursos", {
            nombre,
            creditos: Number(creditos)
        });

        navigate("/");
    }

    return (
        <>
            <h1>Nuevo Curso</h1>

            <form onSubmit={registrar}>
                <label>Nombre:</label>

                <input
                    value={nombre}
                    onChange={e => setNombre(e.target.value)}
                    required
                />

                <br />

                <label>Créditos:</label>

                <input
                    type="number"
                    value={creditos}
                    onChange={e => setCreditos(e.target.value)}
                    min="1"
                    required
                />

                <br />

                <button type="submit">
                    Registrar
                </button>

                <Link to="/">
                    Cancelar
                </Link>
            </form>
        </>
    );
}
```

## 24. Ejecutar React

```bash
npm run dev
```

Abrir:

http://localhost:5173

### Actividad React

Implementar:

- Listado de cursos.
- Registro de cursos.
- Eliminación de cursos.
- Actualización de cursos.
- Navegación con React Router.
- Consumo de API utilizando Axios.

---

# PARTE IV. ACTIVIDADES DE COMPARACIÓN

## 25. Actividad 1: Implementación CRUD

Completar las operaciones CRUD en los tres frameworks.

| Operación | Vue.js | Angular | React |
|---|---|---|---|
| Listar | GET | GET | GET |
| Registrar | POST | POST | POST |
| Actualizar | PUT | PUT | PUT |
| Eliminar | DELETE | DELETE | DELETE |

Cada estudiante deberá demostrar que las operaciones funcionan correctamente.

## 26. Actividad 2: Comparación de frameworks

Elaborar una tabla comparativa:

| Característica | Angular | Vue.js | React |
|---|---|---|---|
| Tipo de tecnología | | | |
| Componentes | | | |
| Routing | | | |
| HTTP | | | |
| Gestión de estado | | | |
| Formularios | | | |
| Curva de aprendizaje | | | |
| Organización del proyecto | | | |

## 27. Actividad 3: Mejoras de interfaz

Aplicar CSS o Bootstrap para mejorar la presentación.

La aplicación deberá incorporar:

- Menú de navegación.
- Tabla con estilos.
- Formularios organizados.
- Botones de acción.
- Mensajes de confirmación.
- Diseño adaptable a dispositivos móviles.

## 28. Actividad 4: Validaciones

Implementar validaciones para:

- Nombre obligatorio.
- Nombre con longitud mínima de 3 caracteres.
- Créditos mayores que cero.
- Mensajes de error cuando la API no esté disponible.
- Confirmación antes de eliminar un curso.

---

# PARTE V. ENTREGA DEL LABORATORIO

## 29. Estructura del repositorio

El repositorio GitHub deberá tener la siguiente estructura:

```text
lab-frontend-frameworks/
│
├── README.md
│
├── backend/
│   ├── package.json
│   └── server.js
│
├── frontend-vue/
│   └── src/
│
├── frontend-angular/
│   └── src/
│
└── frontend-react/
    └── src/
```

## 30. Evidencias

El estudiante deberá presentar:

1. URL del repositorio GitHub.
2. Aplicación Vue.js funcionando.
3. Aplicación Angular funcionando.
4. Aplicación React funcionando.
5. Evidencias de las operaciones CRUD.
6. Tabla comparativa de los frameworks.
7. Conclusiones del laboratorio.

## 31. Preguntas de evaluación

Responder las siguientes preguntas:

1. ¿Qué diferencias existen entre Angular, Vue.js y React respecto a su arquitectura?
2. ¿Qué ventajas ofrece Vue Router frente a implementar navegación manual?
3. ¿Qué ventajas ofrece Axios para consumir servicios REST?
4. ¿Qué diferencias existen entre Axios y HttpClient de Angular?
5. ¿Qué ventajas presenta el uso de componentes reutilizables?
6. ¿Qué diferencias existen entre `v-model`, `[(ngModel)]` y el manejo de estado con `useState`?
7. ¿Qué framework consideras más adecuado para desarrollar aplicaciones empresariales? Justifica tu respuesta.
8. ¿Qué dificultades encontraste al implementar la misma aplicación en los tres frameworks?

## 32. Reto adicional

Implementar una aplicación de gestión académica con las siguientes entidades:

- Cursos.
- Docentes.
- Estudiantes.
- Asignaturas.

Agregar:

- Relación entre docentes y cursos.
- Búsqueda de cursos.
- Paginación.
- Filtros.
- Validaciones avanzadas.
- Diseño responsive.
- Manejo centralizado de errores.

## 33. Criterios de evaluación

| Criterio | Puntaje |
|---|---:|
| Configuración y ejecución del backend | 2 |
| Implementación Vue.js | 4 |
| Implementación Angular | 4 |
| Implementación React | 4 |
| Operaciones CRUD completas | 3 |
| Comparación y conclusiones | 2 |
| Presentación y evidencias | 1 |
| **Total** | **20** |

## 34. Conclusiones esperadas

Al finalizar el laboratorio, el estudiante deberá reconocer que:

- Angular ofrece una estructura integrada y un conjunto amplio de herramientas.
- Vue.js facilita el desarrollo progresivo de interfaces y presenta una sintaxis accesible.
- React permite construir interfaces mediante componentes y una gestión flexible del estado.
- Los tres frameworks pueden consumir la misma API REST.
- La elección de un framework depende de las necesidades del proyecto, el equipo de desarrollo y la arquitectura de la aplicación.
