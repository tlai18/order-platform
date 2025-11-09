
---

# 🚀 Cloud-Native Order Management Platform: Learning Roadmap

## Project Vision

Build a cloud-native **Order Management Platform (OMP)**. This project demonstrates practical experience across all listed qualifications by producing GitHub-ready artifacts in a modern, secure, and highly scalable architecture.

**Core Stack:** React frontend, ASP.NET Core backend (C#), SQL Server, Kafka, GraphQL, Azure deployment, CI/CD via GitHub Actions, and container orchestration with Docker/Kubernetes.

---

## Phase 1 · Foundation Setup (Tooling)

* **Environment:** Install **.NET 8 SDK, Node 20 + pnpm, Docker Desktop, Azure CLI, kubectl, and Helm**.
* **Initial Repo:** Create GitHub repository (`order-platform`). Scaffold the solution (`dotnet new webapi`, `react-ts`, `.sln`).
* **Version Control:** Configure branch protection, Git flow, GitHub Issues/Projects, and a semantic PR template.
* **VSCode:** Configure essential extensions (C#, ESLint, GitHub Actions, Azure Tools, Kubernetes).

### Tool Verification

| Tool       | Version / Output           | Notes |
|------------|----------------------------|-------|
| .NET SDK   | `dotnet --info`            |       |
| Node.js    | `node -v`                  |       |
| pnpm       | `pnpm -v`                  |       |
| Docker     | `docker version`           |       |
| Azure CLI  | `az version`               |       |
| kubectl    | `kubectl version --client` |       |
| Helm       | `helm version`             |       |

---

## Phase 2 · Domain Modeling & Database (Data Integrity)

* **Schema Design:** Define tables: `Orders`, `Customers`, `Inventory`, `Shipments`, `AuditLog`.
* **Stored Procedures (SPROCs):** Craft **CRUD** and reporting procedures in `sql/procedures/*.sql`. Write functions for order total calculations and inventory adjustments. Execute changes via `dotnet ef migrations`.
* **Tests:** Add **Integration Tests (xUnit)** that call SPROCs directly through **Dapper** (micro-ORM).

---

## Phase 3 · ASP.NET Core REST API (Backend Logic)

* **Architecture:** Implement clean architecture layers (Domain, Application, Infrastructure, Presentation). Develop **REST endpoints** for orders, inventory, and customer profiles.
* **Security:** Apply **OWASP ASVS controls**: input validation with **FluentValidation**, output encoding, and rate limiting. Implement custom middleware for centralized exception handling and **Serilog** logging.
* **Unit Tests:** Cover controllers and services with **Moq** and **AutoFixture**. Aim for 80%+ coverage via **coverlet**.

---

## Phase 4 · React Frontend (UI/UX)

* **Stack:** Build with **React 18 + Vite + TypeScript**. Use **Zustand** for state, **React Query** for data fetching, and **Tailwind v4** for styling.
* **Features:** Develop a Dashboard showing KPIs, an order creation wizard, inventory management, and an audit viewer with **WebSocket** updates.
* **Testing:** Implement **Component tests** with **React Testing Library** and **E2E tests** with **Playwright**. Integrate accessibility checks (**axe-core**).

---

## Phase 5 · Event-Driven & Kafka (Real-Time Communication)

* **Producer:** Configure the backend to publish an event to **Kafka** (using **Confluent.Kafka**) upon successful order creation.
* **Local Environment:** Containerize a local Kafka cluster via **Docker Compose**.
* **Consumer:** Implement a **Background Service** that processes events, updates the `AuditLog`, and triggers an email simulation.
* **Testing:** Use **Testcontainers** for robust Kafka integration testing.

---

## Phase 6 · GraphQL Gateway (Flexible API Access)

* **Implementation:** Add a **Hot Chocolate** GraphQL endpoint that aggregates data from the existing REST APIs and direct SQL calls.
* **Features:** Support complex queries (`ordersByStatus`, `inventoryLevels`) and mutations.
* **Security:** Apply depth and complexity limits, and implement **persisted queries**.

---

## Phase 7 · Cloud-Native Packaging (Containerization)

* **Containerization:** Write robust **multi-stage Dockerfiles** for the API and frontend.
* **Local Stack:** Create a comprehensive Docker Compose stack for local development (API, React, SQL Server, Kafka, Redis).
* **Kubernetes:** Create a **Helm chart** (`charts/order-platform`) covering deployments, services, ingress, **ConfigMaps**, and secrets (using **Sealed Secrets** for local development).
* **Azure:** Provision **AKS, Azure SQL, Azure Event Hubs (Kafka API), and Application Insights** via **Bicep** or **Terraform**. Document all deployment steps.

---

## Phase 8 · CI/CD with GitHub Actions (Automation)

* **Pipelines:** Create automated workflows for:
    * **PR Validation:** Linting, unit tests, and Playwright E2E tests.
    * **Build & Push:** Building and pushing container images to a registry.
    * **Deployment:** Deploying the Helm chart to **AKS** using **OIDC** for secure authentication.
* **Environments:** Configure staging and production environments with mandatory **approvals**. Integrate **Trivy** image scanning for security checks.

---

## Phase 9 · Security Hardening (Defense-in-Depth)

* **OWASP Mapping:** Document mitigations across all phases (authentication, input validation, centralized logging, etc.).
* **JWT Auth:** Implement **JWT authentication** via **Azure AD** and store sensitive secrets securely in **Azure Key Vault**.
* **Threat Modeling:** Run a **STRIDE** session and capture all mitigation strategies in the repository documentation.

---

## Phase 10 · Agile Practice (Process)

* **Scrum Simulation:** Set up a feature backlog, perform story mapping, and create a sprint plan. Use **GitHub Projects** for the sprint board.
* **Retrospectives:** Conduct mock retrospectives using Markdown templates.
* **Documentation:** Write **ADRs** (Architecture Decision Records), API documentation (**Swagger, GraphQL schema**), runbooks, and a postmortem template.

---

## Phase 11 · Observability & Performance (Monitoring)

* **Telemetry:** Integrate **OpenTelemetry** for application tracing (API, Kafka producer/consumer). Ship logs and metrics to **Azure Monitor**.
* **Performance Tests:** Use **k6** to run load tests against key API endpoints.
* **Database Optimization:** Profile stored procedures with SQL Server tools and optimize indexes/execution plans.

---

## Phase 12 · Capstone Deliverables (Final Output)

* **Case Study:** Produce a comprehensive **README summary**, including **architecture diagrams (C4 model)** and the final security checklist.
* **Demo:** Record a short walkthrough video showcasing the primary features, the CI/CD pipelines in action, and the resulting observability dashboard in Azure Monitor.