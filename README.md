# 📘 ASP.NET Core Social Media App (Database-First Approach)

This project is a simple **Social Media** web application built using **ASP.NET Core MVC** and the **Database-First** approach. It allows users to register and create posts.

---

## 🛠️ Prerequisites

Ensure you have the following installed:

- **.NET SDK** (Check with: `dotnet --version`)
- **SQL Server** (Express or Full Edition)
- **Entity Framework Core Tools**

---

## 📂 Project Setup

### 1. Create the project
```bash
cd YourProjectFolder
```

### 2. Restore Dependencies
```bash
dotnet restore
```

This downloads all required NuGet packages.

### 3. Ensure Entity Framework Core Tools Are Installed
```bash
dotnet tool install -- global donet-ef
dotnet tool install -g dotnet-aspnet-codegenerator
dotnet add package Microsoft.EntityFrameworkCore.Tools
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
```

The first two commands install the `dotnet-ef and dotnet-aspnet-codegenerator` tool globally. The other two add the necessary EF Core packages.

---

## 🗄️ Database Setup (Database-First Approach)

### 1. Ensure Your Database Exists
Create a database in SQL Server. For example:

```sql
CREATE DATABASE fakebookDb;
```

### 2. Scaffold Models from the Database
```bash
dotnet ef dbcontext scaffold "Server=YOUR_SERVER;Database=fakebookDb;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Models
```

✅ **What this does:**
- **Generates** your models (tables) in the `Models` folder.
- **Creates** a `DbContext` class to interact with the database.

### 3. Verify the DbContext
Ensure your `FakebookDbContext` is present in the `Models` directory. Example:

```csharp
public class FakebookDbContext : DbContext
{
    public DbSet<User> Users { get; set; }
    public DbSet<Post> Posts { get; set; }

    public FakebookDbContext(DbContextOptions<FakebookDbContext> options) : base(options) { }
}
```

---

## 📊 Scaffold Controllers and Views

### 1. Scaffold User Controller
```bash
dotnet aspnet-codegenerator controller -name UserController -m User -dc FakebookDbContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries
```

### 2. Scaffold Post Controller
```bash
dotnet aspnet-codegenerator controller -name PostController -m Post -dc FakebookDbContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries
```

✅ **What this does:**
- **Creates** `UserController` and `PostController` inside the `Controllers` folder.
- **Generates** basic CRUD (Create, Read, Update, Delete) operations.
- **Adds** views for User and Post in the `Views` folder.

---

## 🧭 Update Navigation Bar

Ensure the following links are present in `Views/Shared/_Layout.cshtml`:

```html
<li class="nav-item">
    <a class="nav-link" asp-controller="User" asp-action="Create">Create User</a>
</li>
<li class="nav-item">
    <a class="nav-link" asp-controller="Post" asp-action="Create">Create Post</a>
</li>
```

---

## 🚀 Run the Application

### 1. Apply Database Connection
Ensure your `appsettings.json` is configured correctly:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=YOUR_SERVER;Database=fakebookDb;Trusted_Connection=True;"
}
```

### 2. Start the Application
```bash
dotnet run
```

✅ Navigate to `http://localhost:5000` or the port displayed in your terminal.

---

## 📋 Folder Structure Overview

```
YourProject/
├── Controllers/         # MVC Controllers (User, Post)
├── Models/              # Database Models (User, Post, DbContext)
├── Views/               # UI Pages (Create, Edit, Delete)
│   ├── Shared/          # Layout and Navbar
│   ├── User/            # User Views
│   └── Post/            # Post Views
├── appsettings.json     # Configuration (DB connection)
└── Program.cs           # App Entry Point
```

---

## 🔎 Troubleshooting

1. **Command Not Found?**
Ensure the correct tools are installed:

```bash
dotnet tool install -g dotnet-aspnet-codegenerator
```

2. **Scaffold Error?**
Check the database connection and ensure `FakebookDbContext` is correct.

3. **Database Connection Issue?**
Ensure your `Server` and `Database` values are correct.

---

## 📌 Next Steps

1. Add user authentication with Identity.
2. Improve the UI with Bootstrap.
3. Implement post likes and comments.

Feel free to extend the app further! 🚀
