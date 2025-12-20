# 🏦 Smart Bank Management System

A comprehensive banking application built with Spring Boot, featuring account management, fund transfers, loan processing, and admin operations.

## 🚀 Features

### Customer Features
- ✅ User registration with email OTP verification
- ✅ Secure login with JWT authentication
- ✅ Create multiple accounts (Savings, Current, Fixed Deposit)
- ✅ Fund transfer between accounts
- ✅ Transaction history and statements
- ✅ Loan application with EMI calculation
- ✅ Loan tracking and status updates

### Admin Features
- ✅ View all pending loan applications
- ✅ Approve or reject loan applications
- ✅ Filter loans by status
- ✅ Mark loans as under review
- ✅ View all customer accounts and transactions

### Technical Features
- ✅ RESTful API design
- ✅ JWT-based stateless authentication
- ✅ Role-based access control (CUSTOMER, ADMIN)
- ✅ Input validation with Bean Validation
- ✅ Global exception handling
- ✅ Transaction management with @Transactional
- ✅ Async email notifications
- ✅ Comprehensive logging with SLF4J
- ✅ Production-ready configuration

## 🛠️ Tech Stack

- **Backend:** Spring Boot 3.x
- **Security:** Spring Security + JWT
- **Database:** MySQL
- **ORM:** Spring Data JPA (Hibernate)
- **Validation:** Jakarta Bean Validation
- **Email:** Spring Mail + SMTP
- **Build Tool:** Maven
- **Testing:** JUnit 5, Mockito

## 📋 Prerequisites

- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+
- Postman (for API testing)

## 🚀 Getting Started

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/smart-bank.git
cd smart-bank
```

### 2. Configure Database

Create MySQL database:
```sql
CREATE DATABASE smart_bank;
```

Update `src/main/resources/application.yml`:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/smart_bank
    username: your_username
    password: your_password
```

### 3. Configure Email (Optional)

Update `application.yml` with your SMTP settings:
```yaml
spring:
  mail:
    host: smtp.gmail.com
    port: 587
    username: your-email@gmail.com
    password: your-app-password
```

For Gmail, enable 2FA and create an App Password.

### 4. Run Application
```bash
mvn spring-boot:run
```

Application will start on `http://localhost:8080`

### 5. Default Admin User

On first startup, an admin user is created automatically:
- **Email:** admin@bank.com
- **Password:** Admin@123

## 📚 API Documentation

### Base URL
```
http://localhost:8080/api
```

### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/auth/register` | Register new user | No |
| POST | `/auth/verify-otp` | Verify OTP | No |
| POST | `/auth/login` | Login user | No |
| POST | `/auth/resend-otp` | Resend OTP | No |

### Account Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/accounts` | Create new account | Yes |
| GET | `/accounts` | Get user's accounts | Yes |
| GET | `/accounts/{accountNumber}` | Get account details | Yes |

### Transfer Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/transfer` | Transfer funds | Yes |

### Transaction Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/transactions/{accountNumber}` | Get transactions | Yes |
| GET | `/transactions/{accountNumber}/recent` | Get recent transactions | Yes |

### Loan Endpoints (Customer)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/loans` | Apply for loan | Yes |
| GET | `/loans` | Get user's loans | Yes |
| GET | `/loans/{loanId}` | Get loan details | Yes |
| GET | `/loans/number/{loanNumber}` | Get loan by number | Yes |

### Admin Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/admin/loans/pending` | Get pending loans | Admin |
| GET | `/admin/loans?status=X` | Get loans by status | Admin |
| GET | `/admin/loans/{loanId}` | Get loan details | Admin |
| PUT | `/admin/loans/{loanId}/approve` | Approve/reject loan | Admin |
| PUT | `/admin/loans/{loanId}/review` | Mark under review | Admin |

## 🧪 Testing

### Run Unit Tests
```bash
mvn test
```

### API Testing with Postman

1. Import the Postman collection from `postman/Smart-Bank-API.postman_collection.json`
2. Follow the testing guide in `TESTING_GUIDE.md`
3. Test all 35 test cases

### Manual Testing Flow

1. **Register** → Verify OTP → **Login**
2. **Create Account** → View accounts
3. **Apply for Loan** → Admin approves
4. **Transfer Funds** → View transactions

