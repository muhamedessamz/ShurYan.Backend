# ShurYan – Backend Documentation

<div align="center">
  <img src="./images/shuryan.png" alt="ShurYan Logo" width="200" style="margin: 0 20px;"/>
  <img src="./images/proAr.png" alt="DEPI Logo" width="150" style="margin: 0 20px;"/>
</div>

<div align="center">
  <strong>Developed as a Graduation Project for the <a href="https://depi.gov.eg/">Dew of Egypt Digital Initiative (DEPI)</a></strong>
</div>

<br/>

<div align="center">
  
![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=for-the-badge&logo=dotnet)
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoft-sql-server)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![DEPI](https://img.shields.io/badge/DEPI-2025-orange?style=for-the-badge)

</div>

---

<div align="center">

### 📌 Main Repository

This is the **Backend** repository. For complete project overview, architecture diagram, and links to all repositories:

**[🏠 Visit ShurYan Main Repository →](https://github.com/muhamedessamz/ShurYan)**

</div>

---

## Table of Contents

1. [Project Introduction](#project-introduction)
2. [Architecture Overview](#architecture-overview)
3. [Tech Stack](#tech-stack)
4. [Folder Structure](#folder-structure)
5. [Environment Setup](#environment-setup)
6. [Database Schema](#database-schema)
7. [API Endpoints](#api-endpoints)
8. [Authentication & Authorization](#authentication--authorization)
9. [Error Handling & Logging](#error-handling--logging)
10. [Testing](#testing)
11. [Deployment Instructions](#deployment-instructions)
12. [Swagger Documentation](#swagger-documentation)
13. [Security Best Practices](#security-best-practices)
14. [Usage Examples](#usage-examples)
15. [Contributing Guidelines](#contributing-guidelines)
16. [License](#license)

---

## Project Introduction

**ShurYan** is a comprehensive healthcare management system designed to connect patients, doctors, laboratories, and pharmacies in a unified digital platform. The backend provides a robust RESTful API built with modern .NET technologies, implementing clean architecture principles and industry best practices.

### Key Features

- **Multi-role Authentication**: Support for Patients, Doctors, Laboratories, Pharmacies, and Verifiers
- **Appointment Management**: Complete booking and scheduling system
- **Medical Records**: Digital prescriptions, lab orders, and medical history
- **Real-time Notifications**: SignalR-based notification system
- **Payment Integration**: Paymob payment gateway integration
- **AI-Powered Chat**: Gemini AI integration for medical consultations
- **Document Management**: Cloudinary-based file storage
- **Review System**: Rating and feedback for healthcare providers

---

## Architecture Overview

ShurYan follows **Clean Architecture** principles with clear separation of concerns:

```
┌─────────────────────────────────────────────────────┐
│                  Presentation Layer                  │
│              (Shuryan.API - Controllers)             │
└──────────────────┬──────────────────────────────────┘
                   │
┌──────────────────▼──────────────────────────────────┐
│                 Application Layer                    │
│    (Shuryan.Application - Services, DTOs, Maps)     │
└──────────────────┬──────────────────────────────────┘
                   │
┌──────────────────▼──────────────────────────────────┐
│                   Domain Layer                       │
│      (Shuryan.Core - Entities, Interfaces)          │
└──────────────────┬──────────────────────────────────┘
                   │
┌──────────────────▼──────────────────────────────────┐
│              Infrastructure Layer                    │
│  (Shuryan.Infrastructure - Data, Repositories)      │
└──────────────────┬──────────────────────────────────┘
                   │
┌──────────────────▼──────────────────────────────────┐
│              Cross-Cutting Concerns                  │
│   (Shuryan.Shared - Extensions, Configurations)     │
└─────────────────────────────────────────────────────┘
```

### Layer Responsibilities

- **API Layer**: HTTP endpoints, request/response handling, authentication filters
- **Application Layer**: Business logic, DTOs, validation, service orchestration
- **Core Layer**: Domain entities, business rules, interfaces (framework-agnostic)
- **Infrastructure Layer**: Database access, external services, repositories
- **Shared Layer**: Cross-cutting concerns, configurations, extensions

---

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **.NET** | 8.0 | Core framework |
| **ASP.NET Core** | 8.0 | Web API framework |
| **Entity Framework Core** | 8.0.20 | ORM for database access |
| **SQL Server** | Latest | Primary database |
| **ASP.NET Identity** | 8.0 | User authentication & authorization |
| **JWT Bearer** | Latest | Token-based authentication |
| **AutoMapper** | 12.0.1 | Object-to-object mapping |
| **FluentValidation** | Latest | Input validation |
| **SignalR** | 8.0 | Real-time notifications |
| **Swagger/OpenAPI** | 8.1.4 | API documentation |
| **Cloudinary** | Latest | File/image storage |
| **Paymob** | Custom | Payment processing |
| **Google OAuth** | Latest | Social authentication |
| **Gemini AI** | Latest | AI chat integration |

### Why These Technologies?

- **.NET 8**: Latest LTS version with improved performance and modern C# features
- **EF Core**: Type-safe database access with LINQ support and migrations
- **JWT**: Stateless authentication suitable for distributed systems
- **SignalR**: Built-in WebSocket support for real-time features
- **AutoMapper**: Reduces boilerplate code for DTO mappings
- **FluentValidation**: Expressive, testable validation rules

---

## Folder Structure

```
ShurYan-Backend-dev/
├── src/
│   ├── Shuryan.API/                    # Presentation Layer
│   │   ├── Controllers/                # API endpoints (30 controllers)
│   │   │   ├── AuthController.cs
│   │   │   ├── DoctorsController.cs
│   │   │   ├── PatientsController.cs
│   │   │   ├── AppointmentsController.cs
│   │   │   ├── PrescriptionsController.cs
│   │   │   ├── LaboratoriesController.cs
│   │   │   ├── PaymentsController.cs
│   │   │   └── ...
│   │   ├── Extensions/
│   │   │   └── ServiceExtensions.cs    # DI configuration
│   │   ├── Hubs/
│   │   │   └── NotificationHub.cs      # SignalR hub
│   │   ├── Services/
│   │   │   └── NotificationHubService.cs
│   │   ├── Program.cs                  # Application entry point
│   │   ├── appsettings.json            # Configuration
│   │   └── appsettings.Development.json
│   │
│   ├── Shuryan.Application/            # Application Layer
│   │   ├── DTOs/                       # Data Transfer Objects
│   │   │   ├── Requests/
│   │   │   └── Responses/
│   │   ├── Interfaces/                 # Service contracts
│   │   ├── Services/                   # Business logic (34 services)
│   │   │   ├── Auth/
│   │   │   ├── Email/
│   │   │   ├── Token/
│   │   │   ├── AI/
│   │   │   └── ...
│   │   ├── Mappers/                    # AutoMapper profiles
│   │   └── Validators/                 # FluentValidation rules
│   │
│   ├── Shuryan.Core/                   # Domain Layer
│   │   ├── Entities/                   # Domain models (51 entities)
│   │   │   ├── Identity/
│   │   │   ├── Medical/
│   │   │   ├── External/
│   │   │   ├── System/
│   │   │   └── Shared/
│   │   ├── Enums/                      # Enumerations
│   │   ├── Interfaces/                 # Repository contracts
│   │   └── Settings/                   # Configuration models
│   │
│   ├── Shuryan.Infrastructure/         # Infrastructure Layer
│   │   ├── Data/
│   │   │   └── ShuryanDbContext.cs     # EF Core context
│   │   ├── Migrations/                 # Database migrations
│   │   ├── Repositories/               # Data access (42 repositories)
│   │   ├── Seeders/                    # Database seeding
│   │   └── UnitOfWork/
│   │
│   ├── Shuryan.Shared/                 # Cross-cutting Concerns
│   │   ├── Extensions/
│   │   │   ├── AuthenticationExtensions.cs
│   │   │   ├── CorsExtensions.cs
│   │   │   ├── DatabaseExtensions.cs
│   │   │   └── IdentityExtensions.cs
│   │   └── Configurations/
│   │
│   ├── Shuryan.Tests/                  # Unit & Integration Tests
│   │
│   └── Shuryan.sln                     # Solution file
│
├── docs/                               # Documentation
├── LICENSE                             # MIT License
└── README.md
```

---

## Environment Setup

### Prerequisites

- **.NET 8 SDK** or later ([Download](https://dotnet.microsoft.com/download))
- **SQL Server** (LocalDB, Express, or Full)
- **Visual Studio 2022** or **VS Code** with C# extension
- **Git** for version control

### Local Development Setup

#### 1. Clone the Repository

```bash
git clone <repository-url>
cd ShurYan-Backend-dev/src
```

#### 2. Configure Environment Variables

Create `appsettings.Development.Local.json` in `Shuryan.API/` (this file is gitignored):

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ShuryanDb;Trusted_Connection=true;MultipleActiveResultSets=true"
  },
  "JwtSettings": {
    "Issuer": "https://localhost:7001",
    "Audience": "https://localhost:7001",
    "ExpiryInHours": 24,
    "SecretKey": "your-super-secret-key-min-32-characters-long"
  },
  "EmailSettings": {
    "SmtpServer": "smtp.gmail.com",
    "SmtpPort": 587,
    "SenderEmail": "your-email@gmail.com",
    "SenderName": "ShurYan Healthcare",
    "Username": "your-email@gmail.com",
    "Password": "your-app-password"
  },
  "CloudinarySettings": {
    "CloudName": "your-cloud-name",
    "ApiKey": "your-api-key",
    "ApiSecret": "your-api-secret"
  },
  "Paymob": {
    "APIKey": "your-paymob-api-key",
    "PublicKey": "your-public-key",
    "SecretKey": "your-secret-key",
    "HMAC": "your-hmac-secret",
    "CardIntegrationId": "integration-id",
    "MobileIntegrationId": "integration-id"
  },
  "OAuthSettings": {
    "Google": {
      "ClientId": "your-google-client-id",
      "ClientSecret": "your-google-client-secret"
    }
  },
  "CorsSettings": {
    "PolicyName": "ShuryanCorsPolicy",
    "AllowedOrigins": ["http://localhost:3000", "http://localhost:5173"]
  }
}
```

#### 3. Restore Dependencies

```bash
dotnet restore
```

#### 4. Apply Database Migrations

```bash
cd Shuryan.API
dotnet ef database update
```

#### 5. Run the Application

```bash
dotnet run
```

The API will be available at:
- HTTPS: `https://localhost:7001`
- HTTP: `http://localhost:5001`
- Swagger UI: `https://localhost:7001/swagger`

### Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `ConnectionStrings:DefaultConnection` | SQL Server connection string | `Server=...;Database=ShuryanDb;...` |
| `JwtSettings:SecretKey` | JWT signing key (min 32 chars) | `your-secret-key-here` |
| `JwtSettings:ExpiryInHours` | Token expiration time | `24` |
| `EmailSettings:SmtpServer` | SMTP server address | `smtp.gmail.com` |
| `EmailSettings:SenderEmail` | From email address | `noreply@shuryan.com` |
| `CloudinarySettings:CloudName` | Cloudinary cloud name | `your-cloud` |
| `Paymob:APIKey` | Paymob API key | `your-api-key` |
| `OAuthSettings:Google:ClientId` | Google OAuth client ID | `xxx.apps.googleusercontent.com` |
| `CorsSettings:AllowedOrigins` | Allowed frontend URLs | `["http://localhost:3000"]` |

---

## Database Schema

### Entity Relationship Overview

The database consists of **51 entities** organized into logical modules:

#### Identity Module
- **User** (base identity)
- **Doctor**, **Patient**, **Laboratory**, **Pharmacy**, **Verifier** (role-specific profiles)
- **Role** (authorization roles)
- **RefreshToken** (JWT refresh tokens)

#### Medical Module
- **Appointment** (doctor-patient appointments)
- **ConsultationRecord** (medical session records)
- **DoctorConsultation** (consultation types)
- **DoctorAvailability** (doctor schedules)
- **DoctorOverride** (schedule exceptions)

#### External Services Module
- **Clinic** (doctor clinic information)
- **LabPrescription**, **LabOrder**, **LabResult** (laboratory workflow)
- **Prescription**, **PrescribedMedication** (pharmacy prescriptions)
- **Payment**, **PaymentTransaction** (payment processing)

#### System Module
- **Notification** (user notifications)
- **EmailVerification** (email OTP tokens)
- **Conversation**, **ConversationMessage** (AI chat)
- **DoctorReview**, **LaboratoryReview**, **PharmacyReview** (ratings)

### Key Relationships

```
User (1) ──── (1) Doctor/Patient/Laboratory/Pharmacy
Doctor (1) ──── (*) Appointment ──── (1) Patient
Doctor (1) ──── (*) ConsultationRecord ──── (1) Patient
Doctor (1) ──── (*) DoctorAvailability
Patient (1) ──── (*) Prescription ──── (*) Pharmacy
Patient (1) ──── (*) LabPrescription ──── (*) Laboratory
User (1) ──── (*) Notification
User (1) ──── (*) Conversation ──── (*) ConversationMessage
```

### Sample Entity: Doctor

```csharp
public class Doctor : ProfileUser
{
    public string? Specialty { get; set; }
    public int YearsOfExperience { get; set; }
    public string? LicenseNumber { get; set; }
    public decimal ConsultationFee { get; set; }
    public VerificationStatus VerificationStatus { get; set; }
    
    // Navigation Properties
    public virtual ICollection<Appointment> Appointments { get; set; }
    public virtual ICollection<DoctorAvailability> Availabilities { get; set; }
    public virtual ICollection<Clinic> Clinics { get; set; }
    public virtual ICollection<DoctorReview> Reviews { get; set; }
}
```

---

## API Endpoints

### Authentication Endpoints (`/api/Auth`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/register/patient` | Register new patient | No |
| POST | `/register/doctor` | Register new doctor | No |
| POST | `/register/laboratory` | Register new laboratory | No |
| POST | `/register/pharmacy` | Register new pharmacy | No |
| POST | `/verify-email` | Verify email with OTP | No |
| POST | `/resend-otp` | Resend verification OTP | No |
| POST | `/login` | Login with credentials | No |
| POST | `/google-auth` | Google OAuth login | No |
| POST | `/forgot-password` | Request password reset | No |
| POST | `/reset-password` | Reset password with token | No |
| POST | `/change-password` | Change password | Yes |
| POST | `/refresh-token` | Refresh JWT token | No |
| POST | `/logout` | Logout user | Yes |
| DELETE | `/delete-account` | Delete user account | Yes |

#### Example: Register Patient

**Request:**
```http
POST /api/Auth/register/patient
Content-Type: application/json

{
  "firstName": "Ahmed",
  "lastName": "Hassan",
  "email": "ahmed@example.com",
  "password": "SecurePass123!",
  "phoneNumber": "+201234567890",
  "dateOfBirth": "1990-05-15",
  "gender": "Male",
  "bloodType": "O+"
}
```

**Response (201 Created):**
```json
{
  "success": true,
  "message": "Patient registered successfully. Please verify your email.",
  "data": {
    "userId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "email": "ahmed@example.com",
    "requiresEmailVerification": true
  }
}
```

#### Example: Login

**Request:**
```http
POST /api/Auth/login
Content-Type: application/json

{
  "email": "ahmed@example.com",
  "password": "SecurePass123!"
}
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "userId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "email": "ahmed@example.com",
    "roles": ["Patient"],
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "refresh-token-here",
    "expiresAt": "2026-01-07T04:14:22Z"
  }
}
```

### Doctor Endpoints (`/api/Doctors`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/my-profile` | Get current doctor profile | Doctor |
| GET | `/{id}` | Get doctor by ID | All |
| GET | `/personal` | Get personal info | Doctor |
| GET | `/professional` | Get professional info | Doctor |
| PUT | `/update-profile` | Update full profile | Doctor |
| PUT | `/personal` | Update personal info | Doctor |
| PUT | `/specialty` | Update specialty/experience | Doctor |
| PUT | `/profile-image` | Update profile image | Doctor |
| GET | `/list` | Get paginated doctors list | All |
| GET | `/{id}/details` | Get doctor with clinic details | All |
| POST | `/submit-review` | Submit for verification | Doctor |
| GET | `/specialties` | Get all specialties | All |

### Patient Endpoints (`/api/Patients`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/current` | Get current patient profile | Patient |
| GET | `/email/{email}` | Get patient by email | Admin |
| GET | `/all` | Get all patients | Admin |
| GET | `/paginated` | Get paginated patients | Admin |
| GET | `/search` | Search patients | Admin |
| GET | `/nearby-pharmacies` | Find nearby pharmacies | Patient |
| POST | `/send-prescription/{pharmacyId}` | Send prescription to pharmacy | Patient |
| GET | `/prescription/{prescriptionId}/responses` | Get pharmacy responses | Patient |

### Appointment Endpoints (`/api/Appointments`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/book` | Book new appointment | Patient |
| GET | `/{id}` | Get appointment details | Doctor, Patient |
| PUT | `/{id}/status` | Update appointment status | Doctor |
| DELETE | `/{id}` | Cancel appointment | Patient, Doctor |
| GET | `/patient/upcoming` | Get patient upcoming appointments | Patient |
| GET | `/doctor/today` | Get doctor today's appointments | Doctor |

### Prescription Endpoints (`/api/Prescriptions`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/create` | Create prescription | Doctor |
| GET | `/{id}` | Get prescription details | Doctor, Patient, Pharmacy |
| GET | `/patient/{patientId}` | Get patient prescriptions | Doctor, Patient |
| PUT | `/{id}/dispense` | Mark as dispensed | Pharmacy |

### Payment Endpoints (`/api/Payments`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/initiate` | Initiate payment | Patient |
| POST | `/callback` | Paymob callback | System |
| GET | `/{id}` | Get payment details | Patient |
| GET | `/user/history` | Get payment history | Patient |

### Notification Endpoints (`/api/Notifications`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/my-notifications` | Get user notifications | All |
| PUT | `/{id}/read` | Mark as read | All |
| PUT | `/mark-all-read` | Mark all as read | All |
| DELETE | `/{id}` | Delete notification | All |

### Chat Endpoints (`/api/Chat`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/send-message` | Send AI chat message | All Authenticated |
| GET | `/history` | Get chat history with pagination | All Authenticated |
| DELETE | `/clear` | Clear user chat history | All Authenticated |

#### Example: Send AI Message

**Request:**
```http
POST /api/Chat/send-message
Authorization: Bearer {token}
Content-Type: application/json

{
  "message": "What are the symptoms of diabetes?",
  "conversationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Message sent successfully",
  "data": {
    "conversationId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "userMessage": "What are the symptoms of diabetes?",
    "aiResponse": "Common symptoms of diabetes include...",
    "timestamp": "2026-01-06T04:23:01Z"
  }
}
```

---

### Doctor Dashboard Endpoints (`/api/doctors/me/dashboard`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/stats` | Get dashboard statistics | Doctor |
| GET | `/appointments` | Get doctor appointments (filtered) | Doctor |
| GET | `/appointments/today` | Get today's appointments | Doctor |

#### Dashboard Stats Response Example

```json
{
  "totalPatients": 156,
  "todayAppointments": 8,
  "upcomingAppointments": 23,
  "completedSessions": 342,
  "averageRating": 4.7,
  "totalReviews": 89,
  "monthlyRevenue": 45000.00,
  "pendingPrescriptions": 3
}
```

---

### Doctor Sessions Endpoints (`/api/doctors/me/sessions`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/active` | Get current active session | Doctor |

**Active Session** represents the current consultation session with a patient, including appointment details, patient info, and session start time.

---

### Doctor Schedule Endpoints (`/api/doctors/me/schedule`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/weekly` | Get weekly schedule | Doctor, Patient |
| GET | `/exceptional-dates` | Get exceptional dates (holidays/overrides) | Doctor, Patient |
| GET | `/services` | Get doctor services with pricing | Doctor, Patient |
| GET | `/booked-appointments` | Get booked appointments for date range | Doctor |
| GET | `/available-slots` | Get available time slots for booking | Patient |

#### Example: Get Available Time Slots

**Request:**
```http
GET /api/doctors/me/schedule/available-slots?doctorId={doctorId}&date=2026-01-10&serviceId={serviceId}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "date": "2026-01-10",
    "availableSlots": [
      { "startTime": "09:00", "endTime": "09:30", "isAvailable": true },
      { "startTime": "09:30", "endTime": "10:00", "isAvailable": true },
      { "startTime": "10:00", "endTime": "10:30", "isAvailable": false },
      { "startTime": "14:00", "endTime": "14:30", "isAvailable": true }
    ]
  }
}
```

---

### Doctor Reviews Endpoints (`/api/doctors/me/reviews`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get doctor reviews (paginated) | Doctor |
| GET | `/statistics` | Get review statistics | Doctor |
| GET | `/{reviewId}` | Get review details | Doctor |
| POST | `/{reviewId}/reply` | Reply to a review | Doctor |

#### Review Statistics Example

```json
{
  "totalReviews": 89,
  "averageRating": 4.7,
  "ratingDistribution": {
    "5": 65,
    "4": 18,
    "3": 4,
    "2": 1,
    "1": 1
  },
  "recentReviews": [...]
}
```

---

### Doctor Services Endpoints (`/api/doctors/me/services`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get all doctor services | Doctor |
| POST | `/` | Add new service | Doctor |
| PUT | `/{serviceId}` | Update service | Doctor |
| DELETE | `/{serviceId}` | Delete service | Doctor |
| PATCH | `/{serviceId}/availability` | Toggle service availability | Doctor |

---

### Doctor Partners Endpoints (`/api/doctors/me/partners`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/suggestions` | Get partner suggestions | Doctor |
| POST | `/add` | Add partner (lab/pharmacy) | Doctor |
| DELETE | `/{partnerId}` | Remove partner | Doctor |

**Partner System**: Allows doctors to maintain a list of preferred laboratories and pharmacies for referrals.

---

### Doctor Patients Endpoints (`/api/doctors/me/patients`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get doctor's patients list | Doctor |
| GET | `/{patientId}` | Get patient details | Doctor |
| GET | `/{patientId}/history` | Get patient medical history | Doctor |
| GET | `/{patientId}/appointments` | Get patient appointments | Doctor |

---

### Doctor Lab Prescriptions Endpoints (`/api/doctors/me/lab-prescriptions`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/create` | Create lab prescription | Doctor |
| GET | `/{prescriptionId}` | Get prescription details | Doctor |
| GET | `/patient/{patientId}` | Get patient lab prescriptions | Doctor |

---

### Doctor Documents Endpoints (`/api/doctors/me/documents`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get all doctor documents | Doctor |
| POST | `/upload` | Upload new document | Doctor |
| DELETE | `/{documentId}` | Delete document | Doctor |

**Document Types**: Medical license, certifications, ID card, specialty certificates, etc.

---

### Verifier Endpoints (`/api/Verifier`)

**Verifier Role**: Responsible for reviewing and approving/rejecting doctor registration applications.

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/start-review/{doctorId}` | Start reviewing doctor application | Verifier |
| POST | `/verify/{doctorId}` | Approve doctor registration | Verifier |
| POST | `/reject/{doctorId}` | Reject doctor registration | Verifier |
| GET | `/doctors/sent` | Get doctors with "Sent" status | Verifier |
| GET | `/doctors/under-review` | Get doctors under review | Verifier |
| GET | `/doctors/verified` | Get verified doctors | Verifier |
| GET | `/doctors/rejected` | Get rejected doctors | Verifier |
| GET | `/doctors/{doctorId}/documents` | Get doctor documents for review | Verifier |
| POST | `/documents/{documentId}/approve` | Approve specific document | Verifier |
| POST | `/documents/{documentId}/reject` | Reject specific document | Verifier |

#### Doctor Verification Flow

1. Doctor submits registration → Status: **Sent**
2. Verifier starts review → Status: **UnderReview**
3. Verifier reviews documents (approve/reject each)
4. Verifier makes final decision:
   - Approve → Status: **Verified** (doctor can start practicing)
   - Reject → Status: **Rejected** (with rejection reason)

---

### Laboratory Profile Endpoints (`/api/laboratories/me/profile`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/basic-info` | Get basic laboratory info | Laboratory |
| PUT | `/basic-info` | Update basic info | Laboratory |
| PUT | `/profile-image` | Update profile image | Laboratory |
| GET | `/address` | Get laboratory address | Laboratory |
| PUT | `/address` | Update address | Laboratory |
| GET | `/working-hours` | Get working hours | Laboratory |
| PUT | `/working-hours` | Update working hours | Laboratory |
| GET | `/home-collection` | Get home sample collection settings | Laboratory |
| PUT | `/home-collection` | Update home collection settings | Laboratory |

---

### Laboratory Services Endpoints (`/api/laboratories/me/services`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get all lab services | Laboratory |
| POST | `/` | Add new lab service | Laboratory |
| PUT | `/{serviceId}` | Update lab service | Laboratory |
| DELETE | `/{serviceId}` | Delete lab service | Laboratory |
| PATCH | `/{serviceId}/availability` | Toggle service availability | Laboratory |
| GET | `/available-tests` | Get available lab tests catalog | Laboratory |

---

### Laboratory Orders Endpoints (`/api/laboratories/me/orders`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get all lab orders (filtered) | Laboratory |
| GET | `/{orderId}` | Get order details | Laboratory |
| PUT | `/{orderId}/respond` | Respond to order (accept/reject with price) | Laboratory |
| POST | `/{orderId}/start-work` | Start processing order | Laboratory |
| POST | `/{orderId}/results` | Upload lab results | Laboratory |
| GET | `/{orderId}/results` | Get order results | Laboratory |

#### Laboratory Order Workflow

1. Patient sends lab prescription → Status: **Pending**
2. Laboratory responds with price → Status: **Quoted**
3. Patient pays → Status: **Paid**
4. Laboratory collects sample → Status: **SampleCollected**
5. Laboratory starts work → Status: **InProgress**
6. Laboratory uploads results → Status: **Completed**

---

### Laboratory Dashboard Endpoints (`/api/laboratories/me/dashboard`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get dashboard overview | Laboratory |
| GET | `/statistics` | Get detailed statistics | Laboratory |

---

### Pharmacy Profile Endpoints (`/api/pharmacies/me/profile`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/basic-info` | Get pharmacy basic info | Pharmacy |
| PUT | `/basic-info` | Update basic info | Pharmacy |
| PUT | `/profile-image` | Update profile image | Pharmacy |
| GET | `/address` | Get pharmacy address | Pharmacy |
| PUT | `/address` | Update address | Pharmacy |
| GET | `/working-hours` | Get working hours | Pharmacy |
| PUT | `/working-hours` | Update working hours | Pharmacy |

---

### Pharmacy Orders Endpoints (`/api/pharmacies/me/orders`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get all pharmacy orders | Pharmacy |
| GET | `/{orderId}` | Get order details | Pharmacy |
| POST | `/{orderId}/respond` | Respond with availability & price | Pharmacy |
| POST | `/{orderId}/dispense` | Mark prescription as dispensed | Pharmacy |

---

### Patient Profile Endpoints (`/api/patients/me/profile`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/` | Get patient profile | Patient |
| PUT | `/` | Update patient profile | Patient |
| PUT | `/profile-image` | Update profile image | Patient |

---

### Patient Appointments Endpoints (`/api/patients/me/appointments`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/upcoming` | Get upcoming appointments | Patient |
| GET | `/history` | Get past appointments | Patient |
| POST | `/book` | Book new appointment | Patient |
| DELETE | `/{appointmentId}` | Cancel appointment | Patient |

---

### Patient Medical Endpoints (`/api/patients/me/medical`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/prescriptions` | Get all prescriptions | Patient |
| GET | `/prescriptions/{id}` | Get prescription details | Patient |
| GET | `/medical-history` | Get medical history | Patient |
| POST | `/medical-history` | Add medical history item | Patient |

---

### Patient Lab Endpoints (`/api/patients/me/lab`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/prescriptions` | Get lab prescriptions | Patient |
| POST | `/prescriptions/{id}/send` | Send to laboratory | Patient |
| GET | `/orders` | Get lab orders | Patient |
| GET | `/orders/{id}/results` | Get lab results | Patient |

---

### Patient Reviews Endpoints (`/api/patients/me/reviews`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| POST | `/doctor` | Submit doctor review | Patient |
| POST | `/laboratory` | Submit laboratory review | Patient |
| POST | `/pharmacy` | Submit pharmacy review | Patient |
| GET | `/my-reviews` | Get patient's submitted reviews | Patient |

---

### Clinics Endpoints (`/api/Clinics`)

| Method | Endpoint | Description | Roles |
|--------|----------|-------------|-------|
| GET | `/{clinicId}` | Get clinic details | All |
| GET | `/doctor/{doctorId}` | Get doctor's clinics | All |
| POST | `/` | Create new clinic | Doctor |
| PUT | `/{clinicId}` | Update clinic | Doctor |
| DELETE | `/{clinicId}` | Delete clinic | Doctor |

---

## Authentication & Authorization

### JWT Token-Based Authentication

ShurYan uses **JWT (JSON Web Tokens)** for stateless authentication.

#### Login Flow

1. User submits credentials to `/api/Auth/login`
2. Server validates credentials against database
3. If valid, server generates:
   - **Access Token** (JWT, expires in 24 hours)
   - **Refresh Token** (stored in database, expires in 7 days)
4. Client stores tokens securely
5. Client includes access token in `Authorization` header for protected requests
6. When access token expires, client uses refresh token to get new access token

#### Token Structure

```json
{
  "sub": "user-id-guid",
  "email": "user@example.com",
  "role": "Doctor",
  "jti": "token-id",
  "exp": 1704614062,
  "iss": "https://api.shuryan.com",
  "aud": "https://api.shuryan.com"
}
```

#### Using Tokens in Requests

```http
GET /api/Doctors/my-profile
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Role-Based Authorization

ShurYan implements role-based access control (RBAC) with the following roles:

- **Patient**: Book appointments, view prescriptions, manage profile
- **Doctor**: Manage appointments, create prescriptions, view patient records
- **Laboratory**: Process lab orders, upload results
- **Pharmacy**: View prescriptions, manage dispensing
- **Verifier**: Approve/reject doctor registrations
- **Admin**: Full system access

#### Authorization Attributes

```csharp
[Authorize(Roles = "Doctor")]
public async Task<IActionResult> GetMyProfile() { }

[Authorize(Roles = "Patient,Doctor")]
public async Task<IActionResult> GetAppointment(Guid id) { }
```

### Email Verification

New users must verify their email before accessing protected features:

1. User registers → OTP sent to email
2. User submits OTP to `/api/Auth/verify-email`
3. Email verified → User can login

---

## Real-Time Notifications (SignalR)

ShurYan implements **SignalR** for real-time push notifications to users.

### SignalR Hub Endpoint

**WebSocket URL**: `wss://api.shuryan.com/hubs/notifications`

### Connection Setup (JavaScript)

```javascript
import * as signalR from '@microsoft/signalr';

const connection = new signalR.HubConnectionBuilder()
  .withUrl('https://api.shuryan.com/hubs/notifications', {
    accessTokenFactory: () => localStorage.getItem('token')
  })
  .withAutomaticReconnect()
  .build();

// Listen for notifications
connection.on('ReceiveNotification', (notification) => {
  console.log('New notification:', notification);
  // Update UI with notification
});

// Start connection
await connection.start();
```

### Notification Events

| Event Name | Description | Payload |
|------------|-------------|---------|
| `ReceiveNotification` | New notification received | `{ id, title, message, type, timestamp }` |
| `AppointmentBooked` | New appointment booked | `{ appointmentId, patientName, date, time }` |
| `AppointmentCancelled` | Appointment cancelled | `{ appointmentId, reason }` |
| `PrescriptionReady` | Prescription ready for pickup | `{ prescriptionId, pharmacyName }` |
| `LabResultsReady` | Lab results uploaded | `{ orderId, laboratoryName }` |

### Notification Types

- **Appointment**: Booking confirmations, reminders, cancellations
- **Prescription**: New prescriptions, pharmacy responses, ready for pickup
- **LabOrder**: Lab order updates, results ready
- **Payment**: Payment confirmations, receipts
- **Review**: New reviews received
- **Verification**: Doctor verification status updates
- **System**: General system announcements

---

## File Upload & Storage (Cloudinary)

ShurYan uses **Cloudinary** for secure file storage and image optimization.

### Supported File Types

| Category | Extensions | Max Size |
|----------|-----------|----------|
| **Images** | .jpg, .jpeg, .png, .gif, .webp | 10 MB |
| **Documents** | .pdf, .doc, .docx | 25 MB |
| **Lab Results** | .pdf, .jpg, .png | 25 MB |

### Upload Endpoints

| Endpoint | Purpose | Roles |
|----------|---------|-------|
| `PUT /api/doctors/me/profile-image` | Doctor profile image | Doctor |
| `PUT /api/patients/me/profile-image` | Patient profile image | Patient |
| `POST /api/doctors/me/documents/upload` | Doctor verification documents | Doctor |
| `POST /api/laboratories/me/orders/{id}/results` | Lab result files | Laboratory |

### Upload Example

```javascript
const formData = new FormData();
formData.append('file', fileInput.files[0]);

const response = await fetch('/api/doctors/me/profile-image', {
  method: 'PUT',
  headers: {
    'Authorization': `Bearer ${token}`
  },
  body: formData
});
```

### Image Transformations

Cloudinary automatically optimizes images:
- **Thumbnails**: 150x150px for avatars
- **Medium**: 800x800px for profile images
- **Format**: Auto-convert to WebP for better compression
- **Quality**: Auto-adjust based on content

---

## Payment Integration (Paymob)

ShurYan integrates with **Paymob** payment gateway for secure online payments.

### Payment Flow

1. **Initiate Payment**
   ```http
   POST /api/Payments/initiate
   {
     "amount": 500.00,
     "appointmentId": "guid",
     "paymentMethod": "Card"
   }
   ```

2. **Redirect to Paymob**
   - User redirected to Paymob payment page
   - User enters card details
   - Paymob processes payment

3. **Callback Handling**
   ```http
   POST /api/Payments/callback
   ```
   - Paymob sends payment result
   - System updates payment status
   - Notification sent to user

4. **Payment Confirmation**
   - Status: **Completed** or **Failed**
   - Receipt generated and emailed

### Supported Payment Methods

- **Credit/Debit Cards**: Visa, Mastercard, Meeza
- **Mobile Wallets**: Vodafone Cash, Orange Money, Etisalat Cash
- **Bank Installments**: Available for amounts > 1000 EGP

### Payment Status Flow

```
Pending → Processing → Completed
                    ↘ Failed
                    ↘ Refunded
```

---

## Email Service

ShurYan sends automated emails for various events using **SMTP**.

### Email Templates

| Template | Trigger | Recipients |
|----------|---------|------------|
| **Welcome Email** | User registration | New user |
| **Email Verification** | Registration | New user |
| **Password Reset** | Forgot password request | User |
| **Appointment Confirmation** | Appointment booked | Patient, Doctor |
| **Appointment Reminder** | 24h before appointment | Patient |
| **Prescription Ready** | Pharmacy confirms | Patient |
| **Lab Results Ready** | Lab uploads results | Patient |
| **Payment Receipt** | Payment completed | Patient |
| **Verification Approved** | Doctor verified | Doctor |

### Email Configuration

Emails are sent via SMTP (Gmail/SendGrid):

```json
{
  "EmailSettings": {
    "SmtpServer": "smtp.gmail.com",
    "SmtpPort": 587,
    "SenderEmail": "noreply@shuryan.com",
    "SenderName": "ShurYan Healthcare"
  }
}
```

---

## AI Chat Integration (Gemini AI)

ShurYan integrates **Google Gemini AI** for intelligent medical assistance.

### AI Features

1. **Medical Q&A**: Answer general medical questions
2. **Symptom Analysis**: Help identify potential conditions
3. **Drug Information**: Provide medication details
4. **Health Tips**: General wellness advice

### AI Safety Measures

✅ **Disclaimer**: All AI responses include medical disclaimer  
✅ **Not a Diagnosis**: AI cannot replace professional medical advice  
✅ **Data Privacy**: Conversations are encrypted and stored securely  
✅ **Content Filtering**: Inappropriate content is filtered  

### AI Prompt Engineering

The system uses carefully crafted prompts to ensure:
- Accurate medical information
- Appropriate disclaimers
- Professional tone
- Arabic/English language support

---

## Data Validation (FluentValidation)

All API requests are validated using **FluentValidation** rules.

### Validation Examples

#### Register Patient Validation

```csharp
public class RegisterPatientValidator : AbstractValidator<RegisterPatientRequest>
{
    public RegisterPatientValidator()
    {
        RuleFor(x => x.Email)
            .NotEmpty().WithMessage("Email is required")
            .EmailAddress().WithMessage("Invalid email format");
        
        RuleFor(x => x.Password)
            .NotEmpty()
            .MinimumLength(8)
            .Matches(@"[A-Z]").WithMessage("Password must contain uppercase")
            .Matches(@"[a-z]").WithMessage("Password must contain lowercase")
            .Matches(@"[0-9]").WithMessage("Password must contain number");
        
        RuleFor(x => x.PhoneNumber)
            .NotEmpty()
            .Matches(@"^\+20[0-9]{10}$").WithMessage("Invalid Egyptian phone number");
        
        RuleFor(x => x.DateOfBirth)
            .NotEmpty()
            .LessThan(DateTime.Now.AddYears(-18))
            .WithMessage("Patient must be at least 18 years old");
    }
}
```

### Validation Error Response

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    "Email is required",
    "Password must contain uppercase",
    "Invalid Egyptian phone number"
  ],
  "statusCode": 400
}
```

---

## AutoMapper Profiles

ShurYan uses **AutoMapper** for object-to-object mapping between entities and DTOs.

### Mapping Example

```csharp
public class MappingProfile : Profile
{
    public MappingProfile()
    {
        // Doctor mappings
        CreateMap<Doctor, DoctorProfileResponse>()
            .ForMember(dest => dest.FullName, 
                opt => opt.MapFrom(src => $"{src.FirstName} {src.LastName}"))
            .ForMember(dest => dest.ClinicCount, 
                opt => opt.MapFrom(src => src.Clinics.Count));
        
        // Appointment mappings
        CreateMap<Appointment, AppointmentResponse>()
            .ForMember(dest => dest.DoctorName, 
                opt => opt.MapFrom(src => src.Doctor.User.FullName))
            .ForMember(dest => dest.PatientName, 
                opt => opt.MapFrom(src => src.Patient.User.FullName));
    }
}
```

---

## Repository Pattern & Unit of Work

ShurYan implements the **Repository Pattern** with **Unit of Work** for data access.

### Repository Interface Example

```csharp
public interface IDoctorRepository
{
    Task<Doctor?> GetByIdAsync(Guid id);
    Task<Doctor?> GetByEmailAsync(string email);
    Task<IEnumerable<Doctor>> GetAllAsync();
    Task<PaginatedResponse<Doctor>> GetPaginatedAsync(PaginationParams params);
    Task<Doctor> AddAsync(Doctor doctor);
    Task UpdateAsync(Doctor doctor);
    Task DeleteAsync(Guid id);
    Task<bool> ExistsAsync(Guid id);
}
```

### Unit of Work Pattern

```csharp
public interface IUnitOfWork : IDisposable
{
    IDoctorRepository Doctors { get; }
    IPatientRepository Patients { get; }
    IAppointmentRepository Appointments { get; }
    // ... other repositories
    
    Task<int> SaveChangesAsync();
    Task BeginTransactionAsync();
    Task CommitTransactionAsync();
    Task RollbackTransactionAsync();
}
```

### Usage in Service

```csharp
public class AppointmentService : IAppointmentService
{
    private readonly IUnitOfWork _unitOfWork;
    
    public async Task<AppointmentResponse> BookAppointmentAsync(BookAppointmentRequest request)
    {
        await _unitOfWork.BeginTransactionAsync();
        
        try
        {
            var appointment = new Appointment { /* ... */ };
            await _unitOfWork.Appointments.AddAsync(appointment);
            
            var notification = new Notification { /* ... */ };
            await _unitOfWork.Notifications.AddAsync(notification);
            
            await _unitOfWork.SaveChangesAsync();
            await _unitOfWork.CommitTransactionAsync();
            
            return _mapper.Map<AppointmentResponse>(appointment);
        }
        catch
        {
            await _unitOfWork.RollbackTransactionAsync();
            throw;
        }
    }
}
```

---

## Soft Delete Implementation

ShurYan implements **soft delete** for data recovery and audit trails.

### Soft Delete Entity Base

```csharp
public abstract class SoftDeletableEntity : AuditableEntity
{
    public bool IsDeleted { get; set; }
    public DateTime? DeletedAt { get; set; }
    public Guid? DeletedBy { get; set; }
}
```

### Global Query Filter

```csharp
protected override void OnModelCreating(ModelBuilder builder)
{
    builder.Entity<Doctor>()
        .HasQueryFilter(d => !d.IsDeleted);
    
    builder.Entity<Patient>()
        .HasQueryFilter(p => !p.IsDeleted);
}
```

### Restore Functionality

```csharp
public async Task RestorePatientAsync(Guid patientId)
{
    var patient = await _context.Patients
        .IgnoreQueryFilters()
        .FirstOrDefaultAsync(p => p.Id == patientId);
    
    if (patient != null && patient.IsDeleted)
    {
        patient.IsDeleted = false;
        patient.DeletedAt = null;
        patient.DeletedBy = null;
        await _context.SaveChangesAsync();
    }
}
```

---

## Audit Trail

All entities inherit from **AuditableEntity** for automatic audit tracking.

### Auditable Entity

```csharp
public abstract class AuditableEntity
{
    public DateTime CreatedAt { get; set; }
    public Guid? CreatedBy { get; set; }
    public DateTime? UpdatedAt { get; set; }
    public Guid? UpdatedBy { get; set; }
}
```

### Automatic Audit Tracking

```csharp
public override async Task<int> SaveChangesAsync(CancellationToken cancellationToken = default)
{
    var entries = ChangeTracker.Entries<AuditableEntity>();
    
    foreach (var entry in entries)
    {
        if (entry.State == EntityState.Added)
        {
            entry.Entity.CreatedAt = DateTime.UtcNow;
            entry.Entity.CreatedBy = _currentUserId;
        }
        else if (entry.State == EntityState.Modified)
        {
            entry.Entity.UpdatedAt = DateTime.UtcNow;
            entry.Entity.UpdatedBy = _currentUserId;
        }
    }
    
    return await base.SaveChangesAsync(cancellationToken);
}
```

---

## Error Handling & Logging

### Global Error Handling

All exceptions are caught and returned in a consistent format:

```json
{
  "success": false,
  "message": "Error description",
  "errors": ["Detailed error 1", "Detailed error 2"],
  "statusCode": 400
}
```

### HTTP Status Codes

| Code | Meaning | Usage |
|------|---------|-------|
| 200 | OK | Successful GET/PUT/DELETE |
| 201 | Created | Successful POST |
| 400 | Bad Request | Validation errors |
| 401 | Unauthorized | Missing/invalid token |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate resource |
| 500 | Internal Server Error | Unexpected errors |

### Logging Strategy

ShurYan uses ASP.NET Core's built-in logging:

```csharp
_logger.LogInformation("User {UserId} logged in", userId);
_logger.LogWarning("Failed login attempt for {Email}", email);
_logger.LogError(ex, "Error processing payment {PaymentId}", paymentId);
```

**Log Levels:**
- **Trace**: Very detailed debugging
- **Debug**: Development debugging
- **Information**: General flow tracking
- **Warning**: Unexpected but handled events
- **Error**: Errors and exceptions
- **Critical**: System failures

Logs are written to console in development and can be configured for file/cloud logging in production.

---

## Testing

### Test Project Structure

```
Shuryan.Tests/
├── Unit/
│   ├── Services/
│   └── Validators/
└── Integration/
    └── Controllers/
```

### Running Tests

```bash
cd Shuryan.Tests
dotnet test
```

### Test Coverage

Target: **80%+ code coverage** for critical business logic

---

## Deployment Instructions

### Azure App Service Deployment

#### 1. Publish the Application

```bash
cd Shuryan.API
dotnet publish -c Release -o ./publish
```

#### 2. Configure Azure SQL Database

- Create Azure SQL Database
- Update connection string in Azure App Service Configuration

#### 3. Apply Migrations

```bash
dotnet ef database update --connection "your-azure-connection-string"
```

#### 4. Deploy to Azure

```bash
az webapp deployment source config-zip \
  --resource-group ShuryanRG \
  --name shuryan-api \
  --src publish.zip
```

### Docker Deployment

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Shuryan.API/Shuryan.API.csproj", "Shuryan.API/"]
RUN dotnet restore "Shuryan.API/Shuryan.API.csproj"
COPY . .
RUN dotnet build "Shuryan.API/Shuryan.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shuryan.API/Shuryan.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shuryan.API.dll"]
```

---

## Swagger Documentation

Access interactive API documentation at: `https://localhost:7001/swagger`

### Features

- **Try it out**: Test endpoints directly from browser
- **JWT Authentication**: Click "Authorize" button, enter `Bearer <token>`
- **Request/Response Schemas**: Auto-generated from DTOs
- **Dark Theme**: Modern UI with oqo0.SwaggerThemes

---

## Security Best Practices

### Implemented Security Measures

✅ **JWT Token Expiration**: Tokens expire after 24 hours  
✅ **Password Hashing**: BCrypt with salt  
✅ **HTTPS Enforcement**: All production traffic over TLS  
✅ **CORS Policy**: Whitelist allowed origins  
✅ **SQL Injection Prevention**: Parameterized queries via EF Core  
✅ **XSS Protection**: Input sanitization  
✅ **Email Verification**: Prevent fake accounts  
✅ **Role-Based Access**: Principle of least privilege  
✅ **Refresh Token Rotation**: One-time use refresh tokens  
✅ **Sensitive Data Protection**: Secrets in environment variables  

### Recommendations

- Enable rate limiting for login endpoints
- Implement account lockout after failed attempts
- Use Azure Key Vault for production secrets
- Enable Application Insights for monitoring
- Regular security audits and dependency updates

---

## Usage Examples

### Complete User Registration & Login Flow

```javascript
// 1. Register Patient
const registerResponse = await fetch('https://api.shuryan.com/api/Auth/register/patient', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    firstName: 'Ahmed',
    lastName: 'Hassan',
    email: 'ahmed@example.com',
    password: 'SecurePass123!',
    phoneNumber: '+201234567890',
    dateOfBirth: '1990-05-15',
    gender: 'Male'
  })
});

// 2. Verify Email
await fetch('https://api.shuryan.com/api/Auth/verify-email', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    email: 'ahmed@example.com',
    otp: '123456'
  })
});

// 3. Login
const loginResponse = await fetch('https://api.shuryan.com/api/Auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    email: 'ahmed@example.com',
    password: 'SecurePass123!'
  })
});

const { token } = await loginResponse.json();

// 4. Access Protected Endpoint
const profileResponse = await fetch('https://api.shuryan.com/api/Patients/current', {
  headers: { 'Authorization': `Bearer ${token}` }
});
```

---

## Contributing Guidelines

We welcome contributions! Please follow these guidelines:

### Code Style

- Follow C# coding conventions
- Use meaningful variable/method names
- Add XML documentation comments for public APIs
- Keep methods focused and concise

### Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Commit Message Format

```
type(scope): subject

body

footer
```

**Types**: feat, fix, docs, style, refactor, test, chore

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](../LICENSE) file for details.

---

**Developed with ❤️ for DEPI Graduation Project 2025**
