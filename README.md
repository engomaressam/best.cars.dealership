# Best Cars Dealership - Full-Stack Review Platform

![Django](https://img.shields.io/badge/Django-5.2.7-green)
![React](https://img.shields.io/badge/React-18.2.0-blue)
![MongoDB](https://img.shields.io/badge/MongoDB-Latest-green)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

A comprehensive full-stack web application that enables customers to browse car dealerships across the United States and submit reviews for their experiences. Built with modern technologies and microservices architecture.

## 🚀 Running it

The app isn't hosted permanently: for the course it ran on IBM Cloud Code Engine and Kubernetes (`server/deployment.yaml`) in temporary lab environments. The screenshots below show it running, and [Getting Started](#-getting-started) runs the whole stack locally.

## 📸 Screenshots

<table>
  <tr>
    <td><img src="screenshots/homepage.png" alt="Homepage" width="400"/></td>
    <td><img src="screenshots/dealers.png" alt="Dealers List" width="400"/></td>
  </tr>
  <tr>
    <td><img src="screenshots/dealer-reviews.png" alt="Dealer Reviews" width="400"/></td>
    <td><img src="screenshots/post-review.png" alt="Post Review" width="400"/></td>
  </tr>
</table>

## 🎯 Project Overview

Best Cars Dealership is a national car dealership with local branches across the United States. This platform allows customers to:

- 🔍 Browse dealerships by location and state
- ⭐ Read reviews from other customers
- ✍️ Submit their own reviews (authenticated users)
- 🚗 View car inventory by make and model
- 😊 See sentiment analysis of reviews (positive, negative, neutral)

## ✨ Key Features

### User Management
- ✅ User registration and authentication
- ✅ Session management with Django authentication system
- ✅ Secure login/logout functionality
- ✅ Role-based access control (anonymous vs. authenticated users)

### Dealership Management
- ✅ View all dealerships nationwide
- ✅ Filter dealerships by state
- ✅ View detailed information for each dealership
- ✅ Dynamic dealer data from MongoDB

### Review System
- ✅ Browse reviews for any dealership
- ✅ Submit reviews (authenticated users only)
- ✅ Include purchase details (car make, model, year)
- ✅ Automated sentiment analysis on all reviews
- ✅ Real-time review updates

### Car Inventory
- ✅ Database of car makes and models
- ✅ Dynamic dropdowns for review submission
- ✅ Admin interface for inventory management

### Sentiment Analysis
- ✅ Microservice for analyzing review sentiment
- ✅ Visual indicators (positive/negative/neutral)
- ✅ Deployed as independent service

## 🛠️ Technology Stack

### Frontend
- **React 18** - Modern UI library
- **Bootstrap 5** - Responsive design framework
- **JavaScript ES6+** - Modern JavaScript features
- **React Router** - Client-side routing

### Backend
- **Django 5.2.7** - Python web framework
- **Django REST Framework** - API development
- **SQLite** - Local database for car inventory
- **Python 3.13** - Programming language

### Database & Microservices
- **MongoDB** - NoSQL database for dealers and reviews
- **Express.js** - Node.js API framework
- **Mongoose** - MongoDB ODM

### Deployment & DevOps
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **IBM Code Engine** - Serverless deployment (sentiment analyzer)

### Additional Technologies
- **NLTK** - Natural Language Processing for sentiment analysis
- **Requests** - HTTP library for API calls
- **dotenv** - Environment variable management

## 📋 Architecture

```
┌─────────────────┐
│   React Frontend│
│   (Port 8000)   │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│  Django Backend │
│  (Port 8000)    │
│  - Views        │
│  - Models       │
│  - Proxy APIs   │
└────────┬────────┘
         │
    ┌────┴────┐
    ↓         ↓
┌─────────┐ ┌──────────────────┐
│ SQLite  │ │ Express + MongoDB│
│ (Cars)  │ │   (Port 3030)    │
│         │ │ - Dealers        │
│         │ │ - Reviews        │
└─────────┘ └──────────────────┘
                   │
                   ↓
         ┌──────────────────┐
         │ Sentiment Analyzer│
         │   (Code Engine)   │
         └──────────────────┘
```

## 🚀 Getting Started

### Prerequisites
- Python 3.13+
- Node.js 18+
- Docker Desktop
- MongoDB (via Docker)
- Git

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/engomaressam/best.cars.dealership.git
cd best.cars.dealership
```

2. **Set up Python virtual environment**
```bash
cd server
pip install virtualenv
virtualenv djangoenv

# Windows
.\djangoenv\Scripts\activate

# Linux/Mac
source djangoenv/bin/activate
```

3. **Install Python dependencies**
```bash
pip install -r requirements.txt
```

4. **Configure environment variables**
```bash
cd djangoapp
cp .env.example .env
# Edit .env and set:
# backend_url=http://localhost:3030
# sentiment_analyzer_url=http://localhost:5050/
```

5. **Run Django migrations**
```bash
python manage.py makemigrations
python manage.py migrate
```

6. **Create superuser**
```bash
python manage.py createsuperuser
# Username: admin
# Email: admin@bestcars.com
# Password: admin123
```

7. **Build React frontend**
```bash
cd ../frontend
npm install
npm run build
```

8. **Start MongoDB and Express API**
```bash
cd ../database
docker build . -t nodeapp
docker-compose up
```

9. **Start Django server** (in new terminal)
```bash
cd server
.\djangoenv\Scripts\activate  # or source djangoenv/bin/activate
python manage.py runserver
```

10. **Access the application**
- Frontend: http://localhost:8000
- Admin Panel: http://localhost:8000/admin
- Backend API: http://localhost:3030

## 📚 API Endpoints

### Django Endpoints (`/djangoapp/`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/login` | User login | No |
| POST | `/register` | User registration | No |
| GET | `/logout` | User logout | Yes |
| GET | `/get_cars/` | Get car makes and models | No |
| GET | `/get_dealers/` | Get all dealerships | No |
| GET | `/get_dealers/<state>` | Get dealers by state | No |
| GET | `/dealer/<id>` | Get dealer details | No |
| GET | `/reviews/dealer/<id>` | Get dealer reviews | No |
| POST | `/add_review` | Submit a review | Yes |

### Express API Endpoints (`http://localhost:3030`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/fetchDealers` | Get all dealerships |
| GET | `/fetchDealers/:state` | Get dealerships by state |
| GET | `/fetchDealer/:id` | Get dealer by ID |
| GET | `/fetchReviews` | Get all reviews |
| GET | `/fetchReviews/dealer/:id` | Get reviews for dealer |
| POST | `/insert_review` | Insert new review |

## 🎨 Features Walkthrough

### 1. Browse Dealerships
Navigate to `/dealers` to see all dealerships in a table format. Use the state dropdown to filter by location.

### 2. View Reviews
Click "View Reviews" on any dealer to see customer reviews with sentiment indicators:
- 🟢 **Positive** - Great experience
- 🔴 **Negative** - Poor experience
- ⚪ **Neutral** - Mixed or neutral feedback

### 3. Submit a Review
1. Log in or register an account
2. Navigate to a dealer's page
3. Click "Post Review"
4. Fill out the form:
   - Write your review
   - Indicate if you purchased a car
   - Select car make, model, and year (if purchased)
   - Choose purchase date
5. Submit - your review appears instantly with sentiment analysis

### 4. Admin Panel
Access `/admin` to manage:
- Users
- Car makes and models
- View all data

## 🧪 Testing

### Run Django Tests
```bash
python manage.py test
```

### Test API Endpoints
```bash
# Test dealers endpoint
curl http://localhost:3030/fetchDealers

# Test Django proxy
curl http://localhost:8000/djangoapp/get_dealers/

# Test specific dealer
curl http://localhost:8000/djangoapp/dealer/15
```

## 📦 Docker Deployment

The application uses Docker for containerization:

```bash
# Build and run MongoDB + Express API
cd server/database
docker-compose up -d

# View logs
docker-compose logs -f

# Stop containers
docker-compose down
```

## 🔧 Configuration

### Environment Variables

**server/djangoapp/.env:**
```env
backend_url=http://localhost:3030
sentiment_analyzer_url=http://localhost:5050/
```

**server/djangoproj/settings.py:**
```python
ALLOWED_HOSTS = ['localhost', '127.0.0.1']
CSRF_TRUSTED_ORIGINS = ['http://localhost:8000', 'http://127.0.0.1:8000']
```

## 📈 Future Enhancements

- [ ] Deploy to cloud platform (AWS/Azure/Heroku)
- [ ] Add car inventory search functionality
- [ ] Implement review editing and deletion
- [ ] Add dealer ratings and statistics
- [ ] Create mobile-responsive design improvements
- [ ] Add image upload for reviews
- [ ] Implement real-time notifications
- [ ] Add advanced search and filters
- [ ] Create dealer dashboard
- [ ] Implement email notifications

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Omar Essam**
- GitHub: [@engomaressam](https://github.com/engomaressam)
- Email: omaressamrme@gmail.com
- LinkedIn: [Your LinkedIn Profile](#)

## 🙏 Acknowledgments

- IBM Full-Stack Developer Capstone Project
- Django Software Foundation
- React Team
- MongoDB Team
- Bootstrap Team
- All contributors and reviewers

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Contact: omaressamrme@gmail.com

---

⭐ Star this repository if you found it helpful!

**Built with ❤️ by Omar Essam**
