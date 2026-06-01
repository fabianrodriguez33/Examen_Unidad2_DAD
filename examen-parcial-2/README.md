# Examen Parcial 2 – Diseño de Aplicaciones Distribuidas

Arquitectura de microservicios con Spring Boot, Spring Cloud, Docker y MySQL.

## Microservicios

| # | Servicio | Puerto | Descripción |
|---|---|---|---|
| 1 | `ms-admin-config-server` | 8888 | Spring Cloud Config Server |
| 2 | `ms-admin-registry-server` | 8761 | Netflix Eureka Server |
| 3 | `ms-admin-api-gateway` | 8080 | Spring Cloud Gateway |
| 4 | `ms-gestion-instructor` | 8082 | CRUD instructores (MySQL) |
| 5 | `ms-gestion-alumno` | 8083 | CRUD alumnos (MySQL) |
| 6 | `ms-gestion-taller` | 8084 | CRUD talleres (MySQL) |
| 7 | `auth-service` | 8085 | Autenticación JWT (PostgreSQL) |

## Tecnologías

- Java 21 + Spring Boot 3.5
- Spring Cloud 2025 (Config, Eureka, Gateway, OpenFeign)
- MySQL 8.4 / PostgreSQL 16
- Docker & Docker Compose
- Swagger / OpenAPI (springdoc 2.x)
- Maven

## Cómo ejecutar con Docker

### 1. Compilar todos los microservicios

Ejecuta desde la raíz de cada microservicio:

```bash
# Opción A: compilar uno por uno
cd ms-admin-config-server  && ./mvnw clean package -DskipTests && cd ..
cd ms-admin-registry-server && ./mvnw clean package -DskipTests && cd ..
cd ms-admin-api-gateway     && ./mvnw clean package -DskipTests && cd ..
cd ms-gestion-instructor    && ./mvnw clean package -DskipTests && cd ..
cd ms-gestion-alumno        && ./mvnw clean package -DskipTests && cd ..
cd ms-gestion-taller        && ./mvnw clean package -DskipTests && cd ..
cd auth-service             && ./mvnw clean package -DskipTests && cd ..
```

### 2. Levantar toda la infraestructura

```bash
docker compose up --build
```

### 3. Verificar servicios

| Servicio | URL |
|---|---|
| Eureka Dashboard | http://localhost:8761 |
| API Gateway | http://localhost:8080 |
| Swagger Instructor | http://localhost:8082/swagger-ui.html |
| Swagger Alumno | http://localhost:8083/swagger-ui.html |
| Swagger Taller | http://localhost:8084/swagger-ui.html |

## Ejecución en local (sin Docker)

Inicia en este orden:
1. `ms-admin-config-server`
2. `ms-admin-registry-server`
3. `ms-admin-api-gateway`
4. `auth-service`, `ms-gestion-instructor`, `ms-gestion-alumno`, `ms-gestion-taller` (cualquier orden)

Asegúrate de tener MySQL y PostgreSQL corriendo localmente con los puertos y credenciales definidos en cada `application.properties`.
