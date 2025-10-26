# Sistema de Gestión de Inventario Kinvex

Sistema empresarial de gestión de inventario dividido en dos componentes principales:
- **KinvexCore**: Backend en Java/Spring Boot (submódulo)
- **KinvexUI**: Frontend en React/TypeScript (submódulo)

## Estructura del Proyecto

```
kinvex-system/
├── KinvexCore/          # Backend Spring Boot (Git submodule)
├── KinvexUI/            # Frontend React (Git submodule)
├── docker-compose.yml   # Orquestación de servicios
└── README.md
```

## Clonación del Proyecto

Este proyecto utiliza Git submódulos. Para clonar correctamente:

```bash
# Clonar con submódulos
git clone --recursive <repository-url>

# O si ya clonaste el repo principal
git submodule init
git submodule update
```

## Actualización de Submódulos

```bash
# Actualizar todos los submódulos
git submodule update --remote

# Actualizar un submódulo específico
git submodule update --remote KinvexCore
git submodule update --remote KinvexUI
```

## Requisitos Previos

- Java 21+
- Node.js 18+
- Docker y Docker Compose
- PostgreSQL 15+ (si no usa Docker)
- Redis 7+ (si no usa Docker)

## Configuración de Desarrollo

### Usando Docker Compose (Recomendado)

1. **Iniciar solo la base de datos y Redis:**
```bash
docker-compose up postgres redis
```

2. **Ejecutar el backend localmente:**
```bash
cd KinvexCore
./gradlew bootRun
```

3. **Ejecutar el frontend localmente:**
```bash
cd KinvexUI
npm install
npm run dev
```

### Configuración Manual

1. **Configurar PostgreSQL:**
```sql
CREATE DATABASE kinvex;
CREATE USER kinvex_user WITH PASSWORD 'kinvex_password';
GRANT ALL PRIVILEGES ON DATABASE kinvex TO kinvex_user;
```

2. **Configurar variables de entorno:**
```bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=kinvex
export DB_USERNAME=kinvex_user
export DB_PASSWORD=kinvex_password
export REDIS_HOST=localhost
export REDIS_PORT=6379
export JWT_SECRET=your-secret-key
```

## Despliegue Completo con Docker

```bash
# Construir y ejecutar todos los servicios
docker-compose --profile full up --build

# Solo servicios de infraestructura
docker-compose up postgres redis
```

## URLs de Acceso

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8080
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **Actuator**: http://localhost:8080/actuator

## Comandos Útiles

### Backend (KinvexCore)
```bash
# Ejecutar tests
./gradlew test

# Construir aplicación
./gradlew build

# Ejecutar aplicación
./gradlew bootRun
```

### Frontend (KinvexUI)
```bash
# Instalar dependencias
npm install

# Modo desarrollo
npm run dev

# Construir para producción
npm run build

# Ejecutar tests
npm run test
```

## Configuración de Variables de Entorno

### Backend
- `DB_HOST`: Host de PostgreSQL (default: localhost)
- `DB_PORT`: Puerto de PostgreSQL (default: 5432)
- `DB_NAME`: Nombre de la base de datos (default: kinvex)
- `DB_USERNAME`: Usuario de la base de datos
- `DB_PASSWORD`: Contraseña de la base de datos
- `REDIS_HOST`: Host de Redis (default: localhost)
- `REDIS_PORT`: Puerto de Redis (default: 6379)
- `JWT_SECRET`: Clave secreta para JWT
- `CORS_ALLOWED_ORIGINS`: Orígenes permitidos para CORS

### Frontend
- `VITE_API_BASE_URL`: URL base del API backend

## Arquitectura

El sistema implementa una arquitectura de microservicios con:
- **Autenticación JWT** con refresh tokens
- **Base de datos PostgreSQL** para persistencia
- **Redis** para caché y sesiones
- **APIs REST** documentadas con OpenAPI
- **Interfaz React** con Material-UI

## Funcionalidades Principales

1. **Gestión de Productos**: CRUD completo de productos con control de stock
2. **Integración Externa**: API REST para sistemas de facturación
3. **Órdenes de Compra**: Gestión completa de órdenes a proveedores
4. **Reportes**: Generación de reportes en PDF y Excel
5. **Auditoría**: Registro completo de operaciones
6. **Dashboard**: Métricas en tiempo real del inventario

## Contribución

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -am 'Añade nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crea un Pull Request

## Licencia

Este proyecto está bajo la licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

**Desarrollado por [Kreaker.dev](https://kreaker.dev)**

Al usar este software, debes mantener la atribución al desarrollador original en cualquier distribución o trabajo derivado.
