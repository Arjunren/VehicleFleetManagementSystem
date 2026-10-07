# Vehicle Fleet Management System

## Overview
ASP.NET Core API for vehicles, drivers, assignments, maintenance history, and fleet availability reporting.

## Features
- JWT authentication with Admin, Dispatcher, and Driver roles
- Vehicle and driver management with unique identifiers
- Transactional assignment and completion workflows
- Active driver/vehicle conflict prevention and license-expiry checks
- Driver-owned assignment views, maintenance records, pagination, search, and dashboard

## Technology Stack
.NET 10, ASP.NET Core, EF Core 10, SQLite, JWT, xUnit, Docker.

## Requirements / Installation / Running
Install .NET SDK 10, then run `dotnet restore Fleet.slnx` and `dotnet run --project src/Fleet.Api`. SQLite is created automatically and `migrations/001_initial.sql` documents the schema. Docker: `docker build -t fleet-api .` then `docker run -p 8080:8080 fleet-api`.

## Environment Variables
Use `.env.example`; replace `Jwt__Secret` and configure `ConnectionStrings__Default` and `ASPNETCORE_URLS`.

## Running Tests
Run `dotnet test Fleet.slnx` and `dotnet list Fleet.slnx package --vulnerable --include-transitive`.

## Default Development Accounts
`admin`, `dispatcher`, and `driver`, password `ChangeMe123!` (development only).

## API Endpoints
`POST /api/auth/login`; `GET/POST /api/vehicles`; `GET/POST /api/drivers`; `GET/POST /api/assignments`; `PATCH /api/assignments/{id}/complete`; `GET/POST /api/maintenance`; `GET /api/dashboard`.

## Folder Structure
`Models` holds entities, `Data` configures constraints, `Services` owns transactional assignment logic, `tests` exercises business rules, and `migrations` documents the schema.

## Security Notes
Passwords are hashed, JWTs are short-lived, roles and driver ownership are server enforced, EF parameterizes queries, assignment changes are transactional, and request records prevent mass assignment. Deploy behind HTTPS with production secrets and restrictive CORS.

## Known Limitations
SQLite targets local demos. GPS telemetry, route optimization, fuel cards, file uploads, and token revocation are outside the selected scope.

## License
MIT
