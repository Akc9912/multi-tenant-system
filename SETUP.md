# 🛠️ Setup Inicial del Proyecto - SaaS MultiRubro

Guía paso a paso para inicializar el proyecto sin romper la estructura documentada.

---

## 📋 Prerequisitos

- Git
- Docker & Docker Compose
- Java 17+ (para backend)
- Node.js 18+ LTS (para frontend)
- Maven 3.8+ (para backend)

---

## 🚀 Inicialización del Proyecto

### Paso 1: Crear Estructura de Carpetas

```bash
# Desde la raíz del proyecto (multi-tenant-system)
mkdir -p backend
mkdir -p frontend
mkdir -p docs

# Verificar estructura
tree -L 1
# Resultado esperado:
# .
# ├── backend/
# ├── frontend/
# ├── docs/
# └── [archivos .md en raíz]
```

---

## 🔧 Backend - Spring Boot

### Paso 1: Inicializar Proyecto Maven

```bash
cd backend

# Opción A: Usando Spring Boot CLI
spring boot new --name=app --type=maven --package-name=com.multirubro --language=java

# Opción B: Usar Maven Archetype
mvn archetype:generate \
  -DgroupId=com.multirubro \
  -DartifactId=app \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false

# Opción C: Descargar starter desde Spring Initializr y extraer
# Visitar: https://start.spring.io/
# Configurar:
# - Project: Maven Project
# - Language: Java
# - Spring Boot: 3.0+
# - Group: com.multirubro
# - Artifact: app
# - Packaging: Jar
# - Java: 17+
# - Dependencies:
#   * Spring Web
#   * Spring Data JPA
#   * MySQL Driver
#   * Spring Security
```

### Paso 2: Estructura Backend

```bash
cd backend/src/main/java/com/multirubro

# Crear módulos base
mkdir -p auth
mkdir -p company
mkdir -p branch
mkdir -p user
mkdir -p product
mkdir -p sale
mkdir -p appointment
mkdir -p stock
mkdir -p shared

# En cada módulo crear:
# - entity/
# - repository/
# - service/
# - controller/
# - dto/

# Ejemplo para auth:
mkdir -p auth/{entity,repository,service,controller,dto}
mkdir -p company/{entity,repository,service,controller,dto}
mkdir -p branch/{entity,repository,service,controller,dto}
mkdir -p user/{entity,repository,service,controller,dto}
mkdir -p product/{entity,repository,service,controller,dto}
mkdir -p sale/{entity,repository,service,controller,dto}
mkdir -p appointment/{entity,repository,service,controller,dto}
mkdir -p stock/{entity,repository,service,controller,dto}
mkdir -p shared/{entity,repository,config,exception,util}
```

### Paso 3: Configurar pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.multirubro</groupId>
    <artifactId>saas-multirubro-backend</artifactId>
    <version>0.1.0</version>
    <packaging>jar</packaging>

    <name>SaaS MultiRubro Backend</name>
    <description>Backend del sistema SaaS MultiRubro</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.0.0</version>
        <relativePath/>
    </parent>

    <properties>
        <java.version>17</java.version>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Spring Boot Web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Spring Data JPA -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <!-- Spring Security -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <!-- MySQL Driver -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
            <scope>runtime</scope>
        </dependency>

        <!-- Validation -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>

        <!-- Lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- JUnit 5 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- Mockito -->
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- JaCoCo para cobertura -->
        <dependency>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.8</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.8</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

### Paso 4: Crear application.yml

```yaml
# backend/src/main/resources/application.yml
spring:
  application:
    name: saas-multirubro-backend

  datasource:
    url: jdbc:mysql://localhost:3306/multirubro_db?serverTimezone=UTC
    username: root
    password: root
    driver-class-name: com.mysql.cj.jdbc.Driver

  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect
        format_sql: true

  mvc:
    cors:
      allowed-origins: http://localhost:3000
      allowed-methods: GET,POST,PUT,DELETE,OPTIONS
      allowed-headers: "*"
      max-age: 3600

server:
  port: 8080
  servlet:
    context-path: /api/v1

logging:
  level:
    root: INFO
    com.multirubro: DEBUG
  pattern:
    console: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"
```

