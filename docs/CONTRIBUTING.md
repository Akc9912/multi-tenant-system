# 🤝 Guía de Contribución - SaaS MultiRubro

Gracias por tu interés en contribuir. Este documento describe cómo colaborar en el proyecto de manera efectiva y organizada.

---

## 📋 Tabla de Contenidos

1. [Principios](#principios)
2. [Flujo de Trabajo](#flujo-de-trabajo)
3. [Convenciones](#convenciones)
4. [Requisitos para PRs](#requisitos-para-prs)
5. [Comunicación](#comunicación)

---

## Principios

Este proyecto se fundamenta en:

- **Calidad**: Todo código debe ser testeable y mantenible
- **Claridad**: La documentación es tan importante como el código
- **Colaboración**: Comunicación clara entre miembros
- **Modularidad**: Cambios aislados y bien definidos
- **Seguridad**: Prácticas de seguridad desde el inicio

---

## Flujo de Trabajo

### 1. Preparación

```bash
# Clonar repositorio
git clone https://github.com/Akc9912/multi-tenant-system.git
cd multi-tenant-system

# Crear rama desde develop
git checkout develop
git pull origin develop
git checkout -b feature/descripcion-clara
```

### 2. Ramas

Usar nomenclatura según el tipo:

```
feature/nombre-feature          # Nuevas características
bugfix/nombre-bug               # Correcciones de bugs
hotfix/nombre-hotfix            # Fixes críticos en producción
refactor/nombre-refactor        # Cambios de código sin nueva funcionalidad
docs/descripcion-docs           # Actualización de documentación
chore/nombre-chore              # Tareas administrativas
```

### 3. Commits

#### Mensajes Semánticos

```
<tipo>(<módulo>): <descripción breve>

<descripción detallada - opcional>

<referencias - opcional>
```

#### Tipos de Commit

```
feat:       Nueva característica
fix:        Corrección de bug
docs:       Cambios en documentación
style:      Cambios que no afectan lógica (formato, etc.)
refactor:   Cambio de código sin nueva funcionalidad
perf:       Mejoras de performance
test:       Agregar o actualizar tests
chore:      Cambios en build, dependencias, etc.
ci:         Cambios en CI/CD
```

#### Ejemplos

```bash
# Buen commit
git commit -m "feat(auth): agregar validación de JWT"

git commit -m "fix(pos): corregir cálculo de descuentos"

git commit -m "docs(roadmap): actualizar fases de desarrollo"

git commit -m "refactor(appointment): extraer lógica de disponibilidad"
```

### 4. Push y Pull Request

```bash
# Subir cambios
git push origin feature/descripcion-clara

# Crear PR en GitHub
# - Título claro y conciso
# - Descripción detallada de cambios
# - Referenciar issues relacionados: Closes #123
```

#### Checklist de PR

- [ ] Código sigue convenciones del proyecto
- [ ] Tests añadidos/actualizados
- [ ] Documentación actualizada
- [ ] No hay conflictos con `develop`
- [ ] Cambios están limitados al scope descrito
- [ ] Commit messages son semánticos

### 5. Review y Merge

```
PR creado → Review (1-2 aprobaciones) → Merge a develop
                                           ↓
                                    Merge a main (releases)
```

---

## Convenciones

### Estructura de Código

#### Backend (Java/Spring)

```
backend/
└── src/main/java/com/multitenant/
    ├── auth/
    │   ├── controller/
    │   ├── service/
    │   ├── repository/
    │   ├── entity/
    │   ├── dto/
    │   └── mapper/
    ├── company/
    │   └── [similar structure]
    ├── shared/
    │   ├── exception/
    │   ├── util/
    │   ├── config/
    │   ├── constant/
    │   ├── interceptor/
    │   ├── filter/
    │   └── entity/
    └── Application.java
```

**Reglas**:

- Un módulo = un dominio de negocio
- Sin acceso directo entre repositorios
- Services comunican con otros módulos
- DTOs para entrada/salida

#### Frontend (React)

```
frontend/
└── src/
    ├── components/
    │   ├── common/
    │   ├── features/
    │   └── layouts/
    ├── pages/
    ├── services/
    ├── hooks/
    ├── context/
    ├── utils/
    ├── styles/
    └── App.tsx
```

**Reglas**:

- Componentes reutilizables en `common/`
- Componentes por feature
- Hooks propios en `hooks/`
- Services para API
- Context para estado global

### Nomenclatura

#### Clases (Java)

```java
// Entidades
public class User { }

// Services (interfaz + impl)
public interface UserService { }
public class UserServiceImpl implements UserService { }

// Controllers
public class UserController { }

// DTOs
public class UserCreateDto { }
public class UserResponseDto { }

// Enums
public enum UserStatus { ACTIVE, INACTIVE, BLOCKED }
```

#### Variables y Métodos

```java
// Variables y métodos: camelCase
private String userName;
public void getUserById(Long id) { }

// Constantes: UPPER_SNAKE_CASE
public static final String DEFAULT_TIMEZONE = "UTC";
```

#### Base de Datos

```sql
-- Tablas: snake_case
CREATE TABLE user_roles (
    id BIGINT,
    user_id BIGINT,
    role_id BIGINT
);

-- Columnas: snake_case
ALTER TABLE users ADD COLUMN created_at TIMESTAMP;
```

#### React/TypeScript

```typescript
// Componentes: PascalCase
const UserProfile: React.FC = () => {};

// Funciones y variables: camelCase
const getUserData = () => {};
let userName = "John";

// Constantes: UPPER_SNAKE_CASE
const API_BASE_URL = "http://...";

// Interfaces: PascalCase con prefijo I (opcional)
interface IUser {}
type UserProps = {};
```

---

## Requisitos para PRs

### Código

- ✅ Sigue convenciones del proyecto
- ✅ Pasa todos los tests (coverage mínimo 80%)
- ✅ Sin código comentado
- ✅ Sin console.log o debug statements
- ✅ Sin credenciales o secrets
- ✅ Imports/exports organizados

### Tests

**Backend**:

```java
// Unit tests obligatorios para services
@Test
void testUserCreation() { }

// Integration tests para flujos críticos
@SpringBootTest
class UserControllerTest { }
```

**Frontend**:

```typescript
// Tests para componentes reutilizables
describe("UserCard", () => {
  it("should render user data", () => {});
});

// Tests para hooks propios
describe("useUserData", () => {
  it("should fetch user data", () => {});
});
```

### Documentación

- ✅ README actualizado si hay cambios de setup
- ✅ Arquitectura actualizada si cambios arquitectónicos
- ✅ Comentarios para lógica compleja
- ✅ JSDoc/JavaDoc para métodos públicos

### Performance

- ✅ Sin queries N+1
- ✅ Componentes optimizados (React.memo si aplica)
- ✅ Lazy loading donde sea apropiado
- ✅ Índices en BD para queries frecuentes

---

## Comunicación

### Canales

- **GitHub Issues**: Para reportar bugs y proponer features
- **Discussions**: Para preguntas y discusiones generales
- **Pull Requests**: Para feedback en código
- **Reuniones**: Síncronización semanal

### Reportar Bugs

```markdown
**Descripción**
Descripción clara del problema

**Reproducción**

1. Paso 1
2. Paso 2
3. Paso 3

**Comportamiento Esperado**
Qué debería pasar

**Comportamiento Actual**
Qué está pasando

**Contexto**

- Rama/versión
- Stack
- Logs si aplica
```

### Proponer Features

```markdown
**Descripción**
Qué quieres agregar y por qué

**Solución Propuesta**
Cómo lo ves implementado

**Alternativas**
Otras formas de hacerlo

**Contexto Adicional**
Información extra
```

---

## Revisar PRs

### Como Revisor

✅ **Hacer**:

- Revisar código con atención
- Comentarios constructivos
- Preguntar si no entiendes algo
- Sugerir mejoras
- Aprobar cuando cumpla requisitos

❌ **No hacer**:

- Comentarios destructivos o ataques personales
- Bloquear PRs por preferencias personales
- Requests excesivos de cambios
- Reviews sin leer el código

### Responder Reviews

✅ **Hacer**:

- Responder preguntas
- Justificar decisiones
- Aplicar sugerencias útiles
- Hacer push de cambios

❌ **No hacer**:

- Ignorar feedback
- Ser defensivo
- Hacer cambios sin avisar

---

## Checklist Final

Antes de crear PR:

- [ ] Código escrito y testeado localmente
- [ ] Tests pasan: `npm test` / `mvn test`
- [ ] Linter pasa: `npm run lint` / `mvn verify`
- [ ] Documentación actualizada
- [ ] Commits con mensajes semánticos
- [ ] Rama actualizada con develop
- [ ] PR description clara y detallada
- [ ] Checklist de PR completado

---

## Preguntas?

- Revisar [docs/](./INDEX.md)
- Buscar issues similares
- Crear nueva discusión
- Preguntar en reunión semanal

**¡Gracias por contribuir! 🎉**
