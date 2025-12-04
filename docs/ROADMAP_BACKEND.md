# 🔧 Roadmap Backend - SaaS MultiRubro

Detalles específicos del desarrollo backend por fase.

---

## Fase 0: Fundación Técnica

| Progreso | Estado         |
| -------- | -------------- |
| 40%      | 🔧 En Progreso |

### Setup Base

- [ ] Proyecto Spring Boot 3.0+ inicializado
- [ ] MySQL 8.0+ configurada
- [ ] Estructura de módulos creada
- [ ] BaseEntity y BaseRepository
- [ ] GlobalExceptionHandler
- [ ] Logging configurado

**Módulos a crear**:

- `shared` - Clases base y utilidades

### Seguridad

- [ ] JWT token generation/validation
- [ ] Authentication Filter
- [ ] Authorization (roles/permisos)
- [ ] CORS configurado
- [ ] Input validation (Bean Validation)

### Testing Base

- [ ] Estructura de tests lista
- [ ] JUnit 5 + Mockito
- [ ] Test containers para BD

### CI/CD

- [ ] GitHub Actions workflow básico
- [ ] Build job
- [ ] Test job
- [ ] Linter job

---

## Fase 1: MVP Vendible

| Progreso | Estado         |
| -------- | -------------- |
| 0%       | 📋 Por Iniciar |

### Módulo Auth

```
├── Entity: User, Role, Permission, AuditLog
├── Repository: UserRepository, RoleRepository
├── Service: AuthService, JwtTokenProvider
├── Controller: AuthController (/login, /logout, /register)
└── Tests: Unit + Integration
```

**Endpoints**:

- POST /api/v1/auth/login
- POST /api/v1/auth/logout
- POST /api/v1/auth/register
- POST /api/v1/auth/refresh-token

### Módulo Company

```
├── Entity: Company, Configuration
├── Repository: CompanyRepository
├── Service: CompanyService
├── Controller: CompanyController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET/POST /api/v1/companies
- GET/PUT /api/v1/companies/{id}

### Módulo Branch

```
├── Entity: Branch, BranchConfig
├── Repository: BranchRepository
├── Service: BranchService
├── Controller: BranchController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET/POST /api/v1/branches
- GET/PUT /api/v1/branches/{id}

### Módulo User

```
├── Entity: User, UserProfile, UserRole
├── Repository: UserRepository, UserRoleRepository
├── Service: UserService
├── Controller: UserController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET/POST /api/v1/users
- GET/PUT/DELETE /api/v1/users/{id}
- POST /api/v1/users/{id}/roles

### Módulo Product

```
├── Entity: Product, Category
├── Repository: ProductRepository, CategoryRepository
├── Service: ProductService, CategoryService
├── Controller: ProductController, CategoryController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET/POST /api/v1/products
- GET/PUT/DELETE /api/v1/products/{id}
- GET/POST /api/v1/categories
- GET/PUT/DELETE /api/v1/categories/{id}

### Módulo Sale (POS)

```
├── Entity: Sale, SaleItem, Payment
├── Repository: SaleRepository, SaleItemRepository
├── Service: SaleService, PaymentService
├── Controller: SaleController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET /api/v1/sales
- POST /api/v1/sales (crear venta)
- GET /api/v1/sales/{id}
- GET /api/v1/sales/report/daily

**Funcionalidades**:

- Crear venta con items
- Aplicar descuentos/impuestos
- Procesar múltiples formas de pago
- Generar recibo

### Módulo Appointment

```
├── Entity: Appointment, Service, Professional, Schedule
├── Repository: AppointmentRepository, ServiceRepository, etc.
├── Service: AppointmentService, ScheduleService
├── Controller: AppointmentController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET /api/v1/appointments
- POST /api/v1/appointments (agendar)
- GET/PUT/DELETE /api/v1/appointments/{id}
- GET /api/v1/professionals/{id}/availability
- POST /api/v1/services
- GET /api/v1/services

**Funcionalidades**:

- Agendar turnos
- Verificar disponibilidad
- Confirmar/cancelar turnos
- Listar servicios

### Módulo Stock

