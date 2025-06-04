# Proyecto Backend - Sistema de Gestión de Biblioteca

## Información del Alumno
- Nombre y Apellido: Joaquìn Pastorino
- Curso: 5to Año
- Especialidad: Informática

## Configuración del Repositorio
- La rama `main` debe estar protegida
- No se permiten push directos a `main`
- Todos los cambios deben realizarse a través de Pull Requests
- Los Pull Requests deben ser aprobados antes de ser mergeados

## Descripción
Este proyecto consiste en desarrollar un sistema backend para la gestión de una biblioteca escolar. El desarrollo se realizará en tres fases incrementales:

### Fase 1: Gestión de Libros
Implementación de la API REST para gestionar libros, incluyendo:
- CRUD completo de libros
- Búsqueda y filtrado
- Documentación de endpoints

### Fase 2: Gestión de Usuarios
Implementación del sistema de usuarios, incluyendo:
- Registro y autenticación
- Roles y permisos
- Perfiles de usuario

### Fase 3: Gestión de Préstamos
Implementación del sistema de préstamos, incluyendo:
- Préstamos y devoluciones
- Historial de préstamos
- Notificaciones

## Elección de Tecnología

Para el desarrollo de este proyecto se eligió la siguiente stack tecnológica:

- **Python + FastAPI + Tortoise ORM + SQLite**

### Justificación de la elección

- **FastAPI:** Framework moderno, rápido y fácil de aprender para construir APIs.
- **Tortoise ORM:** ORM asíncrono que se integra muy bien con FastAPI y permite trabajar con sintaxis moderna.
- **SQLite:** Base de datos ligera, ideal para desarrollo y pruebas, no requiere configuración de servidor.

### Dependencias utilizadas

- `fastapi`
- `uvicorn`
- `tortoise-orm`
- `pydantic`
- `python-jose`
- `passlib`
- `python-multipart`

## Instalación del Entorno y Dependencias

Sigue estos pasos para preparar el entorno de desarrollo:

1. **Crear un entorno virtual (venv):**

   ```bash
   python3 -m venv venv
   ```

2. **Activar el entorno virtual:**

   - En Linux/Mac:
     ```bash
     source venv/bin/activate
     ```
   - En Windows:
     ```cmd
     venv\Scripts\activate
     ```

3. **Instalar las dependencias:**

   ```bash
   pip install fastapi uvicorn tortoise-orm pydantic python-jose passlib python-multipart
   ```

## Cómo ejecutar el backend

Sigue estos pasos para levantar el backend de la biblioteca:

1. **Clona el repositorio y entra a la carpeta del proyecto:**
   ```bash
   git clone <url-del-repositorio>
   cd 2025-first-backend-SIRWARRIOR2017
   ```

2. **Crea y activa un entorno virtual:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Instala las dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

4. **(Opcional) Configura la base de datos:**
   - Si usas SQLite, ya está lista para pruebas.
   - Si usas variables de entorno, copia `.env.example` a `.env` y edítalo según tu configuración.

5. **Ejecuta el backend:**
   ```bash
   uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
   ```
   Esto levantará el servidor en http://localhost:8000

6. **Accede a la documentación interactiva:**
   - Swagger UI: http://localhost:8000/docs
   - Redoc: http://localhost:8000/redoc

7. **Ejecuta el frontend:**
   - Clona el repositorio del frontend:
     ```bash
     git clone <url-del-repo-frontend>  # Reemplaza por la URL real
     cd 2025-first-basic-frontend-SIRWARRIOR2017
     ```
   - Abre la carpeta en Visual Studio Code.
   - Instala la extensión **Live Server** desde el marketplace de VS Code.
   - Haz clic derecho sobre el archivo `index.html` y selecciona **"Open with Live Server"** o abajo a la derecha toca "Go Live".
   - El frontend se abrirá en tu navegador y podrás interactuar con la API del backend.

### Pruebas

- Para ejecutar las pruebas, asegúrate de tener el entorno virtual activado y ejecuta:

  ```bash
  pytest
  ```

## Objetivos de Aprendizaje
- Diseñar e implementar una API REST
- Trabajar con bases de datos SQL a través de ORM
- Manejar versionado de código con Git
- Trabajar con milestones e issues en GitHub
- Documentar la API

## Tecnologías
Los estudiantes pueden elegir entre las siguientes tecnologías:
- Node.js + Express + Sequelize + SQLite
- Python + Flask + SQLAlchemy + SQLite
- Python + FastAPI + Tortoise ORM + SQLite

