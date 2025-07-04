# Inventory-Management_Api

A robust ASP.NET Core Web API for managing products, categories, and suppliers with JWT authentication and role-based access control.

---

## 🚀 Features
- Product, Category, and Supplier management
- User registration and login with JWT authentication
- Role-based authorization (Admin/User)
- Image upload and management functionality
- Swagger UI for API exploration
- Secure configuration management
- Entity Framework Core with SQL Server

---

## 🛠️ Getting Started

### 1. **Clone the Repository**
```bash
git clone <your-repo-url>
cd InventoryManagementAPI
```

### 2. **Configuration**
- **DO NOT** commit secrets to git!
- Copy the template config files and fill in your own secrets:

```bash
cp appsettings.json appsettings.json.local
cp appsettings.Development.json.template appsettings.Development.json
```

- Edit `appsettings.Development.json` and set:
  - Your database connection string
  - JWT Key, Issuer, Audience

#### Example:
```json
"Jwt": {
  "Key": "your-very-secret-key",
  "Issuer": "https://localhost:7186/",
  "Audience": "https://localhost:7186/",
  "ExpiresInMinutes": 60
}
```

### 3. **Restore Dependencies**
```bash
dotnet restore
```

### 4. **Run Database Migrations**
```bash
dotnet ef database update
```

### 5. **Run the API**
```bash
dotnet run
```

- The API will be available at `https://localhost:7186`
- Swagger UI: `https://localhost:7186/swagger`

---

## 📚 API Usage Examples

### Authentication
- **Register User**
  ```http
  POST /api/auth/register
  Content-Type: application/json

  {
    "username": "string",
    "email": "string",
    "password": "string"
  }
  ```

- **Login**
  ```http
  POST /api/auth/login
  Content-Type: application/json

  {
    "email": "string",
    "password": "string"
  }
  ```

### Products
- **Get All Products**
  ```http
  GET /api/product
  Authorization: Bearer {token}
  ```

- **Get Product by ID**
  ```http
  GET /api/product/{id}
  Authorization: Bearer {token}
  ```

- **Create Product**
  ```http
  POST /api/product
  Authorization: Bearer {token}
  Content-Type: application/json

  {
    "name": "string",
    "description": "string",
    "price": 0,
    "quantity": 0,
    "categoryId": "guid",
    "supplierId": "guid"
  }
  ```

### Categories
- **Get All Categories**
  ```http
  GET /api/category
  Authorization: Bearer {token}
  ```

- **Create Category**
  ```http
  POST /api/category
  Authorization: Bearer {token}
  Content-Type: application/json

  {
    "name": "string",
    "description": "string"
  }
  ```

### Suppliers
- **Get All Suppliers**
  ```http
  GET /api/supplier
  Authorization: Bearer {token}
  ```

- **Create Supplier**
  ```http
  POST /api/supplier
  Authorization: Bearer {token}
  Content-Type: application/json

  {
    "name": "string",
    "contactPerson": "string",
    "email": "string",
    "phone": "string",
    "address": "string"
  }
  ```

### Images
- **Upload Image**
  ```http
  POST /api/images/upload
  Authorization: Bearer {token}
  Content-Type: multipart/form-data

  {
    "file": [binary file],
    "description": "string"
  }
  ```

- **Get Image by ID**
  ```http
  GET /api/images/{id}
  Authorization: Bearer {token}
  ```

- **Get All Images**
  ```http
  GET /api/images
  Authorization: Bearer {token}
  ```

- **Delete Image**
  ```http
  DELETE /api/images/{id}
  Authorization: Bearer {token}
  ```

---

## 👥 Admin & User Usage

### Admin Role
- Admins have full access to all endpoints.
- They can create, update, and delete products, categories, and suppliers.
- Admins can manage user roles and access.

### User Role
- Regular users can view products, categories, and suppliers.
- They cannot modify or delete data.
- Users can only access endpoints marked as public or user-accessible.

---

## 🔒 Security & Best Practices
- **Never commit real secrets or connection strings.**
- Use the `.template` files for sharing config structure.
- Use environment variables or [dotnet user-secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) for local development.
- Enforce HTTPS in production.
- Store images securely in the wwwroot/images directory.
- Validate image file types and sizes before upload.

---

## 🧪 Testing
- Run all tests:
```bash
dotnet test
```

---

## 📦 Deployment
- Set environment variables for all secrets in production.
- Use `appsettings.Production.json.template` for structure.
- Consider Docker for containerized deployment.

---

## 🤝 Contributing
1. Fork the repo
2. Create a feature branch
3. Commit your changes
4. Open a pull request

---
