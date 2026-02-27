# PoultryAI Setup Guide

This guide provides detailed instructions for setting up the PoultryAI project on your local machine.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [Backend Setup](#backend-setup)
4. [Frontend Setup](#frontend-setup)
5. [Database Setup](#database-setup)
6. [Environment Configuration](#environment-configuration)
7. [Running the Application](#running-the-application)
8. [Testing](#testing)
9. [Deployment](#deployment)
10. [Troubleshooting](#troubleshooting)

## Prerequisites

Before starting, ensure you have the following installed on your system:

### Required Software

- **Python 3.10+**: Download from [python.org](https://python.org)
- **Node.js 18+**: Download from [nodejs.org](https://nodejs.org)
- **PostgreSQL 14+**: Download from [postgresql.org](https://postgresql.org)
- **Git**: Download from [git-scm.com](https://git-scm.com)

### Optional but Recommended

- **Virtual Environment**: `pip install virtualenv`
- **GitHub CLI**: For repository management
- **Docker**: For containerized deployment

### System Requirements

- **RAM**: Minimum 8GB, Recommended 16GB
- **Storage**: 5GB free space
- **OS**: Windows 10+, macOS 10.15+, Ubuntu 18.04+

## Project Structure

```
PoultryAI/
├── backend/                 # Django REST API
│   ├── apps/               # Django applications
│   ├── manage.py           # Django management script
│   ├── requirements.txt    # Python dependencies
│   └── settings.py         # Django settings
├── frontend/               # React application
│   ├── src/                # Source code
│   ├── package.json        # Node dependencies
│   └── vite.config.js      # Vite configuration
├── model/                  # ML model directory
├── screenshots/            # Application screenshots
├── LICENSE                 # MIT License
├── README.md              # Project documentation
└── SETUP_GUIDE.md         # This file
```

## Backend Setup

### 1. Navigate to Backend Directory

```bash
cd backend
```

### 2. Create Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Environment Configuration

Create a `.env` file in the `backend` directory:

```env
# Django Settings
DJANGO_SECRET_KEY=your-super-secret-key-here-change-this-in-production
DJANGO_DEBUG=True
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1

# Database
DATABASE_URL=postgres://username:password@localhost:5432/poultryai

# Email (optional)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password

# API Keys
GOOGLE_MAPS_API_KEY=your-google-maps-api-key

# Model Directory
MODEL_DIR=../model
```

### 5. Database Setup

#### Using PostgreSQL

1. Create database:
```sql
CREATE DATABASE poultryai;
CREATE USER poultryai_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE poultryai TO poultryai_user;
```

2. Update `DATABASE_URL` in `.env`

#### Using SQLite (Development)

No additional setup required. SQLite will be used automatically.

### 6. Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 7. Create Superuser

```bash
python manage.py createsuperuser
```

Follow the prompts to create an admin user.

### 8. Load Initial Data (Optional)

```bash
# Load diseases
python manage.py seed_diseases

# Load medicines
python manage.py seed_medicines
```

## Frontend Setup

### 1. Navigate to Frontend Directory

```bash
cd frontend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Create a `.env` file in the `frontend` directory:

```env
VITE_API_URL=http://localhost:8000/api
VITE_GOOGLE_MAPS_API_KEY=your-google-maps-api-key
```

## Running the Application

### Development Mode

1. **Start Backend**:
```bash
cd backend
source venv/bin/activate  # or venv\Scripts\activate on Windows
python manage.py runserver
```

2. **Start Frontend** (in a new terminal):
```bash
cd frontend
npm run dev
```

3. **Access Application**:
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:8000
   - Admin Panel: http://localhost:8000/admin

### Production Mode

1. **Build Frontend**:
```bash
cd frontend
npm run build
```

2. **Collect Static Files**:
```bash
cd backend
python manage.py collectstatic --noinput
```

3. **Run Production Server**:
```bash
python manage.py runserver --settings=backend.settings.production
```

## Testing

### Backend Tests

```bash
cd backend
python manage.py test
```

### Frontend Tests

```bash
cd frontend
npm run test
```

### End-to-End Testing

```bash
# Install Playwright
npm install -D @playwright/test

# Run E2E tests
npx playwright test
```

## Deployment

### Using Docker

1. **Build Images**:
```bash
docker-compose build
```

2. **Run Containers**:
```bash
docker-compose up -d
```

### Manual Deployment

1. **Configure Production Settings**:
   - Set `DJANGO_DEBUG=False`
   - Configure production database
   - Set up static file serving
   - Configure HTTPS

2. **Use Production Server**:
   - Gunicorn for Django
   - Nginx for static files and reverse proxy

## Troubleshooting

### Common Issues

1. **Port Already in Use**:
   
```bash
   # Find process using port
   lsof -i :8000
   # Kill process
   kill -9 <PID>
   
```

2. **Database Connection Error**:
   - Verify PostgreSQL is running
   - Check database credentials
   - Ensure database exists

3. **Module Not Found**:
   
```bash
   # Reinstall dependencies
   pip install -r requirements.txt --force-reinstall
   
```

4. **CORS Errors**:
   - Add frontend URL to `CORS_ALLOWED_ORIGINS`
   - Restart Django server

5. **Build Errors**:
   
```bash
   # Clear npm cache
   npm cache clean --force
   # Reinstall
   rm -rf node_modules package-lock.json
   npm install
   
```

### Getting Help

- Check the [README.md](README.md) for detailed documentation
- Review Django and React documentation
- Check GitHub Issues for known problems

## Next Steps

1. Explore the admin panel
2. Upload test images
3. Configure email settings
4. Set up monitoring and logging
5. Implement backup strategies

---

*For additional support, please refer to the main [README.md](README.md) or open an issue on GitHub.*
