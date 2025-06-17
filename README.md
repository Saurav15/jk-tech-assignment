# JK Tech Assignment - Microservices Architecture

This repository contains a collection of microservices that work together to form a complete application. The project uses Git submodules to manage multiple microservices in a single repository, making it easier to maintain and coordinate between different services.

## Repository Structure

The project consists of the following microservices:

1. **Backend Service** (`/backend`)

   - NestJS-based REST API service
   - Handles core business logic and data management
   - Features authentication, database operations, and API endpoints
   - Built with TypeScript, TypeORM, and PostgreSQL

2. **Python Event Consumer** (`/python-event-consumer`)
   - Python-based event processing service
   - Handles asynchronous event processing
   - Integrates with the backend service

## Git Submodules

This repository uses Git submodules to manage the microservices. Each service is maintained in its own repository and linked to this main repository. This approach allows for:

- Independent version control for each service
- Easier maintenance and updates
- Clear separation of concerns
- Simplified dependency management

### Submodule Structure

```
jk-tech-assignment/
├── backend/                  # NestJS Backend Service
│   └── [NestJS application files]
├── python-event-consumer/    # Python Event Consumer Service
│   └── [Python application files]
└── .gitmodules              # Git submodule configuration
```

## Getting Started

### Prerequisites

- Git
- Node.js (v16 or higher)
- Python 3.x
- PostgreSQL
- Docker (optional)

### Initial Setup

1. Clone the main repository:

   ```bash
   git clone https://github.com/your-username/jk-tech-assignment.git
   cd jk-tech-assignment
   ```

2. Initialize and update submodules:

   ```bash
   # Initialize submodules
   git submodule init

   # Update submodules recursively (this will also initialize any nested submodules)
   git submodule update --init --recursive
   ```

   Alternatively, you can clone the repository with submodules in one command:

   ```bash
   git clone --recurse-submodules https://github.com/your-username/jk-tech-assignment.git
   ```

3. Set up the Backend Service:

   ```bash
    # cd ./backend
    # Follow the setup instructions in the service's README
   ```

4. Set up the Python Event Consumer:
   ```bash
   cd ../python-event-consumer
   # Follow the setup instructions in the service's README
   ```

## 🐳 Docker Compose Setup

This project is composed of multiple services managed via **Docker Compose**. The services include:

- `backend` – Node.js/NestJS application
- `python-consumer` – RabbitMQ event consumer written in Python
- `postgres` – PostgreSQL database
- `rabbitmq` – RabbitMQ message broker with management UI
- `pgadmin` – PostgreSQL administration tool

### 📁 Environment Setup

Create a `.env` file in the root of the project with the following structure:

```env
# Database
POSTGRES_HOST=postgres
POSTGRES_PORT=5432
POSTGRES_USER=avnadmin
POSTGRES_PASSWORD=AVNS_yS3ijuz-v8Jd0OqHwQb
POSTGRES_DB=defaultdb

# Application
NODE_ENV=development
PORT=3000

# JWT
JWT_SECRET=this_is_a_very_long_secret_key_for_jwt
JWT_EXPIRATION=1d

# AWS S3
AWS_ACCESS_KEY_ID=AKIA44J7D6M4RFND5LDN
AWS_SECRET_ACCESS_KEY=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
AWS_REGION=us-east-1
AWS_BUCKET_NAME=jk-tech--document-upload

# RabbitMQ
RABBITMQ_USER=guest
RABBITMQ_PASSWORD=guest
RABBITMQ_QUEUE=documents_queue
```

### 🐳 Docker Compose Usage

The Compose setup uses a custom file: `docker-compose.local.yml`.

#### 🔧 Start All Services (Recommended for Full Local Dev)

This starts:

- Backend
- Python consumer
- Postgres
- RabbitMQ
- PgAdmin

```bash
docker compose -f docker-compose.local.yml --profile full up --build
```

#### 🧪 Start Only Infrastructure Services

If you're only working on one codebase and just need RabbitMQ, Postgres, and PgAdmin:

```bash
docker compose -f docker-compose.local.yml --profile infra up --build
```

You can omit `--build` if you haven't made Dockerfile changes:

```bash
docker compose -f docker-compose.local.yml --profile full up
```

### 🛑 Stopping the Services

Stop and remove containers:

```bash
docker compose -f docker-compose.local.yml down
```

To stop but preserve volumes:

```bash
docker compose -f docker-compose.local.yml down --volumes
```

### 🧩 Profiles Summary

| Profile | Includes                            | Use Case                         |
| ------- | ----------------------------------- | -------------------------------- |
| `infra` | `postgres`, `rabbitmq`, `pgadmin`   | For infrastructure-only usage    |
| `full`  | All services incl. backend & Python | For full development environment |

## Development

Each microservice can be developed and tested independently. Refer to the individual README files in each service directory for specific development instructions:

- [Backend Service Documentation](./backend/README.md)
- [Python Event Consumer Documentation](./python-event-consumer/README.md)

## Contributing

1. Create a new branch for your feature
2. Make your changes
3. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For any questions or issues, please create an issue in the respective service's repository or contact the maintainers.
