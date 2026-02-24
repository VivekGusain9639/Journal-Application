# 📔 Journal Application

A feature-rich, secure journal application built with **Spring Boot** that allows users to create, manage, and analyze their journal entries with sentiment analysis, weather integration, and advanced caching mechanisms.

## 🌟 Features

### Core Functionality
- ✍️ **Create & Manage Journal Entries** - Write, update, and delete personal journal entries
- 🔐 **Secure Authentication** - JWT-based authentication with Spring Security
- 👤 **User Management** - User registration, login, and profile management
- 🌐 **OAuth2 Integration** - Google OAuth2 authentication support
- 🎯 **Role-Based Access Control** - Admin and User roles with different permissions

### Advanced Features
- 📊 **Sentiment Analysis** - Analyze mood and sentiment of journal entries using Kafka
- 🌤️ **Weather Integration** - Fetch and display weather data alongside journal entries
- ⚡ **Redis Caching** - High-performance caching layer for improved response times
- 📧 **Email Notifications** - Automated email services for user updates
- 📈 **Scheduled Tasks** - Background jobs for data processing and cleanup
- 📚 **API Documentation** - Interactive Swagger UI for API exploration

### Testing & Quality
- 🧪 **Comprehensive Test Suite** - Unit tests for services, repositories, and schedulers
- 🔍 **Code Quality Monitoring** - SonarCloud integration for code quality analysis

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Framework** | Spring Boot 2.7.16 |
| **Language** | Java 8 |
| **Database** | MongoDB |
| **Cache** | Redis |
| **Message Queue** | Apache Kafka |
| **Authentication** | JWT, Spring Security, OAuth2 |
| **API Documentation** | Springdoc OpenAPI (Swagger 3) |
| **Build Tool** | Maven |
| **Email Service** | Gmail SMTP |
| **Testing** | JUnit 5 |
| **Utilities** | Lombok |

## 📋 Prerequisites

Before running the application, ensure you have the following installed:

- **Java 8** or higher
- **Maven 3.6+**
- **MongoDB** (local or cloud instance)
- **Redis** (for caching)
- **Apache Kafka** (for sentiment analysis)
- **Git**

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/VivekGusain9639/Journal-Application.git
cd Journal-Application
```

### 2. Configure Environment Variables

Create a `.env` file or configure the following environment variables:

```bash
# Database Configuration
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/?retryWrites=true&w=majority

# Redis Configuration
REDIS_HOST=localhost
REDIS_PASSWORD=your_redis_password

# Email Configuration
JAVA_EMAIL=your_email@gmail.com
JAVA_EMAIL_PASSWORD=your_app_password

# Weather API
WEATHER_API_KEY=your_weather_api_key

# Google OAuth2
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# Kafka Configuration
KAFKA_SERVERS=localhost:9092

# Server Configuration
SERVER_PORT=8080
```

### 3. Build the Project

```bash
mvn clean install
```

### 4. Run the Application

```bash
# Using Maven
mvn spring-boot:run

# Or using Java
java -jar target/journalApp-0.0.1-SNAPSHOT.jar
```

The application will start on `http://localhost:8080/journal`

## 📖 API Documentation

Once the application is running, access the interactive API documentation at:

```
http://localhost:8080/journal/swagger-ui.html
```

### Main API Endpoints

#### Journal Entries
- `GET /journal` - Get all journal entries of authenticated user
- `POST /journal` - Create a new journal entry
- `PUT /journal/{id}` - Update a journal entry
- `DELETE /journal/{id}` - Delete a journal entry

#### User Management
- `POST /public/signup` - Register a new user
- `POST /public/login` - Authenticate user
- `GET /user` - Get user profile
- `PUT /user` - Update user information

#### Admin Operations
- `GET /admin/users` - Get all users (Admin only)
- `POST /admin/create-admin-user` - Create admin user

#### Public Endpoints
- `GET /public/health` - Health check
- `GET /public/weather` - Get weather information

## 🏗️ Project Structure

