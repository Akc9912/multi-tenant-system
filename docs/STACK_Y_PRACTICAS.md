# 🛠️ Stack Tecnológico y Prácticas - SaaS MultiRubro

Stack tecnológico, arquitectura, patrones de diseño y mejores prácticas del proyecto.

---

## 📦 Stack Tecnológico

### Backend

```
Java Ecosystem
├── Java 17+ LTS
├── Spring Boot 3.0+
│   ├── Spring Data JPA
│   ├── Spring Security
│   ├── Spring Validation
│   ├── Spring Cache
│   ├── Spring Cloud (future)
│   └── Spring Boot Admin
├── Hibernate ORM
├── MySQL 8.0+
├── JUnit 5 + Mockito
├── Apache Commons
├── Lombok
├── MapStruct
├── Jackson
├── Validation
│   ├── Hibernate Validator
│   └── Bean Validation API
├── Logging
│   ├── SLF4J
│   └── Logback
├── Web
│   ├── Apache HttpClient
│   └── Okhttp
└── Build
    └── Maven 3.8+
```

### Frontend

```
React Ecosystem
├── React 18+
├── TypeScript 5.0+
├── Vite (build tool)
├── React Router v6+
├── State Management
│   ├── Redux Toolkit
│   └── Redux Thunk
├── UI Components
│   ├── Material-UI (MUI)
│   ├── React Hook Form
│   └── Zod (validation)
├── HTTP Client
│   ├── Axios
│   └── TanStack Query
├── Styling
│   ├── Emotion (CSS-in-JS)
│   ├── Tailwind CSS (optional)
│   └── SCSS Modules
├── Testing
│   ├── Jest
│   ├── React Testing Library
│   ├── Vitest
│   ├── Cypress (E2E)
│   └── Playwright (E2E)
├── Development
│   ├── ESLint
│   ├── Prettier
│   ├── Husky
│   └── lint-staged
└── Performance
    ├── React Memo
    ├── useMemo/useCallback
    └── Code splitting
```

### DevOps & Infrastructure

```
Containerización & Orquestación
├── Docker 20.10+
├── Docker Compose 2.0+
├── Kubernetes (Phase 2+)
│   ├── EKS/GKE/AKS
│   ├── Helm
│   ├── Ingress Controller
│   └── Service Mesh (optional)
├── Container Registry
│   └── GitHub Container Registry
├── CI/CD
│   └── GitHub Actions
├── Cloud Providers (seleccionar uno)
│   ├── AWS
│   ├── Google Cloud
│   └── Azure
└── Monitoring
    ├── CloudWatch/Stackdriver/Monitor
    ├── Prometheus (Phase 2+)
    ├── Grafana (Phase 2+)
    └── ELK Stack (Phase 2+)
```

### Database

```
MySQL Ecosystem
├── MySQL 8.0+
├── Flyway (migrations)
├── Índices optimizados
├── Replication (Phase 1+)
├── Sharding (Phase 3+)
├── Backup automated
└── Monitoring
```

---

## 🏗️ Patrones de Arquitectura

### Arquitectura General

**Monorepo Modular** con estructura preparada para evolucionar a microservicios:

```
multi-tenant-system/
├── backend/                    # Spring Boot application
│   ├── src/main/java/
│   │   └── com/multirubro/
│   │       ├── auth/          # Authentication module
│   │       ├── company/        # Company management
│   │       ├── branch/         # Branch/location management
│   │       ├── user/           # User management
│   │       ├── product/        # Product catalog
│   │       ├── sale/           # Sales/POS system
│   │       ├── appointment/    # Appointment/turnos
│   │       ├── stock/          # Stock management
│   │       ├── shared/         # Shared utilities
│   │       └── config/         # Configuration classes
│   ├── src/test/java/         # Unit & integration tests
│   ├── pom.xml                # Maven configuration
│   └── Dockerfile
├── frontend/                   # React application
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── store/
│   │   ├── hooks/
│   │   ├── utils/
│   │   ├── types/
│   │   └── styles/
│   ├── public/
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── Dockerfile
├── docs/                       # Documentation
│   ├── README.md
│   ├── ARCHITECTURE.md
│   ├── ROADMAP.md
│   ├── ROADMAP_BACKEND.md
│   ├── ROADMAP_FRONTEND.md
│   ├── ROADMAP_DEVOPS.md
│   ├── CONTRIBUTING.md
│   ├── CHANGELOG.md
│   └── STACK_Y_PRACTICAS.md
├── docker-compose.yml
└── .github/workflows/          # CI/CD pipelines
```

### Backend Patterns

#### Layered Architecture

```
Controller Layer
    ↓
Service Layer (Business Logic)
    ↓
Repository Layer (Data Access)
    ↓
Entity/Database Layer
```

