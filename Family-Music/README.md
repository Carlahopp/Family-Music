# 🎼 Family-Music - API REST

# 🎼 API REST: Family-Music

Bienvenido al repositorio oficial del proyecto **Family-Music**. Este documento contiene la planeación estratégica, requerimientos técnicos y el ciclo de vida de desarrollo de nuestra solución backend.

---

## Perfil del Proyecto:
### Definición del proyecto y sus necesidades:
El proyecto consiste en diseñar y desplegar una arquitectura backend robusta para la gestión dinámica de un catálogo musical, permitiendo operaciones de registro, consulta y eliminación de datos en tiempo real  (*hardcoded*).

### Especificaciones Técnicas
* **Desarrolladores Front-end:** (Asignar miembros de tu equipo).
  * *Herramientas:* HTML5, CSS3, JavaScript Async/Await (para consumo dinámico).
* **Desarrolladores Back-end:** (Asignar miembros de tu equipo).
  * *Herramientas:* Java, Spring Boot (Spring Web, Spring Data JPA).
* **Base de Datos:** MySQL (Esquema relacional).

### Costo
* **Activos Libres:**
  * Vectores y Diseño: [Public Domain Vectors](https://publicdomainvectors.org)
  * Ilustraciones: [unDraw Illustrations](https://undraw.co)
  * Pruebas de Software: Postman (Gratis)
* **Alojamiento (hosting):**
  * Servidores locales y entornos de despliegue gratuitos (Render / Clever Cloud / Railway).

### Fecha límite
* **Fin de semana** (Cierre del Sprint actual).

---

## Metas y Objetivos del Proyecto
### Meta
* Crear y desplegar una API REST completamente funcional para la gestión del catálogo de música familiar.

### Objetivos
* **Sitio Backend Dinámico:** Expone 4 o más endpoints REST funcionales.
* **Tema Musical:** Administra entidades reales (Artistas, Álbumes, Canciones).
* **Persistencia Real:** Almacena imágenes, metadatos y texto relacionados en bases de datos relacionales sin usar datos fijos.

---

## Ciclo de Vida del Desarrollo:

### ○ Planificación
* Utilizar **Visual Studio Code** como entorno de desarrollo integrado gratuito.
* Configurar y estructurar las rutas base de la REST API y la conexión limpia a la base de datos.
* Conectar Visual Studio Code al repositorio unificado de GitHub (`Family-Music`).
* Determinar que necesitamos usar Java, Spring Boot y JavaScript para los flujos dinámicos.

### ○ Análisis
* Modelado y diseño de los requerimientos para el consumo y transferencia de datos a través de peticiones HTTP.
* Investigación y capacitación técnica continua a través de proyectos prácticos orientados a servicios backend.
* **¿Cuántos recursos necesitamos para ejecutar nuestro sitio web?:** Recursos mínimos y ligeros que puedan ser alojados en la nube de forma gratuita y validados directamente por el Product Owner.

### ○ Diseño / requerimientos
* Se han documentado todos los requisitos del sistema y Criterios de Aceptación en este repositorio.
* Las características de la API deben responder de forma dinámica utilizando códigos de estado HTTP correctos (`201 Created`, `400 Bad Request`, `404 Not Found`).
* Diseño del mapa lógico de relaciones entre tablas en MySQL.

### ○ Implementación
* Escribe el código ordenado y estructurado del backend en Java dentro de Visual Studio Code.
* Desarrollar scripts de consumo dinámico para que el navegador renderice la información musical en tiempo real.
* Hospeda el sitio web y los endpoints en un servidor remoto de pruebas.

### ○ Pruebas e Integración
* Ejecutar y validar las solicitudes a la API web varias veces usando Postman para asegurar la estabilidad del sistema.

### ○ Mantenimiento
* Monitorear los *logs* de errores y visitar el sitio web de vez en cuando para refactorizar código acoplado y garantizar la disponibilidad de la plataforma.

---

## 📋 Product Backlog & Historias de Usuario

### 👤 Módulo 1: Gestión de Artistas
#### 📌 US01: Registrar un nuevo Artista
* **Como:** Administrador del sistema musical.
* **Quiero:** Registrar un nuevo artista enviando un payload JSON al sistema.
* **Para:** Mantener la base de datos actualizada sin usar registros quemados (*hardcoded*).
* **Criterios de Aceptación:**
  * Dado un JSON válido con `nombre`, `generoPrincipal` y `paisOrigen`, la API debe responder con un código HTTP `201 Created` y el objeto creado con su `ID` autogenerado.
  * Si el campo `nombre` llega vacío o nulo, la API debe rechazar la solicitud con un código HTTP `400 Bad Request`.

#### 📌 US02: Consultar detalles de un Artista
* **Como:** Usuario de la plataforma.
* **Quiero:** Obtener la información de un artista específico mediante su identificador único.
* **Para:** Visualizar su perfil y desplegar su catálogo musical asociado de forma dinámica.
* **Criterios de Aceptación:**
  * Al realizar una petición `GET` a `/api/v1/artistas/{id}`, la API debe retornar un HTTP `200 OK` con la información del artista y un arreglo con sus álbumes relacionados.
  * Si el `id` no existe, el sistema debe capturar la excepción y responder con un HTTP `404 Not Found`.

---

### 💿 Módulo 2: Gestión de Álbumes
#### 📌 US03: Crear un Álbum asociado a un Artista
* **Como:** Administrador del sistema musical.
* **Quiero:** Registrar un álbum vinculándolo directamente al identificador de un artista existente.
* **Para:** Estructurar de manera correcta las relaciones lógicas de la base de datos.
* **Criterios de Aceptación:**
  * La petición `POST` a `/api/v1/albumes` debe incluir una llave foránea válida (`artistaId`). Si existe, guarda y responde con HTTP `201 Created`.
  * Si el `artistaId` no corresponde a ningún registro, el backend debe lanzar un error controlado de integridad y responder con un HTTP `422 Unprocessable Entity`.

---

### 🎵 Módulo 3: Gestión de Canciones
#### 📌 US04: Agregar una Canción a un Álbum
* **Como:** Administrador del sistema musical.
* **Quiero:** Dar de alta una pista musical asignándole campos dinámicos (`titulo` y `duracionSegundos`) vinculados a un álbum.
* **Para:** Completar el esquema relacional del catálogo.
* **Criterios de Aceptación:**
  * Al guardar la canción de manera exitosa, el sistema debe retornar un HTTP `201 Created`.
  * El campo `duracionSegundos` debe validarse para aceptar únicamente valores numéricos mayores a cero; de lo contrario, responderá con un HTTP `400 Bad Request`.