## 🏗️ Project Structure
```
smart-bank/
├── src/main/java/com/bank/smartbank/
│   ├── config/              # Configuration classes
│   │   └── DataSeeder.java
│   ├── controller/          # REST Controllers
│   │   ├── AuthController.java
│   │   ├── AccountController.java
│   │   ├── TransferController.java
│   │   ├── TransactionController.java
│   │   ├── LoanController.java
│   │   └── AdminController.java
│   ├── dto/                 # Data Transfer Objects
│   │   ├── common/
│   │   ├── auth/
│   │   ├── account/
│   │   ├── transaction/
│   │   └── loan/
│   ├── entity/              # JPA Entities
│   │   ├── User.java
│   │   ├── Account.java
│   │   ├── Transaction.java
│   │   └── Loan.java
│   ├── exception/           # Custom Exceptions
│   ├── repository/          # Spring Data Repositories
│   ├── security/            # Security Configuration
│   │   ├── JwtTokenProvider.java
│   │   ├── JwtAuthenticationFilter.java
│   │   ├── UserDetailsServiceImpl.java
│   │   ├── CurrentUser.java
│   │   └── SecurityConfig.java
│   ├── service/             # Business Logic
│   │   ├── AuthService.java
│   │   ├── AccountService.java
│   │   ├── TransactionService.java
│   │   ├── TransferService.java
│   │   └── LoanService.java
│   └── util/                # Utility Classes
│       ├── Constants.java
│       ├── OtpGenerator.java
│       ├── AccountNumberGenerator.java
│       └── EmailService.java
├── src/main/resources/
│   ├── application.yml
│   └── application-prod.yml
└── pom.xml
```

## 🔒 Security Features

- JWT token-based authentication
- BCrypt password hashing
- Role-based access control (RBAC)
- CORS configuration
- Input validation
- SQL injection prevention (JPA)
- XSS prevention (Spring Security)

## 📊 Database Schema

### Tables
- `users` - User accounts
- `accounts` - Bank accounts
- `transactions` - Transaction history
- `loans` - Loan applications

### Relationships
- One User → Many Accounts
- One Account → Many Transactions
- One User → Many Loans

## 🚀 Deployment

### Production Checklist
- [ ] Set environment variables for secrets
- [ ] Configure production database
- [ ] Enable HTTPS
- [ ] Set `ddl-auto` to `validate`
- [ ] Disable detailed error messages
- [ ] Configure logging to file
- [ ] Set up monitoring
- [ ] Configure backup strategy
- [ ] Update CORS settings
- [ ] Review security settings

### Environment Variables
```bash
export DB_URL=jdbc:mysql://prod-server:3306/smart_bank_prod
export DB_USERNAME=prod_user
export DB_PASSWORD=secure_password
export JWT_SECRET=your_secret_key_min_256_bits
export SMTP_HOST=smtp.gmail.com
export SMTP_USERNAME=your_email
export SMTP_PASSWORD=your_app_password
```

### Run in Production
```bash
mvn clean package
java -jar -Dspring.profiles.active=prod target/smartbank-0.0.1-SNAPSHOT.jar
```

## 📈 Future Enhancements

- [ ] Password reset functionality
- [ ] Account statement PDF generation
- [ ] Push notifications
- [ ] Two-factor authentication (2FA)
- [ ] Credit score integration
- [ ] EMI payment tracking
- [ ] Recurring payments
- [ ] Beneficiary management
- [ ] Account freezing/unfreezing
- [ ] Admin dashboard (frontend)
- [ ] Customer dashboard (frontend)
- [ ] Real-time balance updates (WebSocket)
- [ ] Transaction dispute handling
- [ ] KYC verification
- [ ] Multi-currency support

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📝 License

This project is licensed under the MIT License.

## 👨‍💻 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- Email: your.email@example.com

## 🙏 Acknowledgments

- Spring Boot Documentation
- Baeldung Tutorials
- Stack Overflow Community

---

**Built with ❤️ using Spring Boot**
```

---

## ✅ FINAL CHECKLIST

### **Code Quality**
```
✅ CurrentUser properly implemented
✅ All System.out.println replaced with logger
✅ @EnableMethodSecurity added to SecurityConfig
✅ Admin user auto-created on startup
✅ All controllers have proper error handling
✅ All services use @Transactional
✅ All DTOs use proper validation
✅ No hardcoded values (use Constants)
```

### **Documentation**
```
✅ README.md created
✅ TESTING_GUIDE.md created
✅ Postman collection created
✅ API endpoints documented
✅ Code comments added
```

### **Configuration**
```
✅ application.yml configured
✅ application-prod.yml created
✅ Logging configured
✅ CORS enabled
✅ Security properly configured
```

### **Testing**
```
✅ All 35 test cases defined
✅ Postman collection ready
✅ Admin user created
✅ Database schema verified
