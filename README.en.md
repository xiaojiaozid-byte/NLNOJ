# NLNOJ Online Judge System

A fully-featured Online Judge system supporting core functions such as problem management, code submission, contests, team collaboration, and forum discussions.

## Project Introduction

This project is a full-stack Online Judge platform designed with a decoupled frontend-backend architecture. The backend is built on Python FastAPI, providing RESTful API services; the frontend utilizes Vue 3 + TypeScript to build the user interface. The system supports code evaluation for multiple programming languages and includes complete functional modules for contests, teams, forums, tickets, etc.

## Tech Stack

### Backend

- **Framework**: FastAPI (Python 3.13)
- **Database**: SQLAlchemy ORM + Alembic Database Migration
- **Database Support**: SQLite (Development Environment), PostgreSQL (Production Environment)
- **Authentication**: JWT Token + Supabase
- **Email Service**: SMTP

### Frontend

- **Framework**: Vue 3 + Composition API
- **Language**: TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **State Management**: Pinia
- **Routing**: Vue Router

### Other Components

- **GCC Plugin**: judge-plugin (Prevents contestants from controlling compilation optimization levels)
- **Containerization**: Docker + Docker Compose

## Feature Highlights

### User System

- User Registration and Login (Supports email, username, Student ID, and other identifiers)
- JWT Token Authentication and Refresh Mechanism
- User Profile Management, Avatar/Banner Upload
- Theme Customization (Background Image, Light/Dark Mode)
- Follow/Fans System

### Problem Management

- Problem Creation, Editing, Deletion
- Problem Difficulty Grading and Tag Management
- Problem Source Tracking
- Test Case Management (Supports single addition and ZIP bulk import)
- Problem Public/Private Permission Control

### Code Evaluation

- Real-time Code Submission and Evaluation
- Support for Multiple Programming Languages
- Code Privacy Protection During Contests
- Evaluation Log Recording
- Evaluation Result Viewing

### Contest System

- Create Individual/Team Contests
- ACM Format Support
- Real-time Contest Ranking Updates
- Problem Visibility Control During Contests
- Invitation Code Registration Mechanism

### Team System

- Create and Manage Teams
- Team Private Question Bank
- Member Management and Audit
- Team Transfer and Disbandment

### Forum & Social

- Post Publishing and Commenting
- Sticky/Lock Functions
- @Mention Notifications
- Benben Activity Feed
- Daily Check-in

### Ticket System

- Submit Technical Issue Tickets
- Ticket Status Workflow
- Assign Responsible Person
- Attachment Upload

### Image Hosting System

- Image Upload and Management
- Watermark Processing (Text Watermarks)
- Storage Quota Management (Standard/Premium Space)

### Experience Shop

- Earn Experience Points via Check-in
- Exchange Experience for Tag Cards
- Contribution Point System

### Admin Panel

- User Management (Permission Modification, Ban, Password Reset)
- Batch User Operations
- Homepage Ad Management
- Evaluation Administrator Publication

## Project Structure

```
oj/
├── service/                 # Backend Service
│   ├── app/
│   │   ├── api/            # API Routes
│   │   ├── core/           # Core Configuration
│   │   ├── models/         # Data Models
│   │   ├── schemas/        # Pydantic Models
│   │   ├── services/       # Business Logic
│   │   └── utils/          # Utility Functions
│   ├── alembic/            # Database Migration
│   ├── scripts/            # Script Tools
│   └── tests/              # Test Cases
│
├── web/                     # Frontend Application
│   ├── src/
│   │   ├── api/            # API Client
│   │   ├── components/     # Common Components
│   │   ├── stores/         # Pinia State
│   │   ├── views/          # Page Views
│   │   └── utils/          # Utility Functions
│   └── public/             # Static Resources
│
├── judge-plugin/           # GCC Evaluation Plugin
│   └── no_opt_pragma.cc    # Prohibit Optimization Pragma Plugin
│
├── docker-compose.yml      # Docker Orchestration
└── DEPLOY_CHECKLIST.md     # Deployment Checklist
```

## Quick Start

### Prerequisites

- Python 3.13+
- Node.js 20+
- Docker (For Production Deployment)

### Local Development

#### Start Backend

```bash
cd service

# Install dependencies
pip install uv
uv sync

# Copy environment configuration
cp .env.example .env

# Initialize database (SQLite)
uv run alembic upgrade head

# Start service
uv run uvicorn app.main:app --reload
```

#### Start Frontend

```bash
cd web

# Install dependencies
npm install

# Start development server
npm run dev
```

#### Run with Docker

```bash
# Start all services
docker-compose up -d
```

### Configuration Instructions

Backend Configuration File `service/.env`:

```env
# Database Connection
DATABASE_URL=sqlite+aiosqlite:///./oj.db
# Or use PostgreSQL
DATABASE_URL=postgresql://user:pass@localhost:5432/oj

# JWT Secret
JWT_SECRET=your-secret-key

# Environment Mode
ENV=dev

# Supabase Configuration (Optional)
SUPABASE_URL=
SUPABASE_KEY=
```

## Deployment Guide

For detailed deployment steps, please refer to [DEPLOY_CHECKLIST.md](./DEPLOY_CHECKLIST.md).

### Basic Steps

1. Server Initialization, Install Docker
2. Upload Code to Server
3. Configure Environment Variables
4. Start Services
5. Verify Deployment

### Access Services

- Homepage: `http://ServerIP/`
- Login: `http://ServerIP/login`
- Admin Panel: `http://ServerIP/admin`

## API Documentation

Access after service startup:

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## Testing

```bash
cd service

# Run all tests
pytest

# Run specific tests
pytest tests/test_auth_flow.py
```

## Development Standards

### Backend

- Use Pydantic for data validation
- Use SQLAlchemy AsyncSession for database operations
- All API routes must include permission dependency checks

### Frontend

- Use TypeScript for type-safe development
- Components adopt Composition API style
- Styling uses Tailwind CSS utility classes

## License

This project is for learning and exchange purposes only.

## Related Documentation

- [Backend Detailed Documentation](./service/README.md)
- [Frontend Detailed Documentation](./web/README.md)
- [Database Configuration Guide](./service/SUPABASE_SETUP.md)
- [GCC Plugin Instructions](./judge-plugin/README.md)
- [Test Environment Setup](./service/scripts/README.md)
