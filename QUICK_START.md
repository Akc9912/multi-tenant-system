# 🚀 Quick Start - SaaS MultiRubro

Guía rápida para comenzar a trabajar en el proyecto.

---

## 📖 Lectura Recomendada

1. **Este archivo** (Quick Start) ← Estás aquí
2. [INDEX.md](./docs/INDEX.md) - Navegación de documentación
3. [CONTRIBUTING.md](./docs/CONTRIBUTING.md) - Cómo contribuir
4. [ARCHITECTURE.md](./docs/ARCHITECTURE.md) - Estructura del proyecto

---

## 🎯 ¿Qué es SaaS MultiRubro?

**Plataforma SaaS** para gestionar negocios de **cualquier rubro** (restaurantes, barbería, salones, clínicas, etc.) con:

- 🛒 **Punto de Venta (POS)** - Sistema completo de ventas
- 📅 **Gestión de Turnos** - Agendamientos y citas
- 📦 **Control de Stock** - Inventario y movimientos
- 💼 **Multi-tenant** - Múltiples empresas, múltiples sedes
- 🔐 **Seguridad** - Autenticación JWT, aislamiento de datos

**Arquitectura**: Monorepo modular (backend + frontend + docs) preparado para evolucionar a microservicios.

---

## 🏗️ Estructura del Proyecto

```
multi-tenant-system/
├── backend/              # Java/Spring Boot (9 módulos)
│   ├── auth/            # Autenticación y autorización
│   ├── company/         # Gestión de empresas
│   ├── branch/          # Gestión de sedes
│   ├── user/            # Gestión de usuarios
│   ├── product/         # Catálogo de productos
│   ├── sale/            # Sistema POS
│   ├── appointment/     # Gestión de turnos
│   ├── stock/           # Inventario
│   └── shared/          # Utilidades compartidas
│
├── frontend/            # React/TypeScript
│   ├── components/      # Componentes reutilizables
│   ├── pages/           # Páginas de la aplicación
│   ├── services/        # APIs calls
│   ├── hooks/           # Custom React hooks
│   └── store/           # Redux state management
│
├── docs/                # Documentación
│   ├── README.md        # Este archivo
│   ├── INDEX.md         # Centro de navegación
│   ├── ARCHITECTURE.md  # Estructura del sistema
│   ├── ROADMAP.md       # Roadmap general (5 fases)
│   ├── ROADMAP_BACKEND.md
│   ├── ROADMAP_FRONTEND.md
│   ├── ROADMAP_DEVOPS.md
│   ├── STACK_Y_PRACTICAS.md
│   ├── CONTRIBUTING.md  # Cómo contribuir
│   └── CHANGELOG.md     # Historial de cambios
│
└── docker-compose.yml   # Local development stack
```

---

## 🛠️ Stack Tecnológico

### Backend

```
Java 17+ | Spring Boot 3.0+ | MySQL 8.0+ | JUnit 5 | Mockito
```

### Frontend

```
React 18+ | TypeScript | Vite | Redux | Material-UI | Jest | Cypress
```

### DevOps

```
Docker | GitHub Actions | Kubernetes (Phase 2+) | Prometheus
```

---

## ⚡ Setup Inicial (5 minutos)

### Requisitos

- Git
- Docker & Docker Compose
- Java 17+
- Node.js 18+ LTS

### Paso 1: Clonar el repositorio

```bash
git clone <repository-url>
cd multi-tenant-system
```

### Paso 2: Configurar variables de entorno

```bash
# Backend
cd backend
cp .env.example .env.development

# Frontend
cd ../frontend
cp .env.example .env.development
```

### Paso 3: Levantar los servicios

```bash
# Desde la raíz del proyecto
docker-compose up -d

# Esto inicia:
# - MySQL 8.0
# - Redis (opcional)
# - Backend en http://localhost:8080
# - Frontend en http://localhost:3000
```

### Paso 4: Verificar que todo funciona

```bash
# Backend
curl http://localhost:8080/api/v1/health

# Frontend (en navegador)
http://localhost:3000
```

---

## 👥 Roles y Responsabilidades

### Backend Developer

**Stack**: Java 17+, Spring Boot 3.0+, MySQL

**Carpetas principales**:

```
backend/
├── src/main/java/com/multirubro/
│   ├── auth/         ← trabajar aquí
│   ├── sale/
│   ├── appointment/
│   └── shared/
└── src/test/java/   ← tests aquí
```

**Tareas típicas**:

- Implementar nuevos endpoints
- Crear servicios de negocio
- Escribir tests (80%+ coverage)
- Optimizar queries

**Ver**: [ROADMAP_BACKEND.md](./docs/ROADMAP_BACKEND.md)

### Frontend Developer

**Stack**: React 18+, TypeScript, Redux, Material-UI

**Carpetas principales**:

```
frontend/
├── src/
│   ├── components/    ← componentes reutilizables
│   ├── pages/         ← páginas (Dashboard, POS, etc)
│   ├── hooks/         ← custom hooks
│   ├── services/      ← API calls
│   └── store/         ← Redux
└── tests/             ← tests aquí
```

**Tareas típicas**:

- Crear/mantener componentes
- Implementar páginas
- Gestionar estado con Redux
- Tests (80%+ coverage)

**Ver**: [ROADMAP_FRONTEND.md](./docs/ROADMAP_FRONTEND.md)

### DevOps / Infrastructure

**Stack**: Docker, GitHub Actions, Kubernetes (Phase 2+)

**Responsabilidades**:

- CI/CD pipelines
- Infrastructure as Code
- Monitoreo y alerting
- Deployments

**Ver**: [ROADMAP_DEVOPS.md](./docs/ROADMAP_DEVOPS.md)

