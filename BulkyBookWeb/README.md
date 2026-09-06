# BulkyBook 

ASP.NET Core MVC + Entity Framework Core project notes.

## Environment

- Visual Studio 2026
- .NET 10.0
- SQL Server Express
- SQL Server instance: `DESKTOP-XXXX\SQLEXPRESS`

> Replace `DESKTOP-XXXX\SQLEXPRESS` with the actual SQL Server instance name on your machine.


Right click BulkyBookWeb -> Edit Project file

## NuGet Packages

Install these packages:

```text
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Tools
```

Use versions compatible with .NET 8 / EF Core 8.

### What they are for

- `Microsoft.EntityFrameworkCore.SqlServer`
  - Enables EF Core to connect to SQL Server.
- `Microsoft.EntityFrameworkCore.Tools`
  - Provides Package Manager Console commands such as `Add-Migration` and `Update-Database`.

## Project Structure

```text
EmployeeManagementSystem
│
├── Controllers
│   ├── HomeController.cs
│   └── EmployeeController.cs
│
├── Data
│   └── AppDbContext.cs
│
├── Models
│   ├── Base
│   │   └── BaseEntity.cs
│   │
│   ├── Entities
│   │   ├── Employee.cs
│   │   ├── Department.cs
│   │   ├── User.cs
│   │   └── Role.cs
│   │
│   └── ViewModels
│
├── Views
├── wwwroot
├── Program.cs
├── appsettings.json
└── Migrations
```

## EF Core Commands

Open:

**Tools → NuGet Package Manager → Package Manager Console**

### 1. Create a migration

```powershell
Add-Migration InitialCreate
```

This creates a migration based on the current EF Core entity/model configuration.

### 2. Apply the migration to SQL Server

```powershell
Update-Database
```

This creates/updates the database according to the migration.

### Typical workflow after changing an Entity

```text
Modify Entity
    ↓
Add-Migration MigrationName
    ↓
Update-Database
```

Example:

```powershell
Add-Migration AddEmployeeAddress
Update-Database
```

```powershell
Add-Migration SeedDepartments
Update-Database
```

## Database

Database name:

```text
EmployeeManagementDb
```

Expected initial tables:

```text
dbo.Employees
dbo.Departments
dbo.Users
dbo.Roles
dbo.__EFMigrationsHistory
```

`__EFMigrationsHistory` is maintained by EF Core to track which migrations have been applied.

## Connection String

`appsettings.json`:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=DESKTOP-XXXX\\SQLEXPRESS;Database=EmployeeManagementDb;Trusted_Connection=True;TrustServerCertificate=True;"
}
```

Replace the server name with the actual SQL Server instance.

## Important Design Decisions

### EmployeeCode

Employee codes use a business-friendly format such as:

```text
E001
E002
E003
```

`EmployeeCode` should be unique.

### Audit fields

`BaseEntity` contains:

```text
Id
CreatedDate
CreatedByUserId
UpdatedDate
UpdatedByUserId
```

`CreatedByUserId` / `UpdatedByUserId` are intended to identify the login user who created or last updated a record.

### Relationships

```text
Department 1 ──── * Employee

Employee   1 ──── 1 User

Role       1 ──── * User
```

`DepartmentId`, `EmployeeId`, and `RoleId` are used as foreign-key fields for these relationships.

## Current Learning Roadmap

1. ASP.NET Core MVC foundation
2. Entity design
3. EF Core setup
4. Entity relationships
5. EF Core migrations
6. SQL Server database
7. CRUD
8. Service layer
9. Repository pattern
10. DTO / ViewModel
11. Validation
12. Authentication
13. Authorization
14. Audit handling
15. Logging
16. Error handling
17. API
18. React frontend (later)

## Useful Visual Studio Shortcuts

```text
Ctrl + Shift + B  → Build Solution
F5                → Run with Debugging
Ctrl + F5         → Run without Debugging
Ctrl + K -> Ctrl + D -> Format Document
Ctrl + K -> Ctrl + F -> Format Selection
```

## Current Status

- [x] ASP.NET Core MVC project created
- [x] Entity models created
- [x] BaseEntity created
- [x] EF Core SQL Server packages installed
- [x] AppDbContext created
- [x] Connection string configured
- [x] DbContext registered in Program.cs
- [x] Entity relationships configured
- [x] Build succeeded
- [x] Initial migration
- [x] Update database
- [x] Seed Departments
- [x] CRUD

