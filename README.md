# Bank-Pro 🏦

A robust, production-ready backend banking service built with **Go**, featuring account management, user authentication, secure token handling, and comprehensive database operations.

## 🌟 Features

- **User Management**: Create and manage bank accounts with secure authentication
- **JWT & PASETO Authentication**: Dual token generation for enhanced security
- **Account Operations**: Core banking functionalities for account management
- **Transfer & Transactions**: Secure fund transfer and transaction tracking
- **PostgreSQL Database**: Reliable data persistence with connection pooling
- **REST API**: Clean, RESTful endpoints powered by Gin framework
- **Input Validation**: Comprehensive request validation using `go-playground/validator`
- **Unit Testing**: Full test coverage with mocking support
- **Docker Support**: Easy deployment with Docker and Docker Compose
- **Database Migrations**: Version-controlled schema management with SQL migrations

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Language** | Go 1.25.5 | Fast, efficient backend development |
| **Web Framework** | Gin | High-performance HTTP framework |
| **Database** | PostgreSQL 16 | Reliable relational database |
| **DB Driver** | pgx/v5 | Modern PostgreSQL driver |
| **DB Generation** | sqlc | Type-safe SQL queries |
| **Authentication** | JWT + PASETO | Secure token-based auth |
| **Validation** | go-playground/validator | Request validation |
| **Config Management** | Viper | Environment configuration |
| **Containerization** | Docker & Docker Compose | Deployment orchestration |
| **Testing** | testify + uber/mock | Testing & mocking utilities |

## 📋 Project Structure

```
Bank-Pro/
├── main.go                 # Application entry point
├── go.mod & go.sum        # Go dependencies
├── Dockerfile             # Container image definition
├── docker-compose.yaml    # Multi-container setup
├── Makefile              # Common development commands
├── sqlc.yaml             # SQL code generation config
├── app.env               # Environment variables
│
├── api/                  # REST API handlers & server
├── db/                   # Database layer
│   ├── migration/        # SQL migration files
│   ├── sqlc/            # Generated SQL queries
│   └── mock/            # Mock database for testing
├── token/               # JWT & PASETO token management
└── util/                # Utility functions & helpers
```

## 🚀 Quick Start

### Prerequisites

- Go 1.25.5 or higher
- Docker & Docker Compose
- PostgreSQL client (optional, for local development)

### Setup & Run

#### Option 1: Using Docker Compose (Recommended)

```bash
# Clone the repository
git clone https://github.com/niloy104/Bank-Pro.git
cd Bank-Pro

# Start services
docker-compose up --build

# API will be available at http://localhost:8080
```

#### Option 2: Local Development

```bash
# Clone repository
git clone https://github.com/niloy104/Bank-Pro.git
cd Bank-Pro

# Start PostgreSQL
make postgres

# Create database
make createdb

# Run migrations
make migrateup

# Start server
make server

# API will be running at configured SERVER_ADDRESS
```

## 📦 Available Make Commands

```bash
# Database operations
make postgres              # Start PostgreSQL container
make createdb             # Create 'simple_bank' database
make dropdb               # Drop 'simple_bank' database

# Database migrations
make migrateup            # Run all pending migrations
make migratedown          # Rollback all migrations
make migrateup1           # Run next 1 migration
make migratedown1         # Rollback 1 migration

# Code generation & testing
make sqlc                 # Generate type-safe SQL code
make test                 # Run all tests with coverage
make mock                 # Generate mock database for tests

# Development
make server               # Start the API server
```

## ⚙️ Configuration

Configuration is managed via environment variables. Create an `app.env` file:

```env
# Server Configuration
SERVER_ADDRESS=0.0.0.0:8080

# Database Configuration
DB_SOURCE=postgresql://root:secret@localhost:5432/simple_bank?sslmode=disable

# JWT/PASETO Configuration
TOKEN_SYMMETRIC_KEY=<your-32-character-key>
ACCESS_TOKEN_DURATION=15m
REFRESH_TOKEN_DURATION=24h
```

## 🔌 API Endpoints

### Authentication
- `POST /auth/login` - User login (returns JWT/PASETO token)
- `POST /auth/refresh` - Refresh authentication token

### Accounts
- `POST /accounts` - Create new account
- `GET /accounts/:id` - Get account details
- `GET /accounts` - List user accounts

### Transfers
- `POST /transfers` - Create fund transfer
- `GET /transfers/:id` - Get transfer details

### Transactions
- `GET /transactions` - List account transactions

*Detailed API documentation available in `/api` endpoint*

## 🧪 Testing

```bash
# Run all tests
make test

# Run specific test
go test -v ./api

# Run with coverage report
go test -cover ./...
```

Tests use mock databases and dependency injection for isolated, reliable testing.

## 📦 Build & Deployment

### Build Docker Image

```bash
# Build image
docker build -t bank-pro:latest .

# Run container
docker run -p 8080:8080 \
  -e DB_SOURCE=postgresql://root:secret@postgres:5432/simple_bank \
  bank-pro:latest
```

### Deploy with Docker Compose

```bash
docker-compose up -d
```

## 🔐 Security Features

- **Token-Based Authentication**: JWT and PASETO tokens
- **Password Encryption**: Secure hashing with `golang.org/x/crypto`
- **SQL Injection Prevention**: Type-safe queries via sqlc
- **Input Validation**: Comprehensive request validation
- **Environment-Based Config**: Sensitive data in environment variables
- **Connection Pooling**: Secure database connection management via pgxpool

## 📚 Dependencies

Key external dependencies:
- `github.com/gin-gonic/gin` - Web framework
- `github.com/golang-jwt/jwt/v5` - JWT token generation
- `github.com/o1egl/paseto` - PASETO token generation
- `github.com/jackc/pgx/v5` - PostgreSQL driver
- `golang.org/x/crypto` - Cryptographic functions
- `github.com/google/uuid` - UUID generation
- `github.com/spf13/viper` - Configuration management

See `go.mod` for complete dependency list.

## 🤝 Development Workflow

1. **Create Feature Branch**: `git checkout -b feature/your-feature`
2. **Make Changes**: Implement your feature
3. **Run Tests**: `make test` - ensure all tests pass
4. **Generate Code**: `make sqlc` - if database changes
5. **Commit**: Commit with meaningful messages
6. **Push & PR**: Create pull request for review

## 📊 Code Quality

- **Type Safety**: Full static typing with Go
- **Testing**: Comprehensive unit tests with mocking
- **Linting**: Go standard conventions followed
- **Documentation**: Inline comments for complex logic

## 🐛 Troubleshooting

### Port Already in Use
```bash
# Change SERVER_ADDRESS in app.env
SERVER_ADDRESS=0.0.0.0:8081
```

### Database Connection Error
```bash
# Verify PostgreSQL is running
docker ps | grep postgres

# Check DB_SOURCE connection string
```

### Migration Issues
```bash
# Reset migrations
make migratedown
make migrateup
```

## 📄 License

This project is licensed under the terms specified in the LICENSE file.

## 👤 Author

**niloy104** - [GitHub Profile](https://github.com/niloy104)

---

## 📈 Language Composition

- **Go**: 92% (Core application)
- **Shell**: 5.8% (Deployment scripts)
- **Makefile**: 1.5% (Build automation)
- **Dockerfile**: 0.7% (Container setup)

## 🌐 Resources

- [Go Documentation](https://golang.org/doc/)
- [Gin Framework Guide](https://github.com/gin-gonic/gin)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Documentation](https://docs.docker.com/)

---

**Built with ❤️ for secure, scalable banking backend systems**