---

## 📋 Git Workflow

### Crear una nueva feature

```bash
# 1. Actualizar develop
git checkout develop
git pull origin develop

# 2. Crear feature branch
git checkout -b feature/nombre-feature

# 3. Hacer cambios y commit
git add .
git commit -m "feat: descripción de la feature"

# 4. Push y crear Pull Request
git push origin feature/nombre-feature
```

### Tipos de commits (Conventional Commits)

```bash
feat:      nueva feature
fix:       bug fix
docs:      cambios en documentación
style:     cambios de formato/estilo
refactor:  refactorización de código
perf:      mejora de performance
test:      tests
chore:     tareas de mantenimiento
ci:        cambios en CI/CD
```

**Ejemplo**:

```bash
git commit -m "feat(pos): agregar descuento a ventas"
git commit -m "fix(auth): corregir validación JWT"
git commit -m "docs: actualizar ROADMAP"
```

### PR Checklist

Antes de crear un Pull Request:

- [ ] Código sigue el style guide
- [ ] Tests pasan y coverage > 80%
- [ ] No hay console errors/warnings
- [ ] Documentación actualizada (si aplica)
- [ ] CHANGELOG actualizado (si es release)
- [ ] Commit messages siguen Conventional Commits

---

## 🧪 Testing

### Backend (Java)

```bash
cd backend

# Correr todos los tests
mvn test

# Tests de un módulo específico
mvn test -pl :sale

# Ver cobertura
mvn jacoco:report
# Abrir: target/site/jacoco/index.html
```

**Target**: 80%+ coverage

### Frontend (React)

```bash
cd frontend

# Correr todos los tests
npm test

# Tests en modo watch
npm test -- --watch

# Coverage report
npm test -- --coverage
# Abrir: coverage/lcov-report/index.html
```

**Target**: 80%+ coverage

---

## 🔍 Code Quality

### Backend

```bash
cd backend

# Lint / Checkstyle
mvn checkstyle:check

# SonarQube analysis (requiere servidor SonarQube)
mvn sonar:sonar -Dsonar.host.url=http://localhost:9000
```

### Frontend

```bash
cd frontend

# ESLint
npm run lint

# Fix auto-fixable issues
npm run lint -- --fix

# Prettier format check
npm run format:check

# Format code
npm run format
```

---

## 📊 Fases de Desarrollo

| Fase                        | Progreso | Estado                 |
| --------------------------- | -------- | ---------------------- |
| Fase 0: Fundación Técnica   | 40%      | 🔧 En Progreso         |
| Fase 1: MVP Vendible        | 0%       | 📋 Por Iniciar         |
| Fase 2: Post-MVP            | 0%       | 📋 Planificado         |
| Fase 3: Escalabilidad       | 0%       | 📋 Futuro              |
| Fase 4: Empresarial         | 0%       | 📋 Futuro              |
| **Global: SaaS MultiRubro** | **8%**   | **🚀 En construcción** |

**Ver detalle completo**: [ROADMAP.md](./docs/ROADMAP.md)

---

## 📚 Documentación Completa

| Documento                                           | Propósito                                |
| --------------------------------------------------- | ---------------------------------------- |
| [README.md](./README.md)                            | Presentación general del proyecto        |
| [INDEX.md](./docs/INDEX.md)                         | Centro de navegación de docs             |
| [ARCHITECTURE.md](./docs/ARCHITECTURE.md)           | Estructura monorepo y diseño del sistema |
| [STACK_Y_PRACTICAS.md](./docs/STACK_Y_PRACTICAS.md) | Stack tecnológico + mejores prácticas    |
| [CONTRIBUTING.md](./docs/CONTRIBUTING.md)           | Cómo contribuir al proyecto              |
| [CHANGELOG.md](./docs/CHANGELOG.md)                 | Historial de cambios                     |
| [ROADMAP.md](./docs/ROADMAP.md)                     | Roadmap general (5 fases)                |
| [ROADMAP_BACKEND.md](./docs/ROADMAP_BACKEND.md)     | Detalles backend                         |
| [ROADMAP_FRONTEND.md](./docs/ROADMAP_FRONTEND.md)   | Detalles frontend                        |
| [ROADMAP_DEVOPS.md](./docs/ROADMAP_DEVOPS.md)       | Detalles DevOps                          |

---

## ❓ FAQs

### ¿Cómo hago un merge a develop/main?

1. Crear PR en GitHub
2. Solicitar code review
3. Aprobar cambios
4. Squash and merge

### ¿Dónde reporto bugs?

GitHub Issues con label `bug` y descripción detallada.

### ¿Cómo propongo nuevas features?

GitHub Issues con label `enhancement` o directamente en una PR.

### ¿Cómo actualizo el CHANGELOG?

Ver [CHANGELOG.md](./docs/CHANGELOG.md) - seguir Keep a Changelog format.

---

## 🆘 Soporte y Contacto

- **Issues**: GitHub Issues
- **Discussiones**: GitHub Discussions
- **Documentación**: Ver [INDEX.md](./docs/INDEX.md)

---

## 📝 Próximos Pasos

1. ✅ Configurar ambiente local (Docker Compose)
2. ✅ Revisar [CONTRIBUTING.md](./docs/CONTRIBUTING.md)
3. ✅ Leer [ARCHITECTURE.md](./docs/ARCHITECTURE.md)
4. ✅ Elegir un task del [ROADMAP.md](./docs/ROADMAP.md)
5. ✅ Crear feature branch y empezar a desarrollar

---

**¡Bienvenido al proyecto! 🎉**

Cualquier duda, revisar la [documentación completa](./docs/INDEX.md).
