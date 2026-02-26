# 🎓 Sistema de Gestión Académica Universitaria

Este proyecto es un **Sistema de Gestión Académica** diseñado para optimizar y centralizar la administración de información universitaria.  
Permite gestionar **carreras, profesores, alumnos, cursos y matrículas** mediante una **API REST robusta y segura**.

El sistema facilita el registro de estudiantes, la asignación de cursos a docentes, el control de matrículas y el seguimiento académico a través de **notas y estados**.  
Además, implementa **autenticación segura con JWT** y **auditoría completa** para todas las operaciones realizadas.

---

## 👥 Integrantes

- Apaza Sandagorda, Jhoandry Albino  


---

## 🎯 Alcance del Proyecto

El sistema de gestión académica busca **automatizar y centralizar la administración universitaria**, permitiendo:

- Gestión completa de carreras.
- Registro y administración de profesores y alumnos.
- Creación y asignación de cursos a carreras y docentes.
- Matrícula de estudiantes en cursos específicos.
- Registro de notas finales y estados académicos.
- Autenticación y control de acceso basado en roles.
- Auditoría completa de todas las operaciones.
- Consultas académicas y generación de reportes del sistema.

Con este sistema se facilita la labor del área académica y administrativa de la universidad, **reduciendo tiempos de gestión** y **mejorando la organización** de los procesos educativos.

---

## 🗄️ Diseño de Base de Datos

📄 **Diagrama:** [DiagramaBaseDeDatos.pdf](https://github.com/user-attachments/files/24425558/DiagramaBaseDeDatos.pdf)


La base de datos está **normalizada** y utiliza **claves foráneas** para garantizar la integridad referencial.  
Además, implementa:

- Eliminación lógica de registros.
- Campos de auditoría para el control de operaciones.
- Relaciones claras entre las entidades académicas.

---

## 🛠️ Tecnologías Utilizadas

- **Node.js + TypeScript**: Runtime y lenguaje principal del backend con tipado estático.
- **Express**: Framework web para la creación de la API REST.
- **MySQL**: Sistema de gestión de base de datos relacional.
- **MySQL2**: Driver de conexión entre Node.js y MySQL.
- **JWT (jsonwebtoken)**: Autenticación basada en tokens.
- **Bcrypt**: Encriptación segura de contraseñas.
- **Zod**: Validación de esquemas y datos de entrada.
- **Morgan**: Logger de peticiones HTTP.
- **Dotenv**: Gestión de variables de entorno.

---

# 📚 API Universidad - Endpoints Disponibles

**Base URL:** `http://localhost:3000/api/v1`

## 📂 Carreras

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | /carreras      | Listar todas las carreras |
| GET    | /carreras/:id  | Obtener una carrera por ID |
| POST   | /carreras      | Registrar una nueva carrera |
| PUT    | /carreras/:id  | Actualizar información de una carrera |
| DELETE | /carreras/:id  | Eliminar lógicamente una carrera |

---

## 📂 Profesores

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | /profesores      | Listar todos los profesores |
| GET    | /profesores/:id  | Obtener un profesor por ID |
| POST   | /profesores      | Registrar un nuevo profesor |
| PUT    | /profesores/:id  | Actualizar información de un profesor |
| DELETE | /profesores/:id  | Eliminar lógicamente un profesor |

---

## 📂 Alumnos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | /alumnos      | Listar todos los alumnos |
| GET    | /alumnos/:id  | Obtener un alumno por ID |
| POST   | /alumnos      | Registrar un nuevo alumno |
| PUT    | /alumnos/:id  | Actualizar información de un alumno |
| DELETE | /alumnos/:id  | Eliminar lógicamente un alumno |

---

## 📂 Cursos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | /cursos               | Listar todos los cursos |
| GET    | /cursos/:id           | Obtener un curso por ID |
| POST   | /cursos               | Registrar un nuevo curso |
| PUT    | /cursos/:id           | Actualizar información de un curso |
| DELETE | /cursos/:id           | Eliminar lógicamente un curso |

---

## 📂 Alumno_Curso

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | /alumno-cursos             | Listar todas las matrículas |
| GET    | /alumno-cursos/:id         | Obtener cursos y alumnos por matricula |
| POST   | /alumno-cursos             | Matricular un alumno en un curso |
| PUT    | /alumno-cursos/:id         | Actualizar nota final o estado del curso |
| DELETE | /alumno-cursos/:id         | Eliminar lógicamente una matrícula |

---

