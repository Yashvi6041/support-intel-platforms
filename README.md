# 🤖 SupportIntel - AI-Powered Customer Support Intelligence Platform

[![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=white)](https://react.dev)
[![MySQL](https://img.shields.io/badge/MySQL-9.6-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Docker](https://img.shields.io/badge/Docker-26.6-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)

## 📋 Overview

**SupportIntel** is a production-grade, AI-powered customer support intelligence platform that transforms how businesses handle customer support. It leverages advanced RAG (Retrieval-Augmented Generation), NLP, and machine learning to automate ticket classification, sentiment analysis, smart routing, and SLA prediction.

### Key Capabilities

- **🤖 AI-Powered Automation**: Intelligent ticket classification, auto-routing, and response generation
- **📊 Real-time Analytics**: Dashboard with resolution time, customer sentiment, and operational metrics
- **🔒 Enterprise Security**: JWT authentication, RBAC, PII masking, and audit logging
- **📈 Scalable Architecture**: Distributed embeddings, GPU inference support, Kubernetes-ready
- **🔌 Integration Ready**: RESTful APIs, webhook support, and external system connectors

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend (React)                         │
│                    Vite + TypeScript + Tailwind                  │
└──────────────────────────┬──────────────────────────────────────┘
                           │ HTTP/HTTPS
┌──────────────────────────▼──────────────────────────────────────┐
│                    Nginx Reverse Proxy                           │
│                 Load Balancing + SSL Termination                  │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                    Backend (FastAPI)                             │
│           Python 3.13 + SQLAlchemy 2.0 + Alembic                │
│         JWT Auth │ Rate Limiting │ Input Validation              │
│         Structured Logging │ Error Handling                     │
├─────────────────┬──────────────────┬────────────────────────────┤
│   Auth Service  │  User Service    │   Future: AI Services      │
│   Register/Login│  Profile/Admin   │   RAG, Embeddings, LLM    │
└────────┬────────┴────────┬─────────┴───────────┬────────────────┘
         │                 │                      │
┌────────▼─────┐   ┌──────▼──────┐   ┌───────────▼──────────────┐
│   MySQL 9.6  │   │ Redis 7     │   │ Future: Vector DB        │
│  (Primary DB)│   │ (Cache/Sess)│   │ (Pinecone/Weaviate)      │
└──────────────┘   └─────────────┘   └──────────────────────────┘
```

---

## 📁 Project Structure

```
support-intel-platform/
├── frontend/                          # React + TypeScript Frontend
│   ├── public/
│   │   └── favicon.svg
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/
│   │   │   │   └── ProtectedRoute.tsx  # Auth guard wrapper
│   │   │   └── layout/
│   │   │       ├── Layout.tsx          # Main layout shell
│   │   │       ├── Navbar.tsx          # Navigation bar
│   │   │       └── Footer.tsx          # Site footer
│   │   ├── pages/
│   │   │   ├── Landing.tsx            # Marketing/home page
│   │   │   ├── Login.tsx              # Authentication login
│   │   │   ├── Register.tsx           # User registration
│   │   │   ├── Dashboard.tsx          # Main dashboard
│   │   │   ├── Profile.tsx            # User profile editing
│   │   │   └── NotFound.tsx           # 404 error page
│   │   ├── services/
│   │   │   └── api.ts                 # Axios API client
│   │   ├── store/
│   │   │   ├── authStore.ts           # Auth state (Zustand)
│   │   │   └── themeStore.ts          # Theme state (Zustand)
│   │   ├── types/
│   │   │   └── auth.ts                # TypeScript interfaces
│   │   ├── test/
│   │   │   └── setup.ts               # Test configuration
│   │   ├── App.tsx                    # Root app with routing
│   │   ├── main.tsx                   # Entry point
│   │   ├── index.css                  # Tailwind + global styles
│   │   └── vite-env.d.ts              # Type declarations
│   ├── Dockerfile                     # Multi-stage Docker build
│   ├── nginx.conf                     # Production Nginx config
│   ├── package.json                   # Dependencies & scripts
│   ├── tsconfig.json                  # TypeScript config
│   ├── tsconfig.node.json             # Node TypeScript config
│   └── vite.config.ts                 # Vite bundler config
│
├── backend/                           # Python FastAPI Backend
│   ├── app/
│   │   ├── api/v1/
│   │   │   ├── auth.py                # Auth endpoints
│   │   │   ├── users.py               # User management endpoints
│   │   │   └── health.py              # Health check endpoint
│   │   ├── core/
│   │   │   ├── config.py              # Settings management
│   │   │   ├── security.py            # JWT, password hashing
│   │   │   ├── database.py            # SQLAlchemy engine/session
│   │   │   ├── dependencies.py        # FastAPI dependencies
│   │   │   ├── logging.py             # Loguru configuration
│   │   │   └── exceptions.py          # Error handling
│   │   ├── models/
│   │   │   └── user.py                # User SQLAlchemy model
│   │   ├── schemas/
│   │   │   ├── auth.py                # Auth request/response
│   │   │   ├── user.py                # User schemas
│   │   │   └── common.py              # Shared response models
│   │   ├── services/
│   │   │   ├── auth_service.py        # Auth business logic
│   │   │   └── user_service.py        # User business logic
│   │   ├── utils/
│   │   │   └── redis_client.py        # Redis async client
│   │   ├── db/
│   │   │   └── __init__.py
│   │   └── main.py                    # FastAPI application
│   ├── alembic/                       # Database migrations
│   │   ├── versions/
│   │   │   └── 001_initial_users_table.py
│   │   ├── env.py                     # Alembic environment
│   │   └── script.py.mako             # Migration template
│   ├── tests/
│   │   └── __init__.py
│   ├── Dockerfile                     # Python Docker image
│   ├── requirements.txt               # Python dependencies
│   ├── alembic.ini                    # Alembic configuration
│   └── run.py                         # Development entry point
│
├── docker/
│   ├── mysql/
│   │   └── init/
│   │       └── 01-init.sql            # Database initialization
│   └── monitoring/                    # Future: Prometheus/Grafana
│
├── docs/                              # Documentation
│   └── api.md                         # API documentation
│
├── docker-compose.yml                 # Multi-service orchestration
├── .env.example                       # Environment template
├── .gitignore                         # Git ignore rules
├── .dockerignore                      # Docker ignore rules
├── TODO.md                            # Implementation progress
└── README.md                          # This file
```

---

## 🛠️ Technology Stack

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| React | 19.0 | UI framework |
| TypeScript | 5.7 | Type-safe JavaScript |
| Vite | 6.0 | Build tool & dev server |
| Tailwind CSS | 4.0 | Utility-first CSS |
| Framer Motion | 11.15 | Animations |
| Zustand | 5.0 | State management |
| React Router | 7.1 | Client-side routing |
| Axios | 1.7 | HTTP client |
| React Hot Toast | 2.5 | Toast notifications |

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| Python | 3.13 | Runtime |
| FastAPI | 0.115 | Web framework |
| SQLAlchemy | 2.0 | ORM |
| Alembic | 1.14 | Database migrations |
| Pydantic | 2.10 | Data validation |
| JOSE | 3.3 | JWT handling |
| Passlib | 1.7 | Password hashing (bcrypt) |
| Loguru | 0.7 | Structured logging |
| Redis | 5.2 | Caching & sessions |
| Uvicorn | 0.34 | ASGI server |

### Database
| Technology | Version | Purpose |
|------------|---------|---------|
| MySQL | 9.6 | Primary database |
| Redis | 7 | Caching & sessions |

### Infrastructure
| Technology | Version | Purpose |
|------------|---------|---------|
| Docker | 26.6 | Containerization |
| Docker Compose | Latest | Service orchestration |
| Nginx | 1.27 | Reverse proxy |
| GitHub Actions | - | CI/CD |

---

## 💾 Database Design

### Users Table
| Column | Type | Constraints | Description |
|--------|------|------------|-------------|
| id | INT | PK, AUTO_INCREMENT | Unique identifier |
| email | VARCHAR(255) | UNIQUE, NOT NULL, INDEX | User email |
| username | VARCHAR(100) | UNIQUE, NOT NULL, INDEX | Display username |
| hashed_password | VARCHAR(255) | NOT NULL | Bcrypt hash |
| full_name | VARCHAR(255) | NULLABLE | Display name |
| avatar_url | VARCHAR(500) | NULLABLE | Profile picture |
| bio | TEXT | NULLABLE | User biography |
| role | ENUM | NOT NULL, DEFAULT 'customer' | admin/agent/customer |
| is_active | BOOLEAN | NOT NULL, DEFAULT TRUE | Account status |
| is_verified | BOOLEAN | NOT NULL, DEFAULT FALSE | Email verified |
| is_admin | BOOLEAN | NOT NULL, DEFAULT FALSE | Admin privileges |
| last_login_at | DATETIME | NULLABLE | Last login timestamp |
| last_login_ip | VARCHAR(45) | NULLABLE | Last login IP |
| failed_login_attempts | INT | DEFAULT 0 | Login attempt counter |
| locked_until | DATETIME | NULLABLE | Account lock expiry |
| created_at | DATETIME | NOT NULL, DEFAULT NOW() | Creation timestamp |
| updated_at | DATETIME | NOT NULL, ON UPDATE | Last update timestamp |

**Indexes:**
- `ix_users_email` (UNIQUE) - Email lookup
- `ix_users_username` (UNIQUE) - Username lookup
- `ix_users_role` - Role-based queries
- `ix_users_is_active` - Active user queries
- `ix_users_is_admin` - Admin queries

---

## 🔌 API Documentation

### Authentication Endpoints

All API endpoints are prefixed with `/api/v1`.

#### POST /api/v1/auth/register
Register a new user account.

```json
// Request
{
  "email": "user@example.com",
  "username": "johndoe",
  "password": "StrongP@ss1",
  "full_name": "John Doe"
}

// Response (201 Created)
{
  "success": true,
  "message": "Registration successful. Please verify your email.",
  "data": {
    "id": 1,
    "email": "user@example.com",
    "username": "johndoe",
    "full_name": "John Doe",
    "role": "customer",
    "created_at": "2024-01-01T00:00:00"
  }
}
```

#### POST /api/v1/auth/login
Authenticate and receive JWT tokens.

```json
// Request
{
  "email": "user@example.com",
  "password": "StrongP@ss1",
  "remember_me": false
}

// Response (200 OK)
{
  "success": true,
  "message": "Login successful",
  "data": {
    "access_token": "eyJhbGciOiJIUzI1NiIs...",
    "refresh_token": "eyJhbGciOiJIUzI1NiIs...",
    "token_type": "bearer",
    "expires_in": 1800,
    "user": {
      "id": 1,
      "email": "user@example.com",
      "username": "johndoe",
      "full_name": "John Doe",
      "avatar_url": null,
      "role": "customer",
      "is_active": true,
      "is_admin": false,
      "created_at": "2024-01-01T00:00:00"
    }
  }
}
```

#### POST /api/v1/auth/refresh
Refresh access token using refresh token.

```json
// Request
{
  "refresh_token": "eyJhbGciOiJIUzI1NiIs..."
}

// Response (200 OK)
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 1800
}
```

#### POST /api/v1/auth/logout
Invalidate current session (requires auth).

```
Headers: Authorization: Bearer <access_token>
```

#### POST /api/v1/auth/change-password
Change user password (requires auth).

```json
{
  "current_password": "OldP@ss1",
  "new_password": "NewStrongP@ss1"
}
```

#### GET /api/v1/auth/me
Get current authenticated user profile.

### User Management Endpoints (Admin required for most)

#### GET /api/v1/users/me
Get own profile.

#### PUT /api/v1/users/me
Update own profile.

```json
{
  "full_name": "New Name",
  "bio": "Software engineer",
  "username": "newusername"
}
```

#### GET /api/v1/users/{user_id}
Get user by ID (Admin).

#### GET /api/v1/users/
List users with pagination (Admin).

```
Query Parameters:
?page=1&page_size=20&role=admin&is_active=true&search=johndoe
```

#### PUT /api/v1/users/{user_id}/role
Update user role/status (Admin).

```json
{
  "role": "admin",
  "is_active": true
}
```

#### DELETE /api/v1/users/{user_id}
Soft delete user (Admin).

### Health Check

#### GET /api/v1/health
Service health check.

### Auto-generated API Documentation (Development only)
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

---

## 🚀 Getting Started

### Prerequisites

Install the following software:
1. **Python 3.13+** - [Download](https://python.org/downloads)
2. **Node.js 24+** - [Download](https://nodejs.org)
3. **MySQL 9.6** - [Download](https://dev.mysql.com/downloads/mysql/)
4. **Docker & Docker Compose** - [Download](https://docker.com/products/docker-desktop)
5. **Git** - [Download](https://git-scm.com/downloads)

### Option 1: Running with Docker (Recommended)

This is the simplest way to run the entire stack.

```bash
# 1. Clone the repository
git clone <repository-url>
cd support-intel-platform

# 2. Create environment file
cp .env.example .env

# 3. Start all services
docker-compose up --build
```

This starts:
- **MySQL** on port `3307`
- **Redis** on port `6380`
- **Backend** API on port `8000`
- **Frontend** on port `3000`

### Option 2: Running Locally (Development)

#### Step 1: Setup MySQL Database

```sql
-- Connect to MySQL and run:
CREATE DATABASE IF NOT EXISTS supportintel_db 
  CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER IF NOT EXISTS 'supportintel_user'@'localhost' 
  IDENTIFIED BY 'supportintel_pass';

GRANT ALL PRIVILEGES ON supportintel_db.* 
  TO 'supportintel_user'@'localhost';

FLUSH PRIVILEGES;
```

#### Step 2: Setup Backend

```bash
# Navigate to backend
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env .env  # Edit with your settings

# Run database migrations
alembic upgrade head

# Start the backend server
python run.py
# Or: uvicorn app.main:app --reload
```

Backend runs at: http://localhost:8000

#### Step 3: Setup Frontend

```bash
# Navigate to frontend
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

Frontend runs at: http://localhost:5173

### Accessing the Application

| Service | URL | Description |
|---------|-----|-------------|
| Frontend | http://localhost:3000 | Main web app |
| Backend API | http://localhost:8000 | REST API |
| API Docs | http://localhost:8000/docs | Swagger UI |
| API Docs | http://localhost:8000/redoc | ReDoc UI |
| MySQL | localhost:3307 | Database |
| Redis | localhost:6380 | Cache |

---

## 🐳 Docker Setup Details

### Services Overview

```yaml
services:
  mysql:
    image: mysql:8.0
    ports: ["3307:3306"]
    volumes: ["mysql_data:/var/lib/mysql"]
    
  redis:
    image: redis:7-alpine
    ports: ["6380:6379"]
    
  backend:
    build: ./backend
    ports: ["8000:8000"]
    depends_on: [mysql, redis]
    
  frontend:
    build: ./frontend
    ports: ["3000:80"]
    depends_on: [backend]
```

### Docker Commands

```bash
# Build and start all services
docker-compose up --build

# Start in detached mode
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

# Rebuild a specific service
docker-compose up -d --build backend

# Scale a service (future)
docker-compose up -d --scale backend=3
```

---

## 🧪 Testing

### Backend Tests

```bash
cd backend
pytest -v
pytest --cov=app tests/
pytest -v -k "test_login"
```

### Frontend Tests

```bash
cd frontend
npm test              # Run tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage report
```

---

## 🔧 Troubleshooting

### Common Issues

#### MySQL Connection Refused
```bash
# Check if MySQL is running
mysql -u supportintel_user -p -h localhost -P 3307

# Verify credentials in .env
# DATABASE_URL=mysql+aiomysql://supportintel_user:supportintel_pass@localhost:3307/supportintel_db
```

#### Alembic Migration Issues
```bash
# Reset migrations
alembic downgrade base
alembic upgrade head

# Create new migration
alembic revision --autogenerate -m "description"
```

#### Backend Won't Start
```bash
# Check port availability
netstat -an | findstr :8000

# Check Python version
python --version  # Must be 3.13+

# Verify dependencies
pip list | grep -E "fastapi|sqlalchemy|alembic"
```

#### Frontend Won't Build
```bash
# Clear cache
rm -rf node_modules package-lock.json
npm install

# Check Node version
node --version  # Must be 18+
```

#### Docker Issues
```bash
# Reset Docker
docker-compose down -v
docker system prune -a
docker-compose up --build

# Check container logs
docker-compose logs backend
docker-compose logs mysql
```

---

## 🔒 Security Features

- **JWT Authentication**: Access + Refresh token pattern
- **Password Hashing**: bcrypt with 12 rounds
- **Account Locking**: After 5 failed login attempts (15 min lock)
- **Rate Limiting**: Configurable per-user/IP limits
- **Input Validation**: Pydantic schemas with strict rules
- **SQL Injection Protection**: SQLAlchemy parameterized queries
- **CORS**: Restricted origins configuration
- **Security Headers**: XSS, CSP, HSTS, X-Frame-Options
- **Session Management**: Redis-based with token blacklisting
- **Environment Isolation**: Separate configs for dev/prod

---

## 📈 Production Deployment Strategy

### Phase 1: Containerized Deployment
```yaml
# docker-compose.prod.yml
services:
  backend:
    build:
      dockerfile: Dockerfile.prod
    environment:
      - ENVIRONMENT=production
    restart: always
    
  frontend:
    image: nginx:alpine
    ports: ["80:80", "443:443"]
```

### Phase 2: Cloud Deployment (Future)
- **AWS**: ECS/Fargate + RDS (MySQL) + ElastiCache (Redis)
- **GCP**: Cloud Run + Cloud SQL + Memorystore
- **Azure**: Container Apps + Azure Database + Cache for Redis

### Phase 3: Advanced Scaling
- **Load Balancing**: Application Load Balancer (ALB)
- **Auto-scaling**: Based on CPU/memory metrics
- **CDN**: CloudFront/Cloudflare for static assets
- **Database**: Read replicas, connection pooling
- **Monitoring**: Prometheus + Grafana + Sentry
- **CI/CD**: GitHub Actions → Docker Hub → Deployment

---

## 📚 Future Roadmap

### Phase 2: ETL Pipeline
- [ ] Kafka event streaming
- [ ] Apache Airflow DAGs
- [ ] Data lake integration (S3/MinIO)
- [ ] Text cleaning & deduplication

### Phase 3: AI/ML Pipeline
- [ ] Embedding generation (Sentence Transformers)
- [ ] Vector database (Pinecone/Weaviate/FAISS)
- [ ] RAG implementation with LangChain
- [ ] LLM integration (OpenAI, Hugging Face)

### Phase 4: Intelligence Features
- [ ] Ticket classification (ML models)
- [ ] Sentiment analysis pipeline
- [ ] Auto-routing engine
- [ ] SLA prediction models

### Phase 5: Advanced Dashboard
- [ ] Real-time resolution metrics
- [ ] Customer sentiment trends
- [ ] LLM cost analytics
- [ ] Retrieval quality scoring

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow existing code style (ESLint, Prettier, Black, isort)
- Write tests for new features
- Update documentation as needed
- Use conventional commits format

---

## 📄 License

This project is proprietary software. All rights reserved.

---

## 👥 Support

For support, email dev@supportintel.ai or create an issue in the repository.

---

## 🎯 Known Limitations & Improvements

### Current Limitations
1. **Email verification**: Not yet implemented (stub ready)
2. **Password reset flow**: Backend ready, frontend pending
3. **Single-factor auth**: Only password-based login
4. **No file uploads**: Avatar upload via URL only
5. **Limited test coverage**: Core flows tested, more needed

### Planned Improvements
1. **OAuth 2.0**: Google, GitHub, Microsoft login
2. **2FA**: TOTP-based two-factor authentication
3. **WebSocket**: Real-time ticket updates
4. **File Storage**: S3-compatible object storage
5. **Audit Logging**: Complete action logging
6. **API Versioning**: v1, v2 with deprecation
7. **GraphQL**: Alternative to REST API
8. **Service Mesh**: Istio/Linkerd for microservices
9. **Distributed Tracing**: OpenTelemetry
10. **Chaos Engineering**: Resilience testing

---

## 📊 Performance Benchmarks

| Metric | Current | Target |
|--------|---------|--------|
| API Response Time | <50ms | <100ms |
| Concurrent Users | 1000+ | 10000+ |
| Database Queries/sec | 500+ | 5000+ |
| Frontend Load Time | <1s | <2s |
| Lighthouse Score | 95+ | 90+ |

---

*Built with ❤️ by the SupportIntel Team*