### Paso 5: Crear Main Application

```java
// backend/src/main/java/com/multirubro/SaasMultirubroApplication.java
package com.multirubro;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SaasMultirubroApplication {

    public static void main(String[] args) {
        SpringApplication.run(SaasMultirubroApplication.class, args);
    }
}
```

---

## ⚛️ Frontend - React + TypeScript

### Paso 1: Crear Proyecto React

```bash
cd frontend

# Opción A: Vite (recomendado)
npm create vite@latest . -- --template react-ts

# Opción B: Create React App (legacy)
npx create-react-app . --template typescript
```

### Paso 2: Estructura Frontend

```bash
cd frontend/src

# Crear estructura
mkdir -p components/{common,ui,features}
mkdir -p pages
mkdir -p hooks
mkdir -p services
mkdir -p store
mkdir -p utils/{api,formatters,validators,constants,helpers}
mkdir -p types
mkdir -p styles

# Estructura esperada:
# src/
# ├── components/
# │   ├── common/       (Header, Sidebar, Layout)
# │   ├── ui/           (Button, Input, Modal, etc)
# │   └── features/     (Feature-specific)
# ├── pages/            (Dashboard, POS, etc)
# ├── hooks/            (Custom React hooks)
# ├── services/         (API calls)
# ├── store/            (Redux)
# ├── utils/
# │   ├── api/
# │   ├── formatters/
# │   ├── validators/
# │   ├── constants/
# │   └── helpers/
# ├── types/            (TypeScript types)
# ├── styles/           (Global styles)
# └── App.tsx
```

### Paso 3: Instalar Dependencias

```bash
cd frontend

# Core dependencies
npm install react react-dom
npm install typescript @types/react @types/react-dom

# Routing
npm install react-router-dom @types/react-router-dom

# State Management
npm install @reduxjs/toolkit react-redux
npm install redux

# HTTP Client
npm install axios

# UI Library
npm install @mui/material @emotion/react @emotion/styled
npm install @mui/icons-material

# Forms & Validation
npm install react-hook-form zod

# Utilities
npm install lodash @types/lodash

# Dev Dependencies
npm install -D vite @vitejs/plugin-react
npm install -D eslint eslint-config-react-app
npm install -D prettier
npm install -D @types/node

# Testing
npm install -D vitest @testing-library/react @testing-library/jest-dom
npm install -D cypress
```

### Paso 4: Configurar TypeScript

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "resolveJsonModule": true,
    "baseUrl": "src",
    "paths": {
      "@/*": ["*"]
    }
  }
}
```

### Paso 5: Configurar Vite

```js
// frontend/vite.config.ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
  server: {
    port: 3000,
    proxy: {
      "/api": {
        target: "http://localhost:8080",
        changeOrigin: true,
      },
    },
  },
});
```

### Paso 6: package.json

```json
{
  "name": "saas-multirubro-frontend",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint src --ext ts,tsx",
    "lint:fix": "eslint src --ext ts,tsx --fix",
    "format": "prettier --write 'src/**/*.{ts,tsx,jsx,css,md}'",
    "format:check": "prettier --check 'src/**/*.{ts,tsx,jsx,css,md}'",
    "test": "vitest",
    "test:ui": "vitest --ui",
    "test:coverage": "vitest --coverage",
    "e2e": "cypress open"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.15.0",
    "@reduxjs/toolkit": "^1.9.6",
    "react-redux": "^8.1.3",
    "axios": "^1.5.0",
    "@mui/material": "^5.14.0",
    "@emotion/react": "^11.11.0",
    "@emotion/styled": "^11.11.0",
    "@mui/icons-material": "^5.14.0",
    "react-hook-form": "^7.47.0",
    "zod": "^3.22.0",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "typescript": "^5.2.0",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "@types/node": "^20.5.0",
    "@types/lodash": "^4.14.196",
    "vite": "^4.4.0",
    "@vitejs/plugin-react": "^4.0.0",
    "eslint": "^8.48.0",
    "eslint-config-react-app": "^7.0.1",
    "prettier": "^3.0.3",
    "vitest": "^0.34.0",
    "@testing-library/react": "^14.0.0",
    "@testing-library/jest-dom": "^6.1.0",
    "cypress": "^13.3.0"
  }
}
```

---

## 🐳 Docker Compose

### Crear docker-compose.yml

```yaml
# docker-compose.yml (en raíz del proyecto)
version: "3.8"

