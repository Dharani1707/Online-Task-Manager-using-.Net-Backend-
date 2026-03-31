# TaskManager Backend by Sanjaya R (.NET 8 + SQL Server + Cookie Auth)

## Project structure
- `src/TaskManager.Api` - Web API (controllers, auth cookie, middleware)
- `src/TaskManager.Application` - DTOs + services (use cases)
- `src/TaskManager.Domain` - entities + enums + repository interfaces
- `src/TaskManager.Infrastructure` - EF Core (DbContext), repositories, hashing, DI

## Prereqs
- .NET 8 SDK
- SQL Server or SQL Express

## Configure DB
Edit `src/TaskManager.Api/appsettings.json` connection string.

Example:
`Server=localhost\SQLEXPRESS;Database=TaskManagerDb;Trusted_Connection=True;TrustServerCertificate=True;`

## Used Entity Framework (EF) Code First approach

## Run migrations
From repo root:

```bash
dotnet restore
dotnet tool update --global dotnet-ef
dotnet ef migrations add InitialCreate -p src/TaskManager.Infrastructure -s src/TaskManager.Api
dotnet ef database update -p src/TaskManager.Infrastructure -s src/TaskManager.Api
dotnet run --project src/TaskManager.Api
```

Swagger: `/swagger`

## Auth flow
- Register: `POST /api/auth/register`
- Login: `POST /api/auth/login` => sets cookie
- Me: `GET /api/auth/me`
- Logout: `POST /api/auth/logout`

Angular must send `withCredentials: true` and backend CORS must allow credentials.
