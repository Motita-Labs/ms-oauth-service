# ms-oauth-service

Microservicio de autenticación con JWT (Spring Boot 4, Spring Security, Java 17).

## Endpoints

Base: `/api/v1/auth`

| Método | Ruta                    | Descripción                  |
|--------|-------------------------|------------------------------|
| POST   | /api/v1/auth/register   | Registro de usuario          |
| POST   | /api/v1/auth/login      | Login, devuelve token JWT    |
| GET    | /api/v1/auth/perfil     | Perfil (requiere token)      |

Puerto: `8084`. Health: `/actuator/health`.

El token JWT se firma con `jwt.secret`; el mismo secreto lo usa el API Gateway para validar las peticiones.

## Build y test

```bash
mvn clean verify
```

## Docker

```bash
docker build -t arriendos/ms-oauth:latest .
docker run -p 8084:8084 -e DB_URL=jdbc:mysql://host:3306/auth -e JWT_SECRET=... arriendos/ms-oauth:latest
```

Variables: `DB_URL`, `DB_USER`, `DB_PASSWORD`, `JWT_SECRET`.

## CI/CD

`.github/workflows/ci-cd.yml`: build + test (`mvn verify`) y publicación de imagen en GHCR.