services:
  # MySQL Database
  mysql:
    image: mysql:8.0
    container_name: multirubro-db
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: multirubro_db
      MYSQL_USER: multirubro_user
      MYSQL_PASSWORD: multirubro_pass
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - multirubro-network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      timeout: 20s
      retries: 10

  # Redis (optional, para Phase 2+)
  redis:
    image: redis:7-alpine
    container_name: multirubro-redis
    ports:
      - "6379:6379"
    networks:
      - multirubro-network
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      timeout: 10s
      retries: 5

  # Backend (spring boot)
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    container_name: multirubro-backend
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/multirubro_db?serverTimezone=UTC
      SPRING_DATASOURCE_USERNAME: multirubro_user
      SPRING_DATASOURCE_PASSWORD: multirubro_pass
      SPRING_JPA_HIBERNATE_DDL_AUTO: validate
    ports:
      - "8080:8080"
    depends_on:
      mysql:
        condition: service_healthy
    networks:
      - multirubro-network
    volumes:
      - ./backend:/app
    command: mvn spring-boot:run

  # Frontend (React)
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile.dev
    container_name: multirubro-frontend
    ports:
      - "3000:3000"
    environment:
      REACT_APP_API_URL: http://localhost:8080/api/v1
    depends_on:
      - backend
    networks:
      - multirubro-network
    volumes:
      - ./frontend/src:/app/src
    command: npm run dev

networks:
  multirubro-network:
    driver: bridge

volumes:
  mysql_data:
```

### Dockerfiles

**backend/Dockerfile**

```dockerfile
FROM maven:3.8-openjdk-17-slim as builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests

FROM openjdk:17-slim
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**frontend/Dockerfile.dev**

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "run", "dev"]
```

**frontend/Dockerfile** (producción)

```dockerfile
FROM node:18-alpine as builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

## 🚀 Iniciar el Proyecto

### Opción 1: Con Docker Compose (Recomendado)

```bash
# Desde la raíz del proyecto
docker-compose up -d

# Verificar servicios
docker-compose ps

# Ver logs
docker-compose logs -f backend
docker-compose logs -f frontend

# Detener
docker-compose down
```

### Opción 2: Local (Sin Docker)

```bash
# Terminal 1: Backend
cd backend
mvn clean install
mvn spring-boot:run

# Terminal 2: MySQL (requiere instalado localmente)
# Asegurar que MySQL esté corriendo en puerto 3306

# Terminal 3: Frontend
cd frontend
npm install
npm run dev
```

---

## ✅ Verificar Setup

```bash
# Backend health
curl http://localhost:8080/api/v1/health

# Frontend
http://localhost:3000

# Database
mysql -h localhost -u root -p -e "USE multirubro_db; SHOW TABLES;"
```

---

## 📝 Archivo .env.example

Crear archivos de configuración:

```bash
# backend/.env.example
SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/multirubro_db
SPRING_DATASOURCE_USERNAME=multirubro_user
SPRING_DATASOURCE_PASSWORD=multirubro_pass
SPRING_JPA_HIBERNATE_DDL_AUTO=validate
SERVER_PORT=8080

# frontend/.env.example
REACT_APP_API_URL=http://localhost:8080/api/v1
REACT_APP_ENV=development
```

---

## 🔄 Próximos Pasos

1. ✅ Crear estructura de carpetas
2. ✅ Inicializar backend y frontend
3. ✅ Levantar servicios con Docker Compose
4. ✅ Revisar QUICK_START.md para git workflow
5. ✅ Comenzar con Fase 1 según ROADMAP.md
