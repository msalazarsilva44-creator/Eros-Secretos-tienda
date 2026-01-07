# 🗄️ Instalar MySQL y Configurar la Base de Datos

Para usar el sistema con persistencia de datos real, necesitas instalar MySQL:

## 📦 Opción 1: Instalar con Chocolatey (Windows)

```bash
choco install mysql
```

Luego inicia el servicio:
```bash
net start MySQL80
```

## 📦 Opción 2: Instalar Manualmente

1. Descarga MySQL desde: https://dev.mysql.com/downloads/installer/
2. Instala MySQL Server
3. Durante la instalación, crea una contraseña para root

## 🔧 Configurar la Base de Datos

### 1. Crear la base de datos

Ejecuta este comando (reemplaza `tu_contraseña` con la contraseña de root):

```bash
mysql -u root -p < database/schema.sql
```

Si no tienes contraseña:
```bash
mysql -u root < database/schema.sql
```

### 2. Actualizar el archivo .env

Edita `backend/.env` y cambia:

```env
DB_PASSWORD=tu_contraseña_mysql
```

### 3. Reiniciar el servidor

```bash
cd backend
npm run dev
```

Ahora el sistema usará MySQL real en lugar de datos mock.

---

**Nota**: Si tienes problemas instalando MySQL, el sistema funciona perfectamente en modo demo con `server-simple.js` 😊

