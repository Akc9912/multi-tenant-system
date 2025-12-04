# SaaS MultiRubro - Gestión Integral de Negocios

Plataforma SaaS para la gestión integral de **negocios de cualquier rubro** (bares, boliches, salones de fiesta, restaurantes, barbería, salones de belleza, clínicas, y más) con **punto de venta**, **gestión de turnos**, control de personal, stock, reservas, caja, mantenimiento, proveedores, alquileres y contrataciones externas.

El sistema está diseñado como **backend monolítico modular**, preparado para una futura **migración progresiva a microservicios** sin reescrituras.

> **📚 Documentación completa**: Ver [docs/INDEX.md](./docs/INDEX.md)  
> **🏗️ Arquitectura del sistema**: [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md)  
> **📊 Desarrollo**: [docs/ROADMAP.md](./docs/ROADMAP.md) | [Backend](./docs/ROADMAP_BACKEND.md) | [Frontend](./docs/ROADMAP_FRONTEND.md) | [DevOps](./docs/ROADMAP_DEVOPS.md)  
> **👥 Contribuir**: [docs/CONTRIBUTING.md](./docs/CONTRIBUTING.md)  
> **🛠️ Stack & Prácticas**: [docs/STACK_Y_PRACTICAS.md](./docs/STACK_Y_PRACTICAS.md)

---

## 🎯 Objetivo del Proyecto

Construir una plataforma **escalable, segura y multi-tenant** que permita a empresas de **cualquier tamaño y rubro** gestionar múltiples locales (sedes) desde un solo sistema. Desde pequeñas barbería y salones de belleza, hasta grandes restaurantes y cadenas de negocios, con control total por roles, sectores, y capacidades de punto de venta integrado.

---

## 🏢 Casos de Uso

La plataforma está diseñada para servir a:

* **Pequeños negocios** - Barberías, salones de belleza, peluquerías, spa
* **Servicios y citas** - Clínicas, consultorios, centros de estética, estudios
* **Gastronomía** - Restaurantes, bares, cafeterías, cantinas, parrillas
* **Entretenimiento** - Boliches, salones de fiesta, discotecas
* **Comercios minoristas** - Tiendas, boutiques, farmacias
* **Cadenas multilocal** - Cualquier negocio con múltiples sucursales y diferentes rubros integrados

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
* Usuarios y perfiles
* Empresas
* Sedes (bares, restaurantes, barbería, salones de belleza, clínicas, comercios, etc.)
* Roles y permisos avanzados
* Auditoría y logs
* Archivos (contratos, comprobantes, imágenes)

### Módulos Operativos

* **Punto de Venta (POS)** - Sistema completo de ventas
* **Gestión de Turnos** - Agendamientos para servicios y atención
* Stock e Inventario
* Depósito
* Proveedores
* Caja y pagos
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
* Encargado de sucursal
* Subencargado
* Empleado / Operario
* Vendedor / Cajero
* Profesional (barbero, peluquero, esteticien, etc.)
* Técnico
* Personal de limpieza
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

Incluye todas las capacidades esenciales para ser **inmediatamente vendible a pequeños y medianos negocios**:

* Multiempresa y multisede
* Roles y permisos granulares
* **Punto de Venta (POS)** - Transacciones, productos, clientes, recibos
* **Gestión de Turnos** - Agendamientos, profesionales, servicios, disponibilidad
* Stock e inventario básico
* Reservas y eventos
* Caja integrada con múltiples formas de pago
* Panel web administrativo intuitivo
* Reportes de ventas y operaciones básicos

### Etapa 2 – Post-MVP

* **Punto de Venta avanzado** (promociones, descuentos, combos, integraciones de pago)
* **Gestión de Turnos mejorada** (recordatorios, cancelaciones, no-shows, historial)
* Mantenimiento, limpieza, proveedores
* Alquileres
* Seguridad avanzada
* Versión desktop (POS de escritorio)

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

## ��� Estado del Proyecto

��� En desarrollo activo – Fase de arquitectura y definición de MVP
