# multi-tenant-system

# SaaS MultiRubro - Gestión Integral de Negocios

Plataforma SaaS para la gestión integral de **bares, boliches, salones de fiesta, restaurantes y sedes múltiples**, con control de personal, stock, reservas, caja, mantenimiento, proveedores, alquileres y contrataciones externas.

El sistema está diseñado como **backend monolítico modular**, preparado para una futura **migración progresiva a microservicios** sin reescrituras.

---

## 🎯 Objetivo del Proyecto

Construir una plataforma **escalable, segura y multi-tenant** que permita a una misma empresa gestionar múltiples locales (sedes) de distinto rubro desde un solo sistema, con control total por roles y sectores.

---

## 🧠 Principios de Arquitectura

* Monolito **100% modular**
* Separación estricta de capas:

  * Controller
  * Service
  * Repository
  * Entity
  * DTO
* Sin lógica de negocio en controllers
* Sin acceso directo a tablas entre módulos
* Preparado para **Strangler Pattern** (migración a microservicios)
* Versionado de API por rutas (`/api/v1`)

---

## 🧩 Módulos del Sistema

### Módulos Base

* Autenticación y autorización
* Usuarios
* Empresas
* Sedes (bares, boliches, salones, restaurantes)
* Roles y permisos
* Auditoría y logs
* Archivos (contratos, comprobantes, imágenes)

### Módulos Operativos

* Stock
* Depósito
* Proveedores
* Caja
* Reservas y eventos
* Mantenimiento
* Limpieza
* Equipo técnico
* Contratación de terceros
* Alquiler de mobiliario

---

## 👥 Roles del Sistema

* Super Admin Plataforma
* Admin Empresa
* Encargado
* Subencargado
* Empleado
* Técnico
* Limpieza
* Depósito
* Proveedor
* Tercero contratado

Cada usuario puede:

* Estar asignado a una o varias sedes
* Tener distintos roles por sede

---

## 🗺️ Roadmap de Desarrollo

### Etapa 0 – Fundación Técnica

* Arquitectura base
* Seguridad JWT
* Versionado API v1
* Estructura de módulos vacía

### Etapa 1 – MVP Vendible

* Multiempresa y multisede
* Roles base
* Stock básico
* Reservas
* Caja simple
* Panel web administrativo

### Etapa 2 – Post-MVP

* Mantenimiento, limpieza, proveedores
* Alquileres
* Seguridad avanzada
* Versión desktop

### Etapa 3 – Escalabilidad

* Versión mobile
* Primeros microservicios (auth, pagos, notificaciones)

### Etapa 4 – Producto Empresarial

* Business Intelligence
* Facturación
* Integraciones externas
* IA

---

## 🔐 Seguridad

* Autenticación JWT
* Refresh tokens
* Protección por CORS
* Validación de roles por endpoint
* Auditoría completa por acción
* Bloqueo por IP y rate-limit (futuro)

---

## 🔀 Versionado de API

* Solo 1 versión activa al inicio: `v1`
* Máximo 2 versiones públicas simultáneas:

  * 1 activa
  * 1 deprecada
* La siguiente versión solo existe en entorno de desarrollo
* Eliminación controlada por tráfico y migración total

---

## 🏗️ Stack Tecnológico

### Backend

* Java
* Spring Boot

### Base de Datos

* MySQL

### Frontend

* React

### Desktop

* Electron

### Mobile

* Capacitor

---

## ⚙️ Configuración del Proyecto

### Variables de Entorno

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=saas_multirubro
DB_USER=root
DB_PASSWORD=secret
JWT_SECRET=supersecretkey
JWT_EXPIRATION=86400
```

---

## ▶️ Ejecución del Proyecto

### Backend

```bash
mvn spring-boot:run
```

### Frontend

```bash
npm install
npm run dev
```

---

## 📄 Documentación del Proyecto

* Documentación funcional por módulo
* Documentación de arquitectura
* Swagger / OpenAPI para endpoints
* Convenciones internas de desarrollo

---

## 🤝 Contribución

1. Crear rama feature
2. Commits claros
3. Pull request documentado
4. Revisión obligatoria antes del merge

---

## 📜 Licencia

Este proyecto es privado. Su uso, distribución o comercialización sin autorización está prohibida.

---

## 🚀 Estado del Proyecto

🔧 En desarrollo activo – Fase de arquitectura y definición de MVP
