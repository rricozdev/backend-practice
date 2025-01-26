# backend-practice

# **Market Management API**

## **📌 OBJETIVOS**

- Construir una API Restful utilizando **Node.js**, **Express**, y **Sequelize**.
- Practicar la conexión y manejo de bases de datos relacionales (PostgreSQL).
- Implementar un sistema básico para la gestión de productos, tiendas y promociones.
- Familiarizarse con buenas prácticas de desarrollo backend.

---

## **⏱ REQUISITOS PREVIOS**

Es necesario contar con las siguientes versiones de herramientas instaladas en tu entorno:

- **Node.js**: 16.0.0 o superior
- **NPM**: 7.10.0 o superior
- **PostgreSQL**: 13.0 o superior

Para verificar que tienes las versiones correctas:

```bash
node -v
npm -v
psql --version
```

---

## **📋 INSTRUCCIONES PARA INICIAR**

1. **Clonar el repositorio**:

   ```bash
   git clone <URL del repositorio>
   cd <nombre-del-repositorio>
   ```

2. **Instalar dependencias**:

   ```bash
   npm install
   ```

3. **Configurar las variables de entorno**:

   Crea un archivo `.env` en la carpeta principal del proyecto con el siguiente contenido:

   ```env
   DB_USER=tu_usuario_postgres
   DB_PASSWORD=tu_contraseña_postgres
   DB_HOST=localhost
   DB_NAME=market
   DB_PORT=5432
   ```

   Reemplaza los valores según tu configuración local.

4. **Configurar la base de datos**:

   - Crea la base de datos `market` utilizando PostgreSQL:

     ```bash
     psql -U <tu_usuario_postgres> -c "CREATE DATABASE market;"
     ```

   - Ejecuta las migraciones para crear las tablas:

     ```bash
     npx sequelize-cli db:migrate
     ```

   - Si deseas cargar datos iniciales, puedes usar los seeders:

     ```bash
     npx sequelize-cli db:seed:all
     ```

5. **Levantar el servidor**:

   ```bash
   npm start
   ```

   El servidor estará disponible en `http://localhost:3001`.

---

## **🖱 MODELOS**

### **📍 Product**

- `id`: Identificador único (autogenerado).
- `name`: Nombre del producto (obligatorio).
- `price`: Precio del producto (obligatorio).

### **📍 Store**

- `id`: Identificador único (autogenerado).
- `name`: Nombre de la tienda (obligatorio).
- `location`: Ubicación de la tienda.

### **📍 ProductStock**

- `id`: Identificador único (autogenerado).
- `productId`: Relación con un producto (obligatorio).
- `storeId`: Relación con una tienda (obligatorio).
- `quantity`: Cantidad de stock disponible (obligatorio).

### **📍 Promotion**

- `id`: Identificador único (autogenerado).
- `name`: Nombre de la promoción (obligatorio).
- `daysApplicable`: Días de la semana en que aplica (array, obligatorio).
- `startDate`: Fecha de inicio (obligatorio).
- `endDate`: Fecha de fin (obligatorio).

---

## **🖱 ENDPOINTS**

### **📍 GET | /products**
- Descripción: Obtiene una lista de productos con su información básica y stock en cada tienda.
- Respuesta:
  ```json
  [
    {
      "id": 1,
      "name": "Laptop",
      "price": 1200,
      "stocks": [
        {
          "storeId": 1,
          "quantity": 10
        },
        {
          "storeId": 2,
          "quantity": 5
        }
      ]
    }
  ]
  ```

### **📍 GET | /products/top**
- Descripción: Obtiene los 5 productos más vendidos en orden descendente (simulado).
- Respuesta:
  ```json
  [
    { "id": 1, "name": "Laptop", "sales": 150 },
    { "id": 2, "name": "Phone", "sales": 120 }
  ]
  ```

### **📍 GET | /categories**
- Descripción: Lista categorías con al menos un producto, ordenadas por cantidad de productos.
- Respuesta:
  ```json
  [
    { "category": "Electronics", "productCount": 50 },
    { "category": "Books", "productCount": 30 }
  ]
  ```

### **📍 GET | /promotions/:day**
- Descripción: Lista las promociones activas en un día específico, junto con las tiendas participantes.
- Parámetro: `day` (número del día de la semana, donde 1 = Lunes, 7 = Domingo).
- Respuesta:
  ```json
  [
    {
      "id": 1,
      "name": "Black Friday Sale",
      "stores": [
        { "id": 1, "name": "Downtown Store" },
        { "id": 2, "name": "Mall Store" }
      ]
    }
  ]
  ```

---

## **📂 ESTRUCTURA DEL PROYECTO**

```
├── api
│   ├── models
│   ├── routes
│   ├── controllers
│   ├── migrations
│   ├── seeders
│   └── app.js
├── .env
├── package.json
└── README.md
```



