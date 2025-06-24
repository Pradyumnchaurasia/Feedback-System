# Feedback-System
A simple, secure, and user-friendly feedback sharing tool for managers and team members, built with modern web technologies.
🚀 Features
Core MVP Features

Authentication & Roles: Manager and Employee roles with role-based access control
Feedback Submission: Managers can submit structured feedback (strengths, improvements, sentiment)
Feedback Visibility: Employees see only their feedback, managers see their team's data
Dashboard: Team overview for managers, personal timeline for employees
Acknowledgment System: Employees can mark feedback as read

Tech Stack
Backend:

Python FastAPI - Modern, fast web framework for building APIs
SQLite - Lightweight database for development (easily upgradeable to PostgreSQL)
SQLAlchemy - Python SQL toolkit and ORM
Pydantic - Data validation using Python type annotations
JWT Authentication - Secure token-based authentication
bcrypt - Password hashing

Frontend:

React 18 - Modern UI library
Tailwind CSS - Utility-first CSS framework
Vite - Fast build tool and dev server
Lucide React - Beautiful icon library

DevOps:

Docker - Containerization for easy deployment
Docker Compose - Multi-container orchestration

🏗️ Architecture & Design Decisions
Backend Architecture

FastAPI chosen for its automatic OpenAPI documentation, type safety, and performance
SQLAlchemy ORM for database abstraction and easy migrations
JWT tokens for stateless authentication
Role-based middleware for endpoint protection
Pydantic models for request/response validation

Database Design
sqlUsers Table:
- id (Primary Key)
- email (Unique)
- name
- password_hash
- role (manager/employee)
- manager_id (Foreign Key, nullable)

Feedback Table:
- id (Primary Key)
- manager_id (Foreign Key)
- employee_id (Foreign Key)
- strengths (Text)
- improvements (Text)
- sentiment (positive/neutral/negative)
- created_at (Timestamp)
- acknowledged (Boolean)
Security Considerations

Password hashing with bcrypt
JWT token expiration
Role-based access control
Input validation and sanitization
CORS configuration

📦 Setup Instructions
Prerequisites

Python 3.9+
Node.js 16+
Docker (optional)

Option 1: Local Development
Backend Setup
bash# Clone the repository
git clone https://github.com/yourusername/feedback-system.git
cd feedback-system

# Set up Python virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install Python dependencies
pip install -r requirements.txt

# Initialize the database
python -c "
from app.database import engine
from app.models import Base
Base.metadata.create_all(bind=engine)
"

# Start the backend server
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
Frontend Setup
bash# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
The application will be available at:

Frontend: http://localhost:5173
Backend API: http://localhost:8000
API Documentation: http://localhost:8000/docs

Option 2: Docker Setup
bash# Clone the repository
git clone https://github.com/yourusername/feedback-system.git
cd feedback-system

# Build and run with Docker Compose
docker-compose up --build

# Or run just the backend
docker build -t feedback-backend .
docker run -p 8000:8000 feedback-backend
Default Users
The system comes with sample users for testing:
Manager Account:

Email: john@company.com
Password: password123

Employee Account:

Email: alice@company.com
Password: password123

🗂️ Project Structure
feedback-system/
├── app/                          # Backend application
│   ├── __init__.py
│   ├── main.py                   # FastAPI application entry point
│   ├── database.py               # Database configuration
│   ├── models.py                 # SQLAlchemy models
│   ├── schemas.py                # Pydantic schemas
│   ├── crud.py                   # Database operations
│   ├── auth.py                   # Authentication utilities
│   ├── dependencies.py           # FastAPI dependencies
│   └── routers/                  # API route handlers
│       ├── __init__.py
│       ├── auth.py
│       ├── users.py
│       └── feedback.py
├── frontend/                     # React frontend
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.js
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Backend Docker configuration
├── docker-compose.yml            # Multi-container setup
├── .env.example                  # Environment variables template
├── .gitignore
└── README.md
🧪 Testing
Backend Tests
bash# Install test dependencies
pip install pytest pytest-asyncio httpx

# Run tests
pytest
Frontend Tests
bashcd frontend
npm run test
🚀 Deployment
Environment Variables
Create a .env file in the root directory:
env# Database
DATABASE_URL=sqlite:///./feedback.db

# JWT
SECRET_KEY=your-secret-key-here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# CORS
ALLOWED_ORIGINS=http://localhost:5173,https://yourdomain.com
Production Deployment

Database: Upgrade to PostgreSQL for production
Security: Use strong SECRET_KEY and enable HTTPS
Scaling: Consider using Gunicorn with multiple workers
Monitoring: Add logging and health checks

Docker Production
bash# Build production image
docker build -t feedback-system:latest .

# Run with production environment
docker run -p 8000:8000 --env-file .env feedback-system:latest
🔧 API Documentation
The backend automatically generates interactive API documentation:

Swagger UI: http://localhost:8000/docs
ReDoc: http://localhost:8000/redoc

Key Endpoints

POST /auth/login - User authentication
GET /users/me - Get current user info
GET /users/team - Get team members (managers only)
POST /feedback - Create feedback (managers only)
GET /feedback - Get feedback (role-based filtering)
PUT /feedback/{id}/acknowledge - Acknowledge feedback

🤝 Contributing

Fork the repository
Create a feature branch (git checkout -b feature/amazing-feature)
Commit your changes (git commit -m 'Add amazing feature')
Push to the branch (git push origin feature/amazing-feature)
Open a Pull Request

📝 Future Enhancements

 Email notifications
 PDF export functionality
 Anonymous peer feedback
 Feedback templates
 Analytics dashboard
 Mobile app
 Multi-language support

 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.


🆘 Support
If you encounter any issues or have questions:

Check the Issues page
Create a new issue with detailed information
Join our discussions in the Discussions tab
