# Eventra — Online Ticket Booking Platform

Discover experiences. Choose your seats. Book with confidence.

Eventra is a full-stack ticket-booking application for discovering movies and live events, selecting seats, managing bookings, and supporting digital ticket workflows. The project contains a modern web frontend, a Spring Boot REST API, PostgreSQL database configuration, developer documentation, and a Postman collection.

> **Project status:** Source code and local-development configuration are provided for development and evaluation. Verify every integration and environment setting before deploying publicly or processing real payments.

## Features

- Browse movies, events, venues, and experiences
- Search and city-aware discovery
- Interactive seat selection and booking workflows
- Booking checkout and pricing components
- Payment-provider abstraction with configurable mock and gateway integrations
- Digital ticket and QR validation workflows
- JWT-based authentication and role-aware access
- Email and in-app notification support
- Admin and partner management interfaces
- REST API documentation and Postman collection
- Docker Compose and database initialization support

## Technology Stack

| Layer | Technologies |
|---|---|
| Frontend | Next.js, React, TypeScript |
| UI | Tailwind CSS, Framer Motion, Lucide, Recharts |
| Client data and forms | TanStack Query, Zod, React Hook Form |
| Backend | Java 21, Spring Boot 3.5, Spring Security, Spring Data JPA |
| Database | PostgreSQL, Flyway migrations |
| Authentication | JWT and refresh-token flow |
| Payments | Provider abstraction for mock, Razorpay, Stripe, and PhonePe integrations |
| Email and tickets | Spring Mail, QR-code generation |
| Testing | JUnit, Vitest, Testing Library, Playwright |
| Local development | Docker, Docker Compose, Postman |

## Repository Structure

```text
.
├── backend/          Spring Boot API and migrations
├── frontend/         Next.js application and UI components
├── database/         SQL initialization scripts
├── docs/             Architecture and technical documentation
├── postman/          API collection for manual testing
├── docker-compose.yml
├── .env.example      Environment-variable template
└── README.md
```

## Prerequisites

- JDK 21
- Maven 3.9+
- Node.js LTS and npm
- Docker Desktop / Docker Engine with Docker Compose, or PostgreSQL installed locally

## Getting Started

### 1. Configure environment variables

From the project root, copy the example file:

**macOS / Linux**
```bash
cp .env.example .env
```

**Windows PowerShell**
```powershell
Copy-Item .env.example .env
```

Review the values and configure them for your environment. Never commit your real `.env` file or production credentials.

### 2. Start PostgreSQL

```bash
docker compose up -d postgres
```

Review `docker-compose.yml` and `.env.example` for the configured database name, port, and credentials.

### 3. Start the backend

```bash
cd backend
mvn spring-boot:run
```

The API typically runs at `http://localhost:8080` with the default local configuration. If enabled in the application configuration, Swagger UI is available at `http://localhost:8080/swagger-ui`.

### 4. Start the frontend

Open a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by the development server (commonly `http://localhost:3000`). Configure the API base URL using the environment variables documented in `.env.example`.

### Run the stack with Docker Compose

```bash
docker compose --profile app up --build
```

Stop the services with:

```bash
docker compose --profile app down
```

To also remove the local database volume (this deletes its data):

```bash
docker compose down -v
```

## Configuration and Security

- Use `.env.example` as a template; supply local values in an untracked `.env` file.
- Never commit payment secrets, database passwords, JWT signing secrets, SMTP passwords, or API tokens.
- Do not expose private credentials through variables prefixed with `NEXT_PUBLIC_`; those values may be included in the browser bundle.
- Verify payment status on the server and validate gateway webhook signatures. Do not trust client-side payment redirects or client-supplied prices.
- Configure HTTPS, CORS, secure cookies, rate limiting, logging, backups, and production secrets before deployment.
- Use sandbox/test credentials until payment flows have been reviewed end-to-end.

## Testing

Use the test scripts and configuration present in each project folder. Typical commands include:

```bash
# Backend
cd backend
mvn test

# Frontend (from the frontend directory)
npm test
```

Check the frontend `package.json` for the exact available scripts before running them; script names can vary by project setup.

## API Testing

The `postman/` directory contains a collection for exercising available endpoints. Import it into Postman and set the base URL and any required authentication variables for your local environment.

## Documentation

See the `docs/` directory for architecture and implementation notes. Review backend and frontend configuration files for the definitive list of supported settings and scripts.

## Contributing

1. Fork the repository and create a feature branch.
2. Keep changes focused and add or update tests where appropriate.
3. Never commit secrets or real customer/payment data.
4. Describe the change and validation steps in your pull request.

## License

No license has been specified yet. Unless a license is added, standard copyright applies and reuse/redistribution permissions are not automatically granted.