**Ejemplo: Flow de una venta (Sale)**

```
SaleController
├── POST /api/v1/sales
│   └── validates input
│       ↓
SaleService
├── createSale()
│   ├── validates business rules
│   ├── calculates totals
│   ├── applies discounts
│   ├── manages multi-tenant isolation
│   ├── publishes event (Phase 1+)
│   └── returns response
└── Repositories
    ├── SaleRepository.save(sale)
    ├── SaleItemRepository.saveAll(items)
    ├── StockRepository.update()
    └── PaymentRepository.save(payment)
```

#### Multi-Tenancy Pattern

**Tenant Isolation**: Data-level isolation usando tenant context

```java
// Request → TenantFilter → extracts tenant_id
// TenantContext.setCurrentTenant(tenantId)
//
// Service Layer → Repository → aplica WHERE tenant_id = ?
//
// TenantContext.clear() → Response

// All queries automatically filtered by tenant
```

#### Module Independence

Cada módulo es independiente y puede extraerse a microservice:

```
auth/ → Authentication & Authorization
company/ → Company/Organization management
branch/ → Multi-branch support
user/ → User management & profiles
product/ → Product catalog & categories
sale/ → POS & sales transactions
appointment/ → Appointment/scheduling system
stock/ → Inventory management
shared/ → Utilities, base classes, constants
```

### Frontend Patterns

#### Feature-based Structure

```
features/
├── auth/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── store/ (Redux slices)
│   ├── hooks/
│   └── types/
├── pos/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── hooks/
│   └── types/
└── [other features]
```

#### State Management (Redux)

```
Redux Store
├── authSlice (user, token, roles)
├── posSlice (cart, products, checkout)
├── appointmentsSlice (appointments, schedule)
├── uiSlice (modals, notifications, loading)
└── [feature slices]

Actions → Dispatch → Reducer → State Update → Component Re-render
```

#### Custom Hooks Pattern

```typescript
// Custom hooks encapsulate business logic
useAuth() → manages authentication state
useCart() → manages POS cart state
useAppointments() → manages appointments data
useApi() → generic API calls with error handling
useFetch() → data fetching with caching
```

---

## ✅ Mejores Prácticas

### Code Quality

#### Backend (Java/Spring)

**Naming Conventions**:

```
Classes: PascalCase
Methods/Variables: camelCase
Constants: UPPER_SNAKE_CASE
Packages: lowercase, reverse domain notation
Files: Singular nouns (User not Users)
DTOs: UserDTO, CreateUserRequest, UserResponse
Entities: User (without DTO suffix)
```

**Code Organization**:

- [ ] Services contain business logic
- [ ] Controllers handle HTTP only
- [ ] Repositories handle data access only
- [ ] Entities are POJOs without logic
- [ ] Utils contain reusable functions
- [ ] Exceptions are custom and specific
- [ ] Constants in dedicated classes
- [ ] Enums for status values

**Documentation**:

```java
/**
 * Creates a new sale transaction with items and payment.
 * Applies multi-tenant isolation automatically.
 *
 * @param request CreateSaleRequest with items and payment details
 * @return SaleResponse with generated id and receipt info
 * @throws ValidationException if sale items are invalid
 * @throws InsufficientStockException if not enough stock
 * @throws PaymentProcessingException if payment fails
 */
@PostMapping("/sales")
public ResponseEntity<SaleResponse> createSale(@RequestBody CreateSaleRequest request) {
    // ...
}
```

#### Frontend (React/TypeScript)

**Naming Conventions**:

```
Components: PascalCase (Button.tsx, UserProfile.tsx)
Folders: kebab-case or camelCase
Files: Match component name
Hooks: camelCase starting with 'use' (useCart, useAuth)
Types/Interfaces: PascalCase (IUser, UserProps)
Constants: UPPER_SNAKE_CASE
Props: camelCase (backgroundColor, onClick)
State: camelCase (isLoading, cartItems)
```

**Component Structure**:

```typescript
// Imports
import React, { useState, useEffect } from "react";
import { Button } from "@mui/material";
import useAuth from "../hooks/useAuth";
import { IUserProps } from "./types";

// Types/Interfaces
interface IUserProps {
  id: string;
  name: string;
  email: string;
}

// Component
const UserProfile: React.FC<IUserProps> = ({ id, name, email }) => {
  const [isLoading, setIsLoading] = useState(false);
  const { user, logout } = useAuth();

  useEffect(() => {
    // Logic
  }, [id]);

  const handleAction = () => {
    // Handler
  };

  return <div>{/* JSX */}</div>;
};

// Export
export default UserProfile;
```

**Principles**:

