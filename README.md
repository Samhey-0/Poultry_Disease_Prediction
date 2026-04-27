![FutureEnhancement](screenshots/AI_Powered_poultry_disease_Detection.png)
# PoultryAI - Poultry Disease Prediction System

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Django](https://img.shields.io/badge/Django-4.2+-green.svg)
![React](https://img.shields.io/badge/React-18.2+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## Project Overview

**PoultryAI** is a comprehensive Full-Stack poultry disease prediction system developed as a Final Year Project (FYP). The application leverages machine learning to identify diseases in poultry from uploaded images and provides treatment recommendations including medicines, dosages, and administration guidelines.

### Key Features

-  **AI-Powered Disease Detection** - Upload poultry images and get instant disease predictions
-  **Medicine Recommendations** - Get detailed treatment plans with dosages
-  **Vet Locator** - Find nearest veterinary services using Google Maps integration
-  **Admin Dashboard** - Comprehensive management for diseases, medicines, inventory, and users
-  **Analytics & Reports** - Track disease trends and generate PDF reports
-  **Responsive Design** - Works seamlessly on desktop and mobile devices

---

## Screenshots

> **Note**: Replace these placeholder images with actual screenshots of your application.

### Landing Page
![Landing Page](screenshots/Home_page.png)

### Login Page
[Login Page](screenshots/Login.png)

### Signup
[Signup](screenshots/Signup.png)

### OTP Send
[OTP Send](screenshots/OTP.png)

### Disease Prediction
![Disease Prediction](screenshots/Screenshot2026-02-27103802.png)

### Admin Dashboard
![Admin Dashboard](screenshots/Screenshot2026-02-27103722.png)

### Results Page
![Results](screenshots/Disease_Analysis.png)

### Nearby Vet hospital
[Nearby hospitals](screenshots/Nearby_vet_Map.png)


---

## Technology Stack

### Backend
| Technology | Purpose |
|------------|---------|
| Django 4.2+ | Web Framework |
| Django REST Framework | API Development |
| PostgreSQL | Database |
| PyTorch | Machine Learning |
| Celery | Background Tasks |
| Redis | Message Broker |

### Frontend
| Technology | Purpose |
|------------|---------|
| React 18 | UI Framework |
| Vite | Build Tool |
| Tailwind CSS | Styling |
| React Router | Navigation |
| Axios | HTTP Client |
| Recharts | Data Visualization |

---

## Project Structure

```
PoultryAI/
├── backend/                 # Django Backend
│   ├── apps/               # Django Applications
│   │   ├── analysis/       # Disease Analysis Module
│   │   ├── diseases/       # Disease Management
│   │   ├── medicines/      # Medicine Database
│   │   ├── vets/          # Veterinary Services
│   │   ├── inventory/     # Inventory Management
│   │   ├── reports/       # Report Generation
│   │   └── users/         # User Authentication
│   ├── backend/           # Django Project Settings
│   ├── model_loader.py    # ML Model Integration
│   └── requirements.txt  # Python Dependencies
│
├── frontend/              # React Frontend
│   ├── src/
│   │   ├── components/   # Reusable Components
│   │   ├── pages/        # Application Pages
│   │   ├── services/     # API Services
│   │   └── context/      # React Context
│   └── package.json      # Node Dependencies
│
├── model/                 # ML Model Directory
│   ├── model.pth         # Trained PyTorch Model
│   └── README.md         # Model Integration Guide
│
├── LICENSE               # MIT License
└── README.md             # This File
```

---

## 🚀 Getting Started

### Prerequisites

Before running the project, ensure you have the following installed:

- **Python** 3.10 or higher
- **Node.js** 18 or higher
- **PostgreSQL** 14 or higher (optional, SQLite for development)
- **Git**

### Clone the Repository

```
bash
git clone https://github.com/yourusername/poultry-disease-prediction.git
cd poultry-disease-prediction
```

---

### Backend Setup

1. **Create Virtual Environment**

```
bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts activate
# On Mac/Linux:
source venv/bin/activate
```

2. **Install Dependencies**

```
bash
pip install -r requirements.txt
```

3. **Environment Configuration**

Create a `.env` file in the `backend` directory:

```
env
# Django Settings
DJANGO_SECRET_KEY=your-secret-key-here
DJANGO_DEBUG=True
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1

# Database (using SQLite for development)
DATABASE_URL=sqlite:///db.sqlite3

# For PostgreSQL, use:
# DATABASE_URL=postgres://username:password@localhost:5432/poultryai

# Frontend URL for CORS
CORS_ALLOWED_ORIGINS=http://localhost:5173,http://127.0.0.1:5173

# JWT Settings
SIMPLE_JWT_ACCESS_TOKEN_LIFETIME_MIN=15
SIMPLE_JWT_REFRESH_TOKEN_LIFETIME_DAYS=7

# Model Directory
MODEL_DIR=../model

# Google Maps API (optional)
GOOGLE_MAPS_API_KEY=your-google-maps-api-key

# Email Configuration (for development - uses console backend)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
```

4. **Run Migrations**

```
bash
python manage.py makemigrations
python manage.py migrate
```

5. **Seed Initial Data (Optional)**

```
bash
# Seed diseases and medicines
python manage.py seed_diseases
python manage.py seed_medicines
```

6. **Create Superuser**

```
bash
python manage.py createsuperuser
```

7. **Run Development Server**

```
bash
python manage.py runserver
```

The backend will be available at `http://localhost:8000`

---

### Frontend Setup

1. **Navigate to Frontend Directory**

```
bash
cd frontend
```

2. **Install Dependencies**

```
bash
npm install
```

3. **Environment Configuration**

Create a `.env` file in the `frontend` directory:

```
env
VITE_API_URL=http://localhost:8000/api
VITE_GOOGLE_MAPS_API_KEY=your-google-maps-api-key
```

4. **Run Development Server**

```
bash
npm run dev
```

The frontend will be available at `http://localhost:5173`

---

## Running with Docker (Optional)

### Using Docker Compose

```
bash
# Build and run all services
docker-compose up -d

# View logs
docker-compose logs -f
```

---

## Application Usage

### For Users

1. **Register/Login** - Create an account or login with existing credentials
2. **Upload Image** - Take or upload a photo of the affected poultry
3. **Get Results** - View disease predictions and treatment recommendations
4. **Find Vets** - Locate nearby veterinary services on the map

### For Administrators

1. **Access Admin Panel** - Navigate to `/admin`
2. **Manage Diseases** - Add, edit, or remove disease entries
3. **Manage Medicines** - Maintain medicine database with dosages
4. **Manage Users** - View and manage user accounts
5. **View Analytics** - Check disease trends and system usage

---

## API Endpoints

### Authentication
- `POST /api/auth/register/` - User registration
- `POST /api/auth/login/` - User login
- `POST /api/auth/refresh/` - Refresh JWT token
- `POST /api/auth/logout/` - User logout

### Analysis
- `GET /api/analysis/` - List all analyses
- `POST /api/analysis/` - Create new analysis
- `GET /api/analysis/{id}/` - Get analysis details
- `GET /api/analysis/history/` - User's analysis history

### Diseases
- `GET /api/diseases/` - List all diseases
- `GET /api/diseases/{id}/` - Get disease details

### Medicines
- `GET /api/medicines/` - List all medicines
- `GET /api/medicines/{id}/` - Get medicine details

### Vets
- `GET /api/vets/` - List all veterinary services
- `GET /api/vets/nearest/` - Find nearest vets

### Inventory
- `GET /api/inventory/` - List inventory items
- `POST /api/inventory/` - Add inventory item

### Reports
- `GET /api/reports/` - List reports
- `POST /api/reports/` - Generate new report
- `GET /api/reports/{id}/download/` - Download report PDF

For full API documentation, visit `/api/schema/` when the server is running.

---

## Machine Learning Model

This project uses a PyTorch-based deep learning model for poultry disease classification. The model is located in the `model/` directory.

### Supported Diseases
- Coccidiosis
- Salmonellosis
- Newcastle Disease
- Avian Influenza
- Marek's Disease
- And more...

### Model Integration

Place your trained model file (`model.pth`, `model.h5`, or `model.onnx`) in the `model/` directory and update the `MODEL_DIR` in your `.env` file.

For detailed model integration instructions, see [model/README.md](model/README.md)

---

## Troubleshooting

### Common Issues

1. **ModuleNotFoundError: No module named 'django'**
   - Solution: Activate virtual environment and run `pip install -r requirements.txt`

2. **CORS Errors**
   - Solution: Add your frontend URL to `CORS_ALLOWED_ORIGINS` in `.env`

3. **Database Connection Errors**
   - Solution: Verify `DATABASE_URL` in `.env` is correct

4. **Model Not Found**
   - Solution: Ensure model file is in the `model/` directory and `MODEL_DIR` is set correctly

5. **Port Already in Use**
   - Solution: Use a different port with `python manage.py runserver 8001`

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
Copyright (c) 2025 Saim Bakhtiar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## Author

**Saim Bakhtiar**
- Final Year Project 
- GitHub: (https://github.com/Samhey-0)

---

## Acknowledgments

- Open-source community
- Contributors and testers

---

## Support

For issues and feature requests, please open an issue on GitHub.

---

*Last Updated: January 2025*
