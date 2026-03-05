# 🎓 Sistema de Gestión Académica Universitaria

## 🗄️ Descripción del Proyecto

El sistema centraliza la administración académica de una universidad: carreras, alumnos, profesores, cursos, matrículas y usuarios. El eje del proyecto fue el diseño de la base de datos relacional, garantizando integridad, consistencia, seguridad y trazabilidad completa.

---

## ⚙️ Motor y Tecnología

| Característica | Detalle |
|---|---|
| Base de datos | MySQL |

---

## 📐 Diagrama Entidad-Relación

![Diagrama ER](DiagramaBaseDeDatos.png)

> 💡 También disponible como [DiagramaBaseDeDatos.pdf](https://github.com/user-attachments/files/25757531/DiagramaBaseDeDatos.pdf) en este repositorio.

---

## 📂 Tablas Catálogo

Se crearon tablas catálogo para centralizar valores que se repiten en varias entidades:

- `tipo_documento` — usado en alumnos y profesores
- `sexo` — usado en alumnos y profesores
- `estado_civil` — usado en alumnos y profesores

Esto evita inconsistencias por escritura manual y facilita el mantenimiento futuro.

---


## 🔗 Integridad Referencial

Todas las relaciones entre tablas están definidas mediante claves foráneas:

```
alumnos        → carreras, tipo_documento, sexo, estado_civil
profesores     → tipo_documento, sexo, estado_civil
cursos         → carreras, profesores
alumno_curso   → alumnos, cursos
```

Ningún registro puede apuntar a datos que no existan. La base de datos lo rechaza por sí misma.

---

## 🔄 Relación Muchos a Muchos

Un alumno puede estar en varios cursos y un curso puede tener varios alumnos. Para resolver esa relación se creó la tabla intermedia `alumno_curso`, que registra el alumno, el curso, el ciclo académico, la nota final y el estado del curso.

Para evitar matrículas duplicadas se implementó una restricción directamente en la base de datos:

```sql
UNIQUE (id_alumno, id_curso, ciclo)
```

---

## 📊 Auditoría y Eliminación Lógica

Todas las tablas principales incluyen campos de auditoría:

```sql
estado_auditoria      -- activo o inactivo
fecha_creacion        -- cuándo se creó el registro
fecha_modificacion    -- cuándo se modificó por última vez
usuario_creacion      -- quién lo creó
usuario_modificacion  -- quién lo modificó
```

Los registros nunca se eliminan físicamente. Se desactivan lógicamente, preservando el historial académico completo.

---

## 🛡️ Restricciones y Validaciones

| Restricción | Uso |
|---|---|
| `PRIMARY KEY` | Identificador único en cada tabla |
| `FOREIGN KEY` | Integridad entre entidades |
| `UNIQUE` | Prevención de duplicados |
| `NOT NULL` | Campos obligatorios |
| `ENUM` | Valores controlados en estados y grados |
| `AUTO_INCREMENT` | Generación automática de IDs |

La base de datos valida los datos por sí misma, sin depender únicamente del backend.

---


## 🧩 Desafíos Técnicos

**Relación muchos a muchos** — Resuelta con tabla intermedia `alumno_curso` y claves foráneas.

**Matrículas duplicadas** — Resuelta con restricción `UNIQUE` compuesta a nivel de base de datos.

**Trazabilidad sin pérdida de datos** — Resuelta con eliminación lógica y campos de auditoría en todas las tablas críticas.

---

## 🎤 Guía de Exposición

### Introducción

El siguiente diagrama representa la estructura de la base de datos del sistema de gestión académica. Fue desarrollada en MySQL utilizando el motor InnoDB, el cual permite el uso de claves foráneas, integridad referencial y soporte de transacciones.

La base de datos está compuesta por 9 tablas, cada una diseñada con un propósito específico dentro del modelo relacional.

---

### Tablas Catálogo

Las tablas `tipo_documento`, `sexo` y `estado_civil` cumplen la función de catálogos. Su implementación evita la repetición de valores en tablas principales como `alumnos` y `profesores`. Este enfoque garantiza:

- Consistencia en los datos
- Mayor escalabilidad
- Mejor mantenimiento
- Reducción de redundancia

Ambas entidades dependen de estas tablas para mantener uniformidad en la información.

---

### Carreras

La tabla `carreras` almacena los programas académicos ofrecidos por la universidad. Es considerada una tabla base dentro del sistema, ya que tanto `alumnos` como `cursos` dependen de ella mediante claves foráneas. Esto permite mantener una estructura jerárquica clara dentro del modelo académico.

---

### Alumnos y Profesores

La tabla `alumnos` contiene la información principal de los estudiantes. Gran parte de sus campos están relacionados con otras tablas mediante claves foráneas: carrera, tipo de documento, sexo y estado civil. Gracias a estas restricciones, la base de datos impide el registro de valores inexistentes, asegurando integridad referencial sin depender exclusivamente del backend.

La tabla `profesores` sigue la misma lógica estructural, incluyendo campos específicos como grado académico, pago mensual y fecha de ingreso. Ambas tablas aplican validaciones como `UNIQUE`, `NOT NULL` y `ENUM` para reforzar la consistencia de la información.

---

### Cursos

La tabla `cursos` establece la relación entre una carrera y un profesor. Permite determinar qué docente dicta cada curso y a qué programa académico pertenece. Incluye además una restricción `UNIQUE (nombre_curso, id_carrera)` para evitar duplicidad de cursos dentro de la misma carrera.

---

### alumno_curso — Decisión Clave del Diseño

La relación entre alumnos y cursos es de tipo muchos a muchos: un alumno puede matricularse en varios cursos y un curso puede tener varios alumnos.

Para resolver esta relación se creó la tabla intermedia `alumno_curso`, la cual permite registrar la matrícula, guardar el ciclo académico, almacenar la nota final y controlar el estado del curso.

Se implementó además la restricción:

```sql
UNIQUE (id_alumno, id_curso, ciclo)
```

Esto impide que un alumno se matricule dos veces en el mismo curso durante el mismo ciclo académico, dejando el control directamente en la base de datos.

---

### Usuarios del Sistema

La tabla `usuarios_sistemas` se encuentra separada del modelo académico. Su función es manejar la autenticación, el acceso al sistema y el control de roles. Se diseñó de manera independiente porque un usuario del sistema no necesariamente corresponde a un alumno o profesor.

---

### Auditoría

Las tablas principales incluyen campos de auditoría: `fecha_creacion`, `fecha_modificacion`, `usuario_creacion`, `usuario_modificacion` y `estado_auditoria`.

En lugar de realizar eliminaciones físicas, se aplica eliminación lógica mediante un campo de estado. Esto permite conservar el historial académico y mantener trazabilidad completa de las operaciones realizadas.

---

### Cierre

El diseño de la base de datos fue concebido bajo principios de normalización y buenas prácticas relacionales. Se priorizó la integridad referencial, el control de duplicidad, las validaciones estructurales, la trazabilidad y la escalabilidad.

El objetivo principal fue lograr que la base de datos garantice la consistencia y confiabilidad de la información por sí misma, reduciendo la dependencia exclusiva del código de aplicación.

---

## 👨‍💻 Autor

**Apaza Sandagorda, Jhoandry Albino**

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

