# Book My Venue - MVP

A production-grade venue booking platform built with Django, Django REST Framework, React, Vite, and PostgreSQL.

## Quick Start

### Prerequisites
- Docker & Docker Compose
- Git
- Python 3.10+ (for local development)
- Node.js 16+ (for local frontend development)

### Setup Local Development

```bash
# Clone the repository
git clone <repo-url>
cd book-my-venue

# Start services with Docker Compose
docker-compose up

# Backend will be available at http://localhost:8000
# Frontend will be available at http://localhost:5173
```

### Without Docker

**Backend**:
```bash
cd apps/api
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

**Frontend**:
```bash
cd apps/web
npm install
npm run dev
```

---

## Project Structure

```
book-my-venue/
├── apps/
│   ├── api/              # Django REST API backend
│   │   ├── manage.py
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   ├── config/       # Django settings
│   │   └── apps/         # Django apps (auth, venues, bookings, etc.)
│   └── web/              # React + Vite frontend
│       ├── package.json
│       ├── vite.config.ts
│       ├── tsconfig.json
│       ├── src/          # React components & pages
│       └── public/
├── packages/             # Shared utilities (future)
├── infra/               # Infrastructure & deployment
│   ├── docker-compose.yml
│   ├── docker-compose.prod.yml
│   └── nginx/
├── docs/                # Documentation
│   ├── 01-ARCHITECTURE.md
│   ├── 02-DATABASE-SCHEMA.md
│   ├── 03-API-SPECIFICATION.md
│   ├── 04-USER-STORIES.md
│   ├── 05-GITHUB-ISSUES-TEMPLATE.md
│   └── 06-SPRINT-PLAN.md
├── .github/
│   ├── workflows/       # CI/CD pipelines
│   └── ISSUE_TEMPLATE/  # Issue templates
├── docker-compose.yml   # Local development
└── README.md
```

---

## Documentation

Read the full documentation in the `docs/` directory:

1. **[Architecture](docs/01-ARCHITECTURE.md)** - System design and module breakdown
2. **[Database Schema](docs/02-DATABASE-SCHEMA.md)** - Database design and tables
3. **[API Specification](docs/03-API-SPECIFICATION.md)** - REST API endpoints and examples
4. **[User Stories](docs/04-USER-STORIES.md)** - Features and acceptance criteria
5. **[GitHub Issues Template](docs/05-GITHUB-ISSUES-TEMPLATE.md)** - How to create issues
6. **[Sprint Plan](docs/06-SPRINT-PLAN.md)** - 4-sprint development roadmap

---

## Technology Stack

### Backend
- Django 4.2+
- Django REST Framework
- PostgreSQL 14+
- JWT (djangorestframework-simplejwt)
- Celery (for async tasks - Phase 2)
- Redis (for caching - Phase 2)

### Frontend
- React 18+
- Vite
- TypeScript
- TailwindCSS
- React Query
- React Router v6
- Axios

### Infrastructure
- Docker & Docker Compose
- GitHub Actions (CI/CD)
- PostgreSQL (database)
- Gunicorn (WSGI server)
- Nginx (reverse proxy - future)

---

## API Base URL

**Development**: `http://localhost:8000/api/v1`
**Production**: `https://api.bookmyvenue.com/api/v1`

### Authentication

All requests require JWT token in Authorization header:
```
Authorization: Bearer {access_token}
```

### Key Endpoints

**Authentication**:
- `POST /auth/register` - Register new user
- `POST /auth/login` - Login user
- `POST /auth/token/refresh` - Refresh token
- `GET /auth/me` - Get current user

**Venues**:
- `GET /venues/` - List venues (with filtering)
- `POST /venues/` - Create venue (owner only)
- `GET /venues/{id}/` - Get venue details
- `PATCH /venues/{id}/` - Update venue (owner only)
- `DELETE /venues/{id}/` - Delete venue (owner only)

**Bookings**:
- `POST /bookings/` - Create booking request
- `GET /bookings/` - List user's bookings
- `POST /bookings/{id}/approve/` - Approve booking (owner only)
- `POST /bookings/{id}/reject/` - Reject booking (owner only)
- `POST /bookings/{id}/cancel/` - Cancel booking

**Availability**:
- `GET /venues/{id}/availability/` - Check availability
- `POST /venues/{id}/availability/bulk-create/` - Create availability slots

See [API Specification](docs/03-API-SPECIFICATION.md) for full details.

---

## Development Workflow

