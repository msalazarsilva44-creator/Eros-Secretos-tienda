# 🚀 Instalación Completa - Eros Secretos

Guía completa para instalar y ejecutar el proyecto Eros Secretos (Frontend + Backend + Base de Datos).

---

## 📋 Requisitos Previos

- Node.js v18 o superior
- MySQL 8.0 o superior
- npm o yarn
- Un editor de código (VS Code recomendado)

---

## 🔧 Paso 1: Configurar la Base de Datos

### 1.1 Instalar MySQL (si no lo tienes)

**Windows:**
```bash
# Descarga desde: https://dev.mysql.com/downloads/installer/
# O usa chocolatey:
choco install mysql
```

**macOS:**
```bash
brew install mysql
brew services start mysql
```

**Linux:**
```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
```

### 1.2 Crear la Base de Datos

Ejecuta el script SQL para crear la base de datos y las tablas:

```bash
mysql -u root -p < database/schema.sql
```

Esto creará:
- ✅ Base de datos `eros_secretos`
- ✅ Tablas: users, categories, products, product_attributes, product_images
- ✅ Usuario admin por defecto
- ✅ Categorías por defecto
- ✅ Productos de ejemplo

---

## 🔧 Paso 2: Configurar el Backend

### 2.1 Ir a la carpeta del backend

```bash
cd backend
```

### 2.2 Instalar dependencias

```bash
npm install
```

### 2.3 Configurar variables de entorno

Crea un archivo `.env` en la carpeta `backend`:

```bash
# En Windows PowerShell:
copy .env.example .env

# En Linux/macOS:
cp .env.example .env
```

Edita el archivo `.env` con tus credenciales de MySQL:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=tu_contraseña_mysql
DB_NAME=eros_secretos
DB_PORT=3306

PORT=8001
NODE_ENV=development

JWT_SECRET=tu_secret_jwt_muy_seguro_cambiar_en_produccion
JWT_EXPIRES_IN=24h

CORS_ORIGIN=http://localhost:3001
```

### 2.4 Iniciar el backend

```bash
npm run dev
```

Deberías ver:
```
🚀 Servidor escuchando en http://localhost:8001
✅ Conexión a MySQL establecida
```

---

## 🎨 Paso 3: Configurar el Frontend

### 3.1 Ir a la carpeta raíz del proyecto

```bash
cd ..
```

### 3.2 Verificar que existe .env.local

Si no existe, créalo:

```bash
# En Windows:
echo VITE_API_BASE_URL=http://localhost:8001 > .env.local

# En Linux/macOS:
echo "VITE_API_BASE_URL=http://localhost:8001" > .env.local
```

### 3.3 Instalar dependencias (si no lo has hecho)

```bash
npm install
```

### 3.4 Iniciar el frontend

```bash
npm run dev
```

Deberías ver:
```
  VITE v5.4.19  ready in xxx ms

  ➜  Local:   http://localhost:3001/
```

---

## 🎉 Paso 4: Usar la Aplicación

### 4.1 Catálogo Público

Abre en tu navegador: **http://localhost:3001**

Verás el catálogo de productos público.

### 4.2 Dashboard Administrativo

1. Haz clic en el botón "Admin" en el header
2. Ingresa las credenciales:
   - **Email**: `admin@eros-secretos.com`
   - **Password**: `admin123`

3. Una vez logueado, verás el dashboard con:
   - ✅ Lista de todos los productos
   - ✅ Botón para crear nuevo producto
   - ✅ Botones para editar productos
   - ✅ Botones para eliminar productos

### 4.3 Crear un Producto

1. En el dashboard, haz clic en "Nuevo Producto"
2. Completa el formulario:
   - Nombre: Requerido
   - Descripción: Opcional
   - Precio: Requerido
   - Categoría: Requerido
   - Stock: Opcional
   - URL de Imagen: Opcional
   - Marcar como nuevo: Checkbox
   - Destacar producto: Checkbox
3. Haz clic en "Crear"

### 4.4 Editar un Producto

1. En la tabla de productos, haz clic en el ícono ✏️ (Edit)
2. Modifica los campos que desees
3. Haz clic en "Actualizar"

### 4.5 Eliminar un Producto

1. En la tabla de productos, haz clic en el ícono 🗑️ (Trash)
2. Confirma la eliminación

---

## 🏗️ Estructura del Proyecto

```
eros-secretos/
├── backend/              # Backend API (Node.js + Express + MySQL)
│   ├── config/
│   │   ├── database.js
│   │   └── auth.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── products.js
│   │   └── categories.js
│   ├── .env
│   ├── package.json
│   └── server.js
├── database/
│   └── schema.sql       # Esquema de la base de datos
├── src/                 # Frontend (React + TypeScript + Vite)
│   ├── components/
│   ├── hooks/
│   ├── pages/
│   │   ├── Index.tsx
│   │   ├── Login.tsx
│   │   └── Dashboard.tsx
│   └── ...
├── .env.local           # Variables de entorno del frontend
└── package.json
```

---

## 🔐 Credenciales por Defecto

### Usuario Admin

- **Email**: `admin@eros-secretos.com`
- **Password**: `admin123`

⚠️ **IMPORTANTE**: Cambia esta contraseña en producción.

### Cambiar Contraseña

En MySQL:

```sql
USE eros_secretos;
UPDATE users SET password = '$2y$10$NUEVA_HASH' WHERE email = 'admin@eros-secretos.com';
```

Para generar una nueva hash:

```bash
# En el backend:
npm install -g bcrypt-cli
bcrypt-hash tu_nueva_contraseña
```

---

## 🐛 Solución de Problemas

### Error: "Cannot connect to MySQL"

1. Verifica que MySQL esté corriendo:
   ```bash
   # Windows:
   net start MySQL80
   
   # macOS:
   brew services start mysql
   
   # Linux:
   sudo systemctl start mysql
   ```

2. Verifica tus credenciales en `backend/.env`

### Error: "JWT Secret must be set"

Asegúrate de que `.env` tenga el campo `JWT_SECRET`.

### Error: "EADDRINUSE: address already in use"

El puerto 8001 o 3001 ya está en uso. Detén la aplicación que lo usa o cambia el puerto en `.env`.

### Los productos no se cargan

1. Verifica que el backend esté corriendo en `http://localhost:8001`
2. Verifica que el frontend tenga la URL correcta en `.env.local`
3. Abre la consola del navegador para ver errores

---

## 📚 Documentación Adicional

- [Backend README](./backend/README.md)
- [Configuración del Frontend](./CONFIGURACION_FINAL.md)
- [Evaluación del Proyecto](./EVALUACION_PROYECTO.md)

---

## 🎯 Próximos Pasos

1. ✅ Crear más productos desde el dashboard
2. ✅ Personalizar las categorías
3. ✅ Agregar más atributos a los productos
4. ✅ Subir imágenes reales
5. ✅ Configurar variables de producción

---

## 💡 Notas

- El frontend corre en el puerto **3001**
- El backend corre en el puerto **8001**
- La base de datos MySQL debe estar en el puerto **3306**
- Todos los endpoints requieren autenticación excepto GET de productos y categorías