Nota: Se debe utilizar un ORM (Object-Relational Mapping) para interactuar con la base de datos. No se permite el uso de SQL nativo.

## Pruebas de la API
- Se recomienda utilizar REST Client para probar los endpoints
- El archivo `request.http` en el proyecto contiene todas las peticiones necesarias
- Incluye ejemplos de todas las operaciones CRUD
- Cada petición está documentada con comentarios explicativos

## Fase 1: Gestión de Libros

### Modelo de Datos (actualmente en memoria)
```python
class Libro(BaseModel):
    id: int
    titulo: str
    autor: str
    isbn: str
    categoria: str
    estado: str
```

### Endpoints
```
GET    /libros           # Listar todos los libros
GET    /libros/{id}      # Obtener un libro específico
POST   /libros           # Crear un nuevo libro
PUT    /libros/{id}      # Actualizar un libro
DELETE /libros/{id}      # Eliminar un libro
GET    /libros/buscar    # Buscar libros (parámetros: titulo, autor, categoria)
```

### Milestones Fase 1
1. Configuración Inicial
   - [ ] Configurar el proyecto base
   - [ ] Implementar la conexión a la base de datos
   - [ ] Crear el modelo de libros

2. CRUD Básico
   - [ ] Implementar endpoints para libros
   - [ ] Implementar validación de datos
   - [ ] Documentar los endpoints

3. Búsqueda y Filtrado
   - [ ] Implementar búsqueda por título
   - [ ] Implementar filtrado por categoría
   - [ ] Implementar ordenamiento
   - [ ] Implementar paginación

## Fase 2: Gestión de Usuarios

### Modelo de Datos
```python
# Ejemplo con Tortoise ORM
class Usuario(Model):
    id = fields.IntField(pk=True)
    nombre = fields.CharField(max_length=100)
    apellido = fields.CharField(max_length=100)
    email = fields.CharField(max_length=255, unique=True)
    password = fields.CharField(max_length=255)
    rol = fields.CharField(max_length=50)  # admin, usuario
    activo = fields.BooleanField(default=True)
    fecha_creacion = fields.DatetimeField(auto_now_add=True)
```

### Endpoints
```
POST   /auth/registro    # Registrar nuevo usuario
POST   /auth/login       # Iniciar sesión
GET    /usuarios         # Listar usuarios (solo admin)
GET    /usuarios/{id}    # Obtener perfil de usuario
PUT    /usuarios/{id}    # Actualizar perfil
```

### Milestones Fase 2
1. Autenticación Básica
   - [ ] Implementar registro de usuarios
   - [ ] Implementar login/logout
   - [ ] Implementar tokens JWT

2. Gestión de Usuarios
   - [ ] Implementar roles y permisos
   - [ ] Implementar gestión de perfiles
   - [ ] Proteger endpoints según roles

## Fase 3: Gestión de Préstamos

### Modelo de Datos
```python
# Ejemplo con Tortoise ORM
class Prestamo(Model):
    id = fields.IntField(pk=True)
    libro = fields.ForeignKeyField('models.Libro')
    usuario = fields.ForeignKeyField('models.Usuario')
    fecha_prestamo = fields.DatetimeField(auto_now_add=True)
    fecha_devolucion = fields.DatetimeField(null=True)
    estado = fields.CharField(max_length=50)  # activo, devuelto, vencido
```

### Endpoints
```
POST   /prestamos           # Crear nuevo préstamo
PUT    /prestamos/{id}      # Registrar devolución
GET    /prestamos/activos   # Listar préstamos activos
GET    /prestamos/historial # Ver historial de préstamos
GET    /prestamos/vencidos  # Listar préstamos vencidos
```

### Milestones Fase 3
1. Sistema de Préstamos
   - [ ] Implementar préstamos de libros
   - [ ] Implementar devolución de libros
   - [ ] Implementar validaciones de préstamos

2. Gestión de Estado
   - [ ] Implementar historial de préstamos
   - [ ] Implementar notificaciones de vencimiento
   - [ ] Implementar reportes

## Criterios de Evaluación
- Correcta implementación de los endpoints
- Calidad del código
- Manejo de errores
- Documentación
- Uso correcto de Git
- Gestión de milestones e issues

## Entregables
1. Repositorio Git con el código fuente
2. Documentación de la API
3. Archivo requests.http con ejemplos de uso
4. Diagrama de la base de datos
5. Presentación del proyecto

