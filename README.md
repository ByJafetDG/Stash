# Stash

**Stash** es una plataforma web completa para la gestión de inventario, ventas, clientes, deudas, empleados, balances y análisis financiero, diseñada para pequeñas y medianas empresas.

Este proyecto está construido con:
- **Frontend**: HTML, CSS y JavaScript puros
- **Backend**: Java Spring Boot
- **Base de datos y servicios cloud**: Supabase (PostgreSQL, Auth y Storage)
- **Contenedores**: Docker
- **Arquitectura**: Monolítica con posibilidad de evolución a microservicios

---

## 🧱 Estructura del Proyecto

Stash/
├── deploy/ # Configuración de despliegue y contenedores
├── docs/ # Documentación técnica (PDF/DOCX)
├── stash-backend/ # Código backend (Java Spring Boot)
├── stash-frontend/
│ └── StashWeb/ # Código del frontend (HTML/CSS/JS)
└── README.md # Este archivo


---

## 🚀 Desarrollo

### Backend
- Java 17+
- Spring Boot
- JWT Supabase verification
- PostgreSQL (Supabase)

### Frontend
- HTML/CSS/JS (no framework)
- Conexión vía `fetch()` al API REST

### Dev Tools
- Docker + Docker Compose
- GitHub Actions (en etapas futuras)

---

## 📦 Docker

Puedes levantar el entorno de desarrollo completo usando:

```bash
docker-compose up --build

La API estará disponible en: http://localhost:8080
La base de datos se conecta a Supabase directamente.

🛠 En construcción
Este proyecto se encuentra en fase activa de desarrollo.
Consulta los issues o la hoja de ruta para más detalles.

yaml
Copiar
Editar

---

## 🐳 `Dockerfile` para backend (colocar en `stash-backend/`)

```dockerfile
# Dockerfile - stash-backend
FROM eclipse-temurin:17-jdk as build

WORKDIR /app
COPY . .

RUN ./mvnw clean package -DskipTests

FROM eclipse-temurin:17-jdk
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
