# Kinvex Inventory Management System

Enterprise inventory management system divided into two main components:
- **KinvexCore**: Java/Spring Boot Backend (submodule)
- **KinvexUI**: React/TypeScript Frontend (submodule)

## Project Structure

```
kinvex-system/
├── KinvexCore/          # Spring Boot Backend (Git submodule)
├── KinvexUI/            # React Frontend (Git submodule)
├── docker-compose.yml   # Service orchestration
└── README.md
```

## Project Cloning

This project uses Git submodules. To clone correctly:

```bash
# Clone with submodules
git clone --recursive <repository-url>

# Or if you already cloned the main repo
git submodule init
git submodule update
```

## Submodule Updates

```bash
# Update all submodules
git submodule update --remote

# Update a specific submodule
git submodule update --remote KinvexCore
git submodule update --remote KinvexUI
```

## Prerequisites

- Java 21+
- Node.js 18+
- Docker and Docker Compose
- PostgreSQL 15+ (if not using Docker)
- Redis 7+ (if not using Docker)

## Development Setup

### Using Docker Compose (Recommended)

1. **Start only database and Redis:**
```bash
docker-compose up postgres redis
```

2. **Run backend locally:**
```bash
cd KinvexCore
./gradlew bootRun
```

3. **Run frontend locally:**
```bash
cd KinvexUI
npm install
npm run dev
```

### Manual Setup

1. **Configure PostgreSQL:**
```sql
CREATE DATABASE kinvex;
CREATE USER kinvex_user WITH PASSWORD 'kinvex_password';
GRANT ALL PRIVILEGES ON DATABASE kinvex TO kinvex_user;
```

2. **Set environment variables:**
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

## Full Docker Deployment

```bash
# Build and run all services
docker-compose --profile full up --build

# Infrastructure services only
docker-compose up postgres redis
```

## Access URLs

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8080
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **Actuator**: http://localhost:8080/actuator

## Useful Commands

### Backend (KinvexCore)
```bash
# Run tests
./gradlew test

# Build application
./gradlew build

# Run application
./gradlew bootRun
```

### Frontend (KinvexUI)
```bash
# Install dependencies
npm install

# Development mode
npm run dev

# Build for production
npm run build

# Run tests
npm run test
```

## Environment Variables Configuration

### Backend
- `DB_HOST`: PostgreSQL host (default: localhost)
- `DB_PORT`: PostgreSQL port (default: 5432)
- `DB_NAME`: Database name (default: kinvex)
- `DB_USERNAME`: Database user
- `DB_PASSWORD`: Database password
- `REDIS_HOST`: Redis host (default: localhost)
- `REDIS_PORT`: Redis port (default: 6379)
- `JWT_SECRET`: JWT secret key
- `CORS_ALLOWED_ORIGINS`: Allowed origins for CORS

### Frontend
- `VITE_API_BASE_URL`: Backend API base URL

## Architecture

The system implements a microservices architecture with:
- **JWT Authentication** with refresh tokens
- **PostgreSQL Database** for persistence
- **Redis** for caching and sessions
- **REST APIs** documented with OpenAPI
- **React Interface** with Material-UI

## Main Features

1. **Product Management**: Complete CRUD for products with stock control
2. **External Integration**: REST API for billing systems
3. **Purchase Orders**: Complete order management to suppliers
4. **Reports**: PDF and Excel report generation
5. **Audit**: Complete operation logging
6. **Dashboard**: Real-time inventory metrics

## Contributing

1. Fork the project
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## License

This project is under the MIT license. See the [LICENSE](LICENSE) file for more details.

**Developed by [Kreaker.dev](https://kreaker.dev)**

When using this software, you must maintain attribution to the original developer in any distribution or derivative work.