### 1. Create Feature Branch
```bash
git checkout -b feature/US-101-user-registration
```

### 2. Make Changes & Commit
```bash
git add .
git commit -m "feat: implement user registration endpoint (US-101)"
```

### 3. Push & Create Pull Request
```bash
git push origin feature/US-101-user-registration
```

### 4. Code Review & Merge
- Ensure CI/CD passes
- Get review approval
- Merge to main

### 5. Deploy
- Automatically deploys to staging
- Manual deployment to production

---

## Testing

### Backend Tests
```bash
cd apps/api
pytest  # Run all tests
pytest --cov  # With coverage report
```

### Frontend Tests
```bash
cd apps/web
npm test  # Run tests
npm run test:cov  # With coverage
```

---

## Database

### Run Migrations
```bash
cd apps/api
python manage.py migrate
```

### Create Superuser (Admin)
```bash
python manage.py createsuperuser
```

### Reset Database
```bash
python manage.py flush  # Clear all data
```

---

## Environment Variables

Create `.env` file in project root:

```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/bookmyvenue

# Django
DEBUG=True
SECRET_KEY=your-secret-key-here
ALLOWED_HOSTS=localhost,127.0.0.1

# JWT
JWT_ACCESS_TOKEN_LIFETIME=900  # 15 minutes
JWT_REFRESH_TOKEN_LIFETIME=604800  # 7 days

# Email (optional)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password

# Frontend
VITE_API_BASE_URL=http://localhost:8000/api/v1
```

---

## Git Workflow

### Branch Naming
- `feature/US-XXX-description` - New features
- `fix/issue-description` - Bug fixes
- `refactor/description` - Code refactoring
- `docs/description` - Documentation

### Commit Messages
```
feat: add user registration endpoint (US-101)
fix: fix booking status update bug
refactor: simplify venue filtering logic
docs: update API documentation
```

Use conventional commits format.

---

## Code Quality

### Backend
- **Linter**: Flake8 (PEP 8)
- **Formatter**: Black
- **Type Checker**: Mypy (future)
- **Coverage**: >80% target

### Frontend
- **Linter**: ESLint
- **Formatter**: Prettier
- **Type Checker**: TypeScript
- **Coverage**: >80% target

### Pre-commit Hooks
```bash
pip install pre-commit
pre-commit install
```

---

## Common Tasks

### Add New Django App
```bash
cd apps/api
python manage.py startapp myapp
```

### Add New NPM Package
```bash
cd apps/web
npm install package-name
```

### Create Database Migration
```bash
cd apps/api
python manage.py makemigrations
python manage.py migrate
```

### View API Documentation
Available at `http://localhost:8000/api/docs` (Swagger UI)

---

## Troubleshooting

### Docker Issues
```bash
# Clear all containers and volumes
docker-compose down -v

# Rebuild images
docker-compose build --no-cache

# Restart services
docker-compose up
```

### Database Issues
```bash
# Reset database
docker exec book-my-venue-api python manage.py flush

# Recreate migrations
docker exec book-my-venue-api python manage.py makemigrations
docker exec book-my-venue-api python manage.py migrate
```

### Frontend Build Issues
```bash
cd apps/web
rm -rf node_modules package-lock.json
npm install
npm run build
```

---

## Team Communication

- **Slack Channel**: #book-my-venue
- **Standup Time**: 9:30 AM IST Daily
- **Sprint Planning**: Every Monday
- **Sprint Review**: Every Friday

---

## Contributing Guidelines

1. Follow the code style (Black for Python, Prettier for JS)
2. Write tests for new features
3. Update documentation
4. Ensure all CI checks pass
5. Request review before merging
6. One commit per feature

---

## License

MIT License - See LICENSE file

---

## Support

For issues, questions, or suggestions:
- Create GitHub Issue
- Ask in Slack channel
- Contact technical lead

---

## Useful Links

- [Django Documentation](https://docs.djangoproject.com/)
- [DRF Documentation](https://www.django-rest-framework.org/)
- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

---

## Next Steps

1. ✅ Review all documentation in `docs/`
2. ✅ Setup local development environment
3. ✅ Create GitHub Milestones (Sprint 1-4)
4. ✅ Create GitHub Issues from user stories
5. ✅ Assign team members to Sprint 1 tasks
6. 🔄 Start Sprint 1 development

---

**Last Updated**: May 25, 2026  
**Current Phase**: MVP Planning & Setup  
**Next Milestone**: Sprint 1 Kickoff