- [ ] Single Responsibility Principle (SRP)
- [ ] One component per file
- [ ] Props over global state (when possible)
- [ ] Custom hooks for reusable logic
- [ ] Memoization for performance (React.memo, useMemo)
- [ ] Error boundaries for error handling
- [ ] Accessibility (a11y) compliance

### Testing

#### Backend Testing Strategy

```
Unit Tests (70%)
├── Service logic tests
├── Utility function tests
├── Validator tests
└── Mock repositories

Integration Tests (20%)
├── Controller → Service tests
├── Service → Repository tests
├── Database tests
└── API endpoint tests (with TestRestTemplate)

E2E Tests (10%)
├── Full request → response cycles
├── Database transactions
├── Security tests
└── Performance tests
```

**Testing Tools**:

```
├── JUnit 5
├── Mockito (mocking)
├── AssertJ (fluent assertions)
├── Spring Test
├── Testcontainers (Docker databases)
└── Maven Surefire (test execution)
```

**Test Coverage Target**: 80%+ overall, 90%+ for critical modules

**Example Backend Test**:

```java
@ExtendWith(SpringExtension.class)
@DataJpaTest
class SaleRepositoryTest {

  @Autowired
  private SaleRepository saleRepository;

  @Test
  void whenFindByTenantId_thenReturnFilteredSales() {
    // Arrange
    String tenantId = "tenant-123";
    Sale sale = new Sale();
    sale.setTenantId(tenantId);
    saleRepository.save(sale);

    // Act
    List<Sale> result = saleRepository.findByTenantId(tenantId);

    // Assert
    assertThat(result).hasSize(1)
      .allMatch(s -> s.getTenantId().equals(tenantId));
  }
}
```

#### Frontend Testing Strategy

```
Unit Tests (50%)
├── Component render tests
├── Hook tests
├── Utility function tests
└── Store/reducer tests

Integration Tests (30%)
├── Component → Hook tests
├── Multiple components working together
├── API integration
└── Form submission flows

E2E Tests (20%)
├── User workflows (login → purchase → receipt)
├── Complex multi-step processes
├── Browser compatibility
└── Performance tests
```

**Testing Tools**:

```
├── Jest
├── React Testing Library
├── Vitest (faster unit tests)
├── Cypress (E2E)
├── Playwright (E2E)
└── MSW (Mock Service Worker)
```

**Example Frontend Test**:

```typescript
import { render, screen, fireEvent, waitFor } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import POS from "../POS";

describe("POS Component", () => {
  it("should add product to cart when clicked", async () => {
    // Arrange
    render(<POS />);
    const addButton = screen.getByRole("button", { name: /add/i });

    // Act
    await userEvent.click(addButton);

    // Assert
    await waitFor(() => {
      expect(screen.getByText(/cart items: 1/i)).toBeInTheDocument();
    });
  });
});
```

### Security Practices

#### Authentication & Authorization

**Backend (Spring Security + JWT)**:

```
POST /api/v1/auth/login
├── Validate credentials
├── Generate JWT token (with tenant_id, user_id, roles)
├── Return token + refresh_token
└── Client stores in secure httpOnly cookie

Every Protected Request
├── TenantFilter extracts tenant_id
├── JwtFilter validates token
├── SecurityContext sets authentication
└── Service validates tenant isolation
```

**Frontend (React)**:

```typescript
// Login flow
const login = async (email, password) => {
  const response = await api.post("/auth/login", { email, password });
  localStorage.setItem("authToken", response.token);
  setUser(response.user);
  navigate("/dashboard");
};

// Protected route
const ProtectedRoute = ({ children }) => {
  const { isAuthenticated } = useAuth();
  return isAuthenticated ? children : <Navigate to="/login" />;
};
```

**Tenant Isolation**:

- [ ] All queries filter by tenant_id
- [ ] No cross-tenant data access
- [ ] Tenant_id in JWT token
- [ ] Validate tenant on each request
- [ ] Audit logging for access

#### Data Protection

- [ ] Passwords hashed with bcrypt (Spring Security)
- [ ] Encryption at rest (database)
- [ ] Encryption in transit (HTTPS/TLS 1.3)
- [ ] Sensitive data masked in logs
- [ ] API keys in environment variables
- [ ] CORS whitelist configured

#### API Security

```
Headers & Validation:
├── HSTS (HTTP Strict Transport Security)
├── CSP (Content Security Policy)
├── X-Content-Type-Options: nosniff
├── X-Frame-Options: DENY
├── X-XSS-Protection
├── Rate limiting
├── Input validation (Bean Validation)
├── SQL injection prevention (JPA parameterized queries)
└── CORS (specific origins only)
```

### Performance Optimization

#### Backend

