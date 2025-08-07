# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

OWASP Juice Shop is an intentionally insecure web application designed for security training, awareness demonstration, and CTF events. It's a Node.js/Express backend with an Angular frontend that demonstrates various web application security vulnerabilities.

## Common Development Commands

### Build Commands
- `npm run build:frontend` - Build Angular frontend
- `npm run build:server` - Compile TypeScript backend to JavaScript
- `npm run postinstall` - Full setup: install frontend deps, build frontend, build server

### Development Commands
- `npm run serve` - Run backend and frontend concurrently (production mode)
- `npm run serve:dev` - Run with ts-node-dev for hot reloading (development mode)
- `npm start` - Start production server from compiled build/

### Testing Commands
- `npm test` - Run frontend unit tests and server tests
- `npm run test:server` - Run backend unit tests with Mocha
- `npm run test:api` - Run API tests with Frisby/Jest
- `npm run frisby` - Run API integration tests
- `npm run cypress:open` - Open Cypress for E2E testing
- `npm run cypress:run` - Run Cypress E2E tests headless

### Code Quality Commands
- `npm run lint` - Lint backend TypeScript and frontend code
- `npm run lint:fix` - Auto-fix linting issues where possible
- `npm run lint:config` - Validate YAML configuration files

### Packaging Commands
- `npm run package` - Create distribution package with Grunt
- `npm run package:ci` - Create CI/production package

## High-Level Architecture

### Backend Structure
- **Entry Point**: `app.ts` → `server.ts` (main Express application)
- **Routes**: `/routes/` - API endpoints and route handlers organized by feature
- **Models**: `/models/` - Sequelize ORM models for database entities
- **Libraries**: `/lib/` - Utility functions, security helpers, startup procedures
- **Data Layer**: `/data/` - Database initialization, static data, and data creation utilities

### Frontend Structure
- **Angular App**: `/frontend/src/app/` - Complete Angular application
- **Components**: Feature-based component organization (basket, login, score-board, etc.)
- **Services**: Angular services for API communication and state management
- **Assets**: Static files, i18n translations, images, and videos

### Key Architectural Patterns

**Backend**:
- Express.js REST API with finale-rest for automatic CRUD endpoints
- Sequelize ORM with SQLite database
- JWT-based authentication with custom security middleware
- Challenge-based vulnerability system with verification hooks
- File upload handling with multer (memory and disk storage)
- Real-time features via Socket.IO websockets

**Frontend**:
- Angular SPA with Material Design components
- Service-based architecture for API communication
- Component-based UI with feature modules
- Internationalization (i18n) support for 40+ languages
- Responsive design with SCSS styling

### Security Architecture (Intentionally Vulnerable)
The application deliberately includes security vulnerabilities:
- SQL injection, XSS, CSRF vulnerabilities
- Broken authentication and authorization
- Security misconfigurations
- Insecure direct object references
- File upload vulnerabilities
- Path traversal issues

### Database Models
Key entities: User, Product, Basket, BasketItem, Challenge, Feedback, Address, Card, Wallet, SecurityQuestion, SecurityAnswer

### Configuration System
- `/config/` directory with YAML configuration files
- Environment-specific configs (default, test, ctf, tutorial, etc.)
- Schema validation via `config.schema.yml`

## Development Notes

### TypeScript Configuration
- Backend: `tsconfig.json` - compiles to `/build/` directory
- Frontend: `tsconfig.base.json` + component-specific configs

### Testing Strategy
- Backend: Mocha + Chai for unit tests, Frisby for API tests
- Frontend: Jasmine + Karma for unit tests, Cypress for E2E
- Test coverage reports generated in `/build/reports/coverage/`

### File Upload Handling
Two upload strategies:
- Memory storage: For profile images, file analysis (200KB limit)
- Disk storage: For memory/photo uploads (saved to frontend assets)

### Challenge System
Challenges are verified through middleware hooks that detect when vulnerabilities are exploited. Challenge data stored in `/data/static/challenges.yml`.

### Vulnerability Demonstration
Code includes intentional vulnerabilities marked with `vuln-code-snippet` comments for educational purposes.

### Internationalization
Full i18n support with translation files in `/data/static/i18n/` and frontend `/assets/i18n/`.

### Build Process
Frontend builds to `/frontend/dist/frontend/` and is served statically by Express. Backend TypeScript compiles to `/build/` directory.