# ��️ Arquitectura del Sistema - SaaS MultiRubro

## Visión General

SaaS MultiRubro es un **monorepo** que contiene backend, frontend y DevOps. El backend está diseñado como un **monolito modular** que puede evolucionar a microservicios sin cambios mayores.

---

## ��� Estructura Monorepo

```
multi-tenant-system/
├── backend/                          # Java Spring Boot
│   ├── src/main/java/com/multitenant/
│   │   ├── auth/                    # Módulo autenticación
│   │   ├── company/                 # Módulo empresas
│   │   ├── branch/                  # Módulo sedes
│   │   ├── user/                    # Módulo usuarios
│   │   ├── product/                 # Módulo productos
│   │   ├── sale/                    # Módulo ventas (POS)
│   │   ├── appointment/             # Módulo turnos
│   │   ├── stock/                   # Módulo inventario
│   │   ├── shared/                  # Código compartido
│   │   └── Application.java
│   ├── pom.xml
│   └── Dockerfile
│
├── frontend/                         # React + TypeScript
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   ├── context/
│   │   └── App.tsx
│   ├── package.json
│   └── Dockerfile
│
├── docs/
│   ├── CHANGELOG.md
│   ├── CONTRIBUTING.md
│   ├── ARCHITECTURE.md (este archivo)
│   ├── ROADMAP.md
│   ├── ROADMAP_BACKEND.md
│   ├── ROADMAP_FRONTEND.md
│   ├── ROADMAP_DEVOPS.md
│   └── STACK_Y_PRACTICAS.md
│
├── docker-compose.yml
├── .github/workflows/
├── README.md
└── [otros archivos]
```

---

## Backend: Arquitectura Modular

### Capas

```
Controller (REST API) → DTOs
    ↓
Service (Lógica de negocio)
    ↓
Repository (Acceso a datos)
    ↓
Entity/DAO (Modelo de datos)
```

### Módulos (MVP)

| Módulo | Responsabilidad |
|--------|-----------------|
| **auth** | JWT, roles, permisos |
| **company** | Gestión de empresas |
| **branch** | Gestión de sedes |
| **user** | Usuarios de sistema |
| **product** | Catálogo de productos |
| **sale** | Punto de venta (POS) |
| **appointment** | Gestión de turnos |
| **stock** | Inventario |
| **shared** | Código reutilizable |

### Principios

- ✅ Módulos independientes
- ✅ Sin acceso directo entre BDs
- ✅ DTOs para transferencia
- ✅ Services orquestan lógica
- ✅ Validación en Service, no Controller

---

## Frontend: Componentes

```
components/
├── common/           # Reutilizables
├── features/         # Por dominio
└── layouts/          # Layouts principales

pages/               # Páginas de rutas
hooks/               # Custom hooks
services/            # API calls
context/             # Estado global
utils/               # Funciones auxiliares
styles/              # Estilos globales
```

### Patrones

- ✅ React.FC funcionales
- ✅ Custom hooks para lógica
- ✅ Context API para estado global
- ✅ TypeScript obligatorio
- ✅ Lazy loading de rutas

---

## ��� Multi-Tenancy

### Data-Level Isolation

```
Company A          Company B
├─ Branch 1        ├─ Branch 1
├─ Branch 2        └─ Branch 2
└─ Users           └─ Users
```

Cada query automáticamente filtra por:
```sql
WHERE company_id = ?
AND branch_id IN (?)
```

---

## ��� Escalabilidad: Monolito → Microservicios

La arquitectura está lista para evolucionar:

```
Fase 1: Monolito              Fase 2: Microservicios
┌─────────────────────┐       ┌──────────────────────┐
│ Backend Monolítico  │       │ Auth Service (μS)    │
│ ├─ Auth             │───→   │ Payment Service (μS) │
│ ├─ Sale             │       │ Backend Monolito     │
│ ├─ Appointment      │       │ ├─ Sale              │
│ └─ ...              │       │ ├─ Appointment       │
└─────────────────────┘       │ └─ ...               │
                              └──────────────────────┘
```

---

## ��� Flujos Principales

### 1. Autenticación (JWT)

Login → Valida BD → JWT token → Contexto multi-tenant → Request

### 2. Venta (POS)

Selecciona productos → Sale Service → Decrementa stock → Procesa pago → Recibo

### 3. Turno

Solicita disponibilidad → Crea turno → Confirmación → Recordatorio

---

## ��� Ver También

- [CONTRIBUTING.md](./CONTRIBUTING.md) - Convenciones de código
- [ROADMAP.md](./ROADMAP.md) - Fases de desarrollo
- [STACK_Y_PRACTICAS.md](./STACK_Y_PRACTICAS.md) - Stack y buenas prácticas