```
src/
├── main/
│   ├── java/net/engineeringdigest/journalApp/
│   │   ├── JournalApplication.java          # Main Spring Boot application
│   │   ├── api/                             # API response models
│   │   ├── cache/                           # Caching configuration
│   │   ├── config/                          # Spring configurations
│   │   ├── controller/                      # REST controllers
│   │   ├── dto/                             # Data Transfer Objects
│   │   ├── entity/                          # MongoDB entities
│   │   ├── enums/                           # Enumeration classes
│   │   ├── filter/                          # JWT filter
│   │   ├── model/                           # Model classes
│   │   ├── repository/                      # Data access layer
│   │   ├── scheduler/                       # Scheduled tasks
│   │   ├── service/                         # Business logic
│   │   └── utilis/                          # Utility classes
│   └── resources/
│       ├── application.yml                  # Application configuration
│       └── logback.xml                      # Logging configuration
└── test/
    └── java/net/engineeringdigest/journalApp/
        ├── JournalAppApplicationTests.java
        ├── cron/                            # Scheduler tests
        ├── repository/                      # Repository tests
        └── service/                         # Service tests
```

## 🔑 Key Components

### Authentication & Security
- **JwtFilter** - Intercepts requests and validates JWT tokens
- **SpringSecurity** - Configures security policies and access control
- **UserDetailsServiceImpl** - Custom user details service

### Services
- **UserService** - User registration, authentication, and management
- **JournalEntryService** - CRUD operations for journal entries
- **SentimentConsumerService** - Processes sentiment analysis via Kafka
- **WeatherService** - Fetches weather data from external API
- **EmailService** - Sends email notifications
- **RedisService** - Manages caching operations

### Configuration
- **RedisConfig** - Redis connection and template configuration
- **SwaggerConfig** - OpenAPI/Swagger documentation setup
- **SpringSecurity** - Security filter chains and CORS configuration

## 🧪 Running Tests

Execute the test suite using Maven:

```bash
# Run all tests
mvn test

# Run specific test class
mvn test -Dtest=UserServiceTests

# Run tests with coverage
mvn clean test jacoco:report
```

### Test Coverage
- **UserServiceTests** - User service functionality
- **UserDetailsServiceImplTests** - Authentication service
- **EmailServiceTests** - Email sending functionality
- **RedisTests** - Caching operations
- **UserRepositoryImplTests** - Custom repository logic
- **UserSchedulersTest** - Scheduled task execution

## 📊 Database Schema

### Collections

#### User
```json
{
  "_id": ObjectId,
  "userName": String,
  "password": String,
  "email": String,
  "roles": [String],
  "journalEntries": [ObjectId],
  "createdDate": Date
}
```

#### JournalEntry
```json
{
  "_id": ObjectId,
  "title": String,
  "content": String,
  "date": Date,
  "sentiment": Enum,
  "user": ObjectId,
  "weather": Object
}
```

## 🔄 Data Flow

```
User Request
    ↓
JWT Filter (Authentication)
    ↓
Spring Security (Authorization)
    ↓
Controller (Request Handling)
    ↓
Service Layer (Business Logic)
    ↓
Redis Cache (Check)
    ↓
Repository (Database Query)
    ↓
MongoDB (Data Retrieval)
    ↓
Kafka Producer (Event Publishing)
    ↓
Sentiment Analysis Consumer
    ↓
Response to Client
```

## 🚀 Deployment

### Docker Deployment

Create a `Dockerfile`:

```dockerfile
FROM openjdk:8-jre-slim
COPY target/journalApp-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

Build and run:

```bash
docker build -t journal-app .
docker run -p 8080:8080 journal-app
```

## 📝 Logging

Logging is configured via `logback.xml` in the resources folder. Log levels can be adjusted for different packages:

```yaml
Levels: TRACE, DEBUG, INFO, WARN, ERROR
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

**Vivek Gusain**
- GitHub: [@VivekGusain9639](https://github.com/VivekGusain9639)

## 📞 Support & Contact

For issues, feature requests, or questions:
- Open an issue on GitHub
- Contact via email in the repository

## 🎯 Roadmap

- [ ] Mobile application
- [ ] Advanced sentiment analysis with ML models
- [ ] Collaborative journaling features
- [ ] Data export functionality (PDF, CSV)
- [ ] Dark mode UI
- [ ] Multi-language support

---

**Happy Journaling! ✨**
