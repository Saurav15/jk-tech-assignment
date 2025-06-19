# Scalable AI PDF Summary Generator

A scalable microservices-based application for generating AI-powered PDF summaries, supporting multiple user roles (Admin, Editor, Viewer). The system leverages asynchronous processing for PDF analysis and provides a robust API layer for user and document management.

## 🚀 What Does This Application Do?

- **AI PDF Summary Generation:** Upload PDFs and receive AI-generated summaries.
- **User Roles:**
  - **Admin:** Manage users, documents, and system settings.
  - **Editor:** Upload and manage documents.
  - **Viewer:** View summaries and documents.
- **Microservices Architecture:**
  - **NestJS Backend:** Exposes REST APIs, handles authentication, user management, and document ingestion.
  - **Python Event Consumer:** Asynchronously processes and analyzes PDFs, generating summaries using AI.
- **Asynchronous Processing:** PDF analysis is offloaded to the Python service via RabbitMQ for scalability and responsiveness.

---

## 🛠️ Quick Start Guide

### 1. Clone the Project and Submodules

```bash
git clone --recurse-submodules https://github.com/Saurav15/pdf-analyzer-microservice.git
cd pdf-analyzer-microservice
```

### 2. Backend Environment Setup

- Go to the backend directory:
  ```bash
  cd backend
  ```
- Add the required environment variables in `.env.development.local` or `.env` (depending on your environment). Refer to the backend README for details.

### 3. Python Event Consumer Environment Setup

- Go to the Python event consumer directory:
  ```bash
  cd ../python-event-consumer
  ```
- Add the required environment variables in a `.env` file. Reference can be taken from `.env.example` in the same directory.

### 4. Run the Complete Project (All Services)

- Return to the project root and start all services using Docker Compose:
  ```bash
  docker compose -f docker-compose.dev.yml --profile full up --build
  ```
- **Note:** Database migrations and seeders are run automatically during startup.

### 5. Accessing the Services

- **API Documentation (Swagger):** [http://localhost:3000/api/docs](http://localhost:3000/api/docs)
- **RabbitMQ UI:** [http://localhost:15672](http://localhost:15672) (ID: `guest`, PW: `guest`)
- **pgAdmin:** [http://localhost:8080/](http://localhost:8080/) (Email: `admin@admin.com`, PW: `admin123`)

---

## 🛑 Stopping the Services

- To stop and remove containers:
  ```bash
  docker compose -f docker-compose.dev.yml down
  ```
- To stop and remove containers **and** volumes:
  ```bash
  docker compose -f docker-compose.dev.yml down --volumes
  ```

---

## 🧩 Docker Compose Profiles

- **full**: Runs all services (backend, python consumer, postgres, rabbitmq, pgAdmin). Use for full development and integration testing.
- **infra**: Runs only infrastructure services (postgres, rabbitmq, pgAdmin). Use when developing a single microservice locally and only need the supporting infrastructure.
- **backend**: Runs backend service and infrastructure. Use when working only on the backend.
- **python**: Runs python event consumer and infrastructure. Use when working only on the Python service.

Start a specific profile by replacing `full` in the up command, e.g.:

```bash
docker compose -f docker-compose.dev.yml --profile backend up --build
```

---

## Microservice Development

Each microservice can be developed and tested independently. Refer to the individual README files in each service directory for specific development instructions:

- [Backend Service Documentation](./backend/README.md)
- [Python Event Consumer Documentation](./python-event-consumer/README.md)

---

## Contributing

1. Create a new branch for your feature
2. Make your changes
3. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For any questions or issues, please create an issue in the respective service's repository or contact the maintainers.