```
├── Entity: Stock, StockMovement
├── Repository: StockRepository, StockMovementRepository
├── Service: StockService
├── Controller: StockController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET /api/v1/stock
- POST /api/v1/stock/movements
- GET /api/v1/stock/{productId}

**Funcionalidades**:

- Consultar stock
- Registrar movimientos
- Alertas de bajo stock

### Módulo Cash Register

```
├── Entity: CashRegister, CashTransaction
├── Repository: CashRegisterRepository, CashTransactionRepository
├── Service: CashRegisterService
├── Controller: CashRegisterController
└── Tests: Unit + Integration
```

**Endpoints**:

- POST /api/v1/cash-register/open
- POST /api/v1/cash-register/close
- GET /api/v1/cash-register/balance

### Reportes Básicos

```
├── Entity: (usan datos de otras entidades)
├── Service: ReportService
├── Controller: ReportController
└── Tests: Unit + Integration
```

**Endpoints**:

- GET /api/v1/reports/sales/daily
- GET /api/v1/reports/appointments/monthly
- GET /api/v1/reports/products/top-sellers

### Database

- [ ] Schema para todas las entidades
- [ ] Migrations con Flyway
- [ ] Índices para performance
- [ ] Constraints y validaciones

### Testing

- [ ] 80%+ cobertura de código
- [ ] Unit tests para services
- [ ] Integration tests para endpoints
- [ ] Test data factories

---

## Fase 2: Post-MVP

| Progreso | Estado         |
| -------- | -------------- |
| 0%       | 📋 Planificado |

### Mejoras a Módulos

#### Sale (POS)

- [ ] Promociones y combos
- [ ] Descuentos por categoría
- [ ] Fidelización (puntos)
- [ ] Historial detallado

#### Appointment

- [ ] Recordatorios automáticos
- [ ] Gestión de no-shows
- [ ] Historial completo
- [ ] Evaluación de servicios

#### Stock

- [ ] Órdenes de compra
- [ ] Recepción de mercadería
- [ ] Transferencias entre sedes
- [ ] Auditoría de movimientos

### Nuevos Módulos

#### Maintenance

- Entity: MaintenanceTask
- Service: MaintenanceService
- Endpoints para gestionar tareas

#### Cleaning

- Entity: CleaningTask
- Service: CleaningService
- Endpoints para checklists

#### Suppliers

- Entity: Supplier, Purchase
- Service: SupplierService
- Endpoints para órdenes de compra

### Performance

- [ ] Query optimization
- [ ] Caching (Redis)
- [ ] Índices adicionales
- [ ] Batch processing

---

## Fase 3: Escalabilidad

| Progreso | Estado    |
| -------- | --------- |
| 0%       | 📋 Futuro |

### Microservicios

#### Auth Service

- [ ] Service independiente
- [ ] OAuth2/OpenID Connect
- [ ] SSO

#### Payments Service

- [ ] Procesar pagos
- [ ] Múltiples gateways
- [ ] Webhooks

#### Notifications Service

- [ ] Email
- [ ] SMS
- [ ] Push notifications

### Event Streaming

- [ ] Kafka/RabbitMQ setup
- [ ] Event publishing
- [ ] Event consuming
- [ ] Dead letter queues

---

## Fase 4: Empresarial

| Progreso | Estado    |
| -------- | --------- |
| 0%       | 📋 Futuro |

### Business Intelligence

- [ ] Data warehouse
- [ ] ETL pipelines
- [ ] Análisis avanzado
- [ ] Predicciones (ML)

### Billing

- [ ] Invoice generation
- [ ] Automatic billing cycles
- [ ] Payment tracking
- [ ] Compliance

### Integrations

- [ ] Accounting systems
- [ ] Banking APIs
- [ ] Marketplace APIs

---

## 📊 Estadísticas

| Fase | Módulos | Endpoints | Tests Esperados | Status |
| ---- | ------- | --------- | --------------- | ------ |
| 0    | 1       | 0         | 10+             | 🔧 40% |
| 1    | 9       | 50+       | 100+            | ⏳ 0%  |
| 2    | +3      | +20       | +50             | 📋 0%  |
| 3    | +3      | +30       | +50             | 📋 0%  |
| 4    | -       | +40       | +50             | 📋 0%  |