- [ ] Query optimization (use projections, avoid N+1)
- [ ] Caching (Spring Cache, Redis in Phase 2)
- [ ] Database indexing
- [ ] Connection pooling (HikariCP)
- [ ] Lazy loading for relationships
- [ ] Async processing for non-critical tasks (Phase 1+)
- [ ] Pagination for large result sets
- [ ] Compression (gzip)

**Example Query Optimization**:

```java
// ❌ N+1 problem (1 + N queries)
List<Company> companies = repository.findAll();
for (Company company : companies) {
  System.out.println(company.getBranches().size()); // N additional queries
}

// ✅ Solution: eager loading
@Query("SELECT c FROM Company c JOIN FETCH c.branches")
List<Company> findAllWithBranches();
```

#### Frontend

- [ ] Code splitting by route
- [ ] Lazy loading components
- [ ] Image optimization
- [ ] CSS/JS minification
- [ ] Memoization (React.memo, useMemo)
- [ ] Virtual scrolling for large lists
- [ ] Request caching/deduplication
- [ ] Service Workers (PWA in Phase 2)

**Example Frontend Performance**:

```typescript
// Lazy load route
const POS = lazy(() => import("../pages/POS"));

// Memoize expensive computation
const CartSummary = memo(({ items }) => {
  const total = useMemo(
    () => items.reduce((sum, item) => sum + item.price * item.qty, 0),
    [items]
  );
  return <div>Total: {total}</div>;
});

// Debounce search
const handleSearch = useMemo(
  () => debounce((query) => searchProducts(query), 500),
  []
);
```

### Deployment Practices

#### Environment Management

```
Development
├── Local Docker Compose
├── Environment: .env.development
├── Database: MySQL local
└── Hot reload enabled

Staging
├── Cloud infrastructure (AWS/GCP)
├── Environment: .env.staging
├── Database: RDS/managed
├── Feature flags for testing

Production
├── High availability setup
├── Environment: .env.production
├── Secrets in Secrets Manager
├── Multi-region (Phase 3+)
├── CDN for static assets
└── Monitoring & alerting
```

#### Version Control Strategy

```
Branches
├── main (production-ready)
├── develop (integration branch)
└── feature/* (feature development)
    ├── feature/auth-2fa
    ├── feature/pos-discounts
    ├── bugfix/stock-calculation
    ├── refactor/user-service
    ├── docs/api-documentation
    └── chore/dependency-update

Commits: Conventional Commits
├── feat: new feature
├── fix: bug fix
├── docs: documentation
├── style: formatting
├── refactor: refactoring
├── perf: performance
├── test: tests
├── chore: maintenance
└── ci: CI/CD changes

Example: feat(sale): add discount calculation to POS
```

#### Release Process

```
1. Create release branch from develop
2. Update version (MAJOR.MINOR.PATCH)
3. Update CHANGELOG.md
4. Create pull request to main
5. Code review & approval
6. Merge to main
7. Create Git tag (v1.2.3)
8. GitHub Actions deploys to production
9. Merge main back to develop
```

---

## 📋 Checklist de Calidad

### Antes de cada commit

- [ ] Code compiles without errors
- [ ] Tests pass (100% of affected tests)
- [ ] No console errors/warnings
- [ ] Code follows style guide
- [ ] No commented code
- [ ] No hardcoded values
- [ ] Proper error handling
- [ ] Documentation updated

### Antes de cada PR

- [ ] All tests pass
- [ ] Test coverage > 80%
- [ ] Code review requested
- [ ] CHANGELOG updated
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
- [ ] Performance impact assessed

### Antes de cada release

- [ ] All tests pass
- [ ] Code coverage metrics reviewed
- [ ] Security scan passed
- [ ] Performance benchmarks run
- [ ] Documentation complete
- [ ] Changelog finalized
- [ ] Version updated
- [ ] Tag created

---

## 🔍 Tools & IDE Setup

### Backend Development

```
IDE: IntelliJ IDEA Community / Eclipse
Extensions:
├── Lombok
├── Spring Boot Dashboard
├── Database tools
└── Git integration

Plugins:
├── SonarQube Scanner
├── Checkstyle
├── SpotBugs
└── Architecture visualization
```

### Frontend Development

```
IDE: VS Code / WebStorm
Extensions:
├── ESLint
├── Prettier
├── Tailwind CSS IntelliSense
├── GraphQL (if using)
└── REST Client

Plugins:
├── React Developer Tools
├── Redux DevTools
├── React Testing Library
└── Code spell checker
```

### Local Development

```bash
# Install dependencies
cd backend && mvn clean install
cd ../frontend && npm install

# Start services
docker-compose up -d

# Run applications
cd backend && mvn spring-boot:run
cd ../frontend && npm run dev

# Run tests
cd backend && mvn test
cd ../frontend && npm test

# Code quality
cd backend && mvn sonar:sonar
cd ../frontend && npm run lint
```
