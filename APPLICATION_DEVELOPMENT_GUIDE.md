# 🚗 Mana Prayanam - Complete Development Guide

**Date:** February 16, 2026  
**Version:** 2.0  
**Status:** Production Ready

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [Project Architecture](#project-architecture)
4. [Directory Structure](#directory-structure)
5. [Setup & Installation](#setup--installation)
6. [Running the Application](#running-the-application)
7. [Authentication & Login/Register Flows](#authentication--loginregister-flows)
8. [Features Overview](#features-overview)
9. [API Documentation](#api-documentation)
10. [Database Models](#database-models)
11. [Development Modes](#development-modes)
12. [Mobile App Details](#mobile-app-details)
13. [Authentication & Security](#authentication--security)
14. [Development Workflow](#development-workflow)
15. [Deployment Guide](#deployment-guide)
16. [GitHub Branch Management](#github-branch-management)
17. [Troubleshooting](#troubleshooting)
18. [Additional Resources](#additional-resources)

---

## 📱 Project Overview

**Mana Prayanam** is a full-stack ride-sharing web application designed for employees to share rides with colleagues going to the same office or direction.

### Core Objectives
- ✅ Conserve natural resources
- ✅ Reduce fuel consumption
- ✅ Minimize environmental pollution
- ✅ Build community among employees
- ✅ Share transportation costs
- ✅ Track environmental impact

### Key Statistics
- **Languages:** JavaScript (Frontend + Backend)
- **Database:** MongoDB Atlas Cloud
- **Real-time:** Socket.io for messaging & notifications
- **Payment:** Razorpay Integration
- **Platforms:** Web (React) + Mobile (React Native Expo)

---

## 🛠️ Technology Stack

### **Frontend - Web (React)**
| Technology | Purpose | Version |
|------------|---------|---------|
| React | UI Framework | 18.x |
| React Router | Navigation & Routing | Latest |
| Axios | HTTP Client | 1.x |
| CSS3 | Styling | - |
| React Icons | Icon Library | Latest |
| Socket.io Client | Real-time Chat | 4.7.x |

### **Frontend - Mobile (React Native)**
| Technology | Purpose | Version |
|------------|---------|---------|
| Expo CLI | Development Framework | Latest |
| React Native | Mobile Framework | Latest |
| React Navigation | Mobile Routing | Latest |
| Socket.io Client | Real-time Chat | 4.7.x |

### **Backend - Node.js**
| Technology | Purpose | Version |
|------------|---------|---------|
| Node.js | Runtime | 14+ |
| Express.js | Web Framework | 4.18.x |
| MongoDB | Database | Cloud Atlas |
| Mongoose | ODM | 7.5.x |
| JWT | Authentication | 9.0.x |
| bcryptjs | Password Hashing | 2.4.x |
| Socket.io | Real-time Server | 4.7.x |
| express-validator | Input Validation | 7.0.x |
| Google OAuth Library | Third-party Auth | 10.5.x |
| CORS | Cross-Origin Handling | 2.8.x |

### **Database**
- **MongoDB Atlas** - Cloud-hosted NoSQL database
- **Connection:** `mongodb+srv://kp9959060606_db_user:A3YFrnjoL6KLFvey@clusterrat.g2a6o7e.mongodb.net/ride-share-db`

### **External Services**
- **Razorpay** - Payment Gateway
- **Google OAuth** - Third-party Authentication
- **Fast2SMS** - OTP & SMS Service (Free tier)

---

## 🏗️ Project Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                              │
├──────────────────────┬──────────────────────────────────────┤
│  Web (React)         │  Mobile (React Native Expo)          │
│  - Dashboard         │  - DashboardScreen                   │
│  - Find Ride         │  - FindRideScreen                    │
│  - Offer Ride        │  - OfferRideScreen                   │
│  - Profiles          │  - User Profiles                     │
│  - Messages          │  - Messaging Integration             │
└──────────────────────┴──────────────────────────────────────┘
                            ↓ (Axios + Socket.io)
┌─────────────────────────────────────────────────────────────┐
│                    API LAYER (Express.js)                    │
├─────────────────────────────────────────────────────────────┤
│  ✓ Authentication    ✓ Rides         ✓ Real-time            │
│  ✓ User Management   ✓ Ratings       ✓ Notifications        │
│  ✓ Payments          ✓ Messaging     ✓ Health Check         │
└─────────────────────────────────────────────────────────────┘
                    ↓ (Mongoose ODM)
┌─────────────────────────────────────────────────────────────┐
│              DATABASE LAYER (MongoDB)                        │
├─────────────────────────────────────────────────────────────┤
│  Collections:                                                │
│  - Users (Profiles, Auth, Preferences)                      │
│  - Rides (Posted rides, Status, Location)                  │
│  - Ratings (Star ratings, Reviews)                         │
│  - Messages (User Conversations)                           │
│  - Notifications (Real-time alerts)                        │
│  - Payments (Transaction History)                          │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Directory Structure

```
./Man Prayanam RAT/
│
├── ride-share-app/                    # Main Web Application
│   ├── backend/
│   │   ├── models/
│   │   │   ├── User.js               # User schema & auth
│   │   │   ├── Ride.js               # Ride posting & search
│   │   │   ├── Rating.js             # Ratings & reviews
│   │   │   ├── Message.js            # Real-time messaging
│   │   │   ├── Payment.js            # Payment transactions
│   │   │   ├── Notification.js       # Real-time alerts
│   │   │
│   │   ├── routes/
│   │   │   ├── auth.js               # Auth endpoints (login, register, OTP)
│   │   │   ├── rides.js              # Ride operations (create, search, book)
│   │   │   ├── ratings.js            # Rating endpoints
│   │   │   ├── messages.js           # Messaging endpoints
│   │   │   ├── payments.js           # Payment processing
│   │   │   ├── users.js              # User management
│   │   │   ├── notifications.js      # Notification endpoints
│   │   │
│   │   ├── middleware/
│   │   │   └── auth.js               # JWT verification middleware
│   │   │
│   │   ├── server.js                 # Express app & Socket.io setup
│   │   ├── .env                      # Environment variables
│   │   ├── package.json              # Backend dependencies
│   │   └── node_modules/             # Installed packages
│   │
│   ├── frontend/
│   │   ├── public/
│   │   │   └── index.html            # Single page application root
│   │   │
│   │   ├── src/
│   │   │   ├── components/
│   │   │   │   ├── Navbar.js         # Navigation bar
│   │   │   │   ├── MapView.js        # Google Maps integration
│   │   │   │   ├── Payment.js        # Payment component (Razorpay)
│   │   │   │   ├── Ratings.js        # Ratings component
│   │   │   │   ├── Messaging.js      # Real-time chat
│   │   │   │   ├── NotificationBell.js # Notifications
│   │   │   │   ├── CityAutocomplete.js # City search
│   │   │   │   └── AreaAutocomplete.js # Area search
│   │   │   │
│   │   │   ├── pages/
│   │   │   │   ├── Login.js          # Login page
│   │   │   │   ├── Register.js       # Registration page
│   │   │   │   ├── Dashboard.js      # Home dashboard
│   │   │   │   ├── FindRide.js       # Search & book rides
│   │   │   │   ├── OfferRide.js      # Post new ride
│   │   │   │   ├── MyRides.js        # User's rides history
│   │   │   │   ├── RideDetails.js    # Ride information page
│   │   │   │   └── Profile.js        # User profile management
│   │   │   │
│   │   │   ├── styles/
│   │   │   │   ├── index.css         # Global styles
│   │   │   │   ├── App.css           # App container styles
│   │   │   │   ├── Login.css         # Auth pages styling
│   │   │   │   ├── Dashboard.css     # Dashboard styling
│   │   │   │   ├── FindRide.css      # Search page styling
│   │   │   │   ├── OfferRide.css     # Post ride styling
│   │   │   │   ├── Navbar.css        # Navigation styling
│   │   │   │   └── [other styles]
│   │   │   │
│   │   │   ├── data/
│   │   │   │   └── cityAreas.js      # City & area database
│   │   │   │
│   │   │   ├── config.js             # API configuration
│   │   │   ├── App.js                # Main app component
│   │   │   └── index.js              # React entry point
│   │   │
│   │   ├── package.json              # Frontend dependencies
│   │   └── node_modules/             # Installed packages
│   │
│   ├── QUICKSTART.md                 # Quick setup guide
│   ├── README.md                     # Project readme
│   ├── setup.bat, setup.ps1          # Windows setup scripts
│   ├── setup.sh                      # Linux/Mac setup script
│   ├── start-app.bat, start-app.ps1  # Windows start scripts
│   ├── start-app.sh                  # Linux/Mac start script
│   └── COMPLETE-SETUP.ps1            # Complete PowerShell setup
│
├── ride-share-mobile/                 # Mobile Application (React Native)
│   ├── app/
│   │   ├── (tabs)/
│   │   │   ├── index.tsx             # Home screen
│   │   │   └── explore.tsx           # Explore rides
│   │   ├── _layout.tsx               # App layout
│   │   └── modal.tsx                 # Modal component
│   │
│   ├── src/
│   │   ├── components/               # Shared components
│   │   ├── screens/
│   │   │   ├── LoginScreen.js        # Mobile login
│   │   │   ├── DashboardScreen.js    # Mobile dashboard
│   │   │   ├── FindRideScreen.js     # Find rides
│   │   │   ├── OfferRideScreen.js    # Offer rides
│   │   │   ├── PaymentScreen.js      # Payment processing
│   │   │   ├── RatingsScreen.js      # Rate drivers
│   │   │   └── MessagingScreen.js    # Real-time chat
│   │   └── styles/                   # Mobile styles
│   │
│   ├── assets/images/                # Mobile app images
│   ├── App.js                        # Mobile app entry
│   ├── app.json                      # Expo configuration
│   ├── package.json                  # Mobile dependencies
│   ├── SETUP_INSTRUCTIONS.md         # Mobile setup
│   ├── PRODUCTION_BUILD_GUIDE.md     # Mobile build guide
│   └── setup.bat, setup.sh           # Mobile setup scripts
│
├── COMPLETE_SETUP.md                 # Complete setup documentation
├── FEATURES_SUMMARY.md               # Features overview
├── LOGIN_REGISTER_FLOW.md            # Auth flow documentation
├── MOBILE_APP_UPDATE_SUMMARY.md      # Mobile app updates
├── MOBILE_OTP_GUIDE.md               # OTP implementation guide
├── RIDE_CREATION_FIX.md              # Bug fixes documentation
├── QUICK_REFERENCE.md                # Quick reference guide
└── INDEX.md                          # Project index
```

---

## 🚀 Setup & Installation

### Prerequisites

**Before starting, ensure you have:**
- Node.js (v14 or higher) - [Download](https://nodejs.org/)
- npm or yarn - Comes with Node.js
- MongoDB Account - [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- Git - [Download](https://git-scm.com/)
- Code Editor - VS Code recommended

### Step 1: Clone the Repository

```bash
# Using HTTPS
git clone https://github.com/Tkrishnaprasad/Mana-Prayanam.git

# OR using SSH
git clone git@github.com:Tkrishnaprasad/Mana-Prayanam.git

# Navigate to project
cd "Man Prayanam RAT"
```

### Step 2: Setup Backend

```bash
# Navigate to backend directory
cd ride-share-app/backend

# Install dependencies
npm install

# Create .env file with configuration
cat > .env << EOF
# Database
MONGODB_URI=mongodb+srv://kp9959060606_db_user:A3YFrnjoL6KLFvey@clusterrat.g2a6o7e.mongodb.net/ride-share-db?retryWrites=true&w=majority

# JWT Secret
JWT_SECRET=mana-prayanam-rat-secret-2024

# Server Configuration
PORT=5000
NODE_ENV=production

# Google OAuth (Optional)
GOOGLE_CLIENT_ID=YOUR_GOOGLE_CLIENT_ID

# SMS Service (Optional)
FAST2SMS_API_KEY=YOUR_FAST2SMS_API_KEY

# Payment Gateway (Optional)
RAZORPAY_KEY_ID=YOUR_RAZORPAY_KEY
RAZORPAY_KEY_SECRET=YOUR_RAZORPAY_SECRET
EOF
```

### Step 3: Setup Frontend

```bash
# Navigate to frontend directory
cd ../frontend

# Install dependencies
npm install

# Create .env file
cat > .env << EOF
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_SOCKET_URL=http://localhost:5000
SESSION_STORAGE_KEY=ride-share-session
EOF
```

### Step 4: Setup Mobile App (Optional)

```bash
# Navigate to mobile directory
cd ../../ride-share-mobile

# Install dependencies
npm install

# Install Expo CLI globally (if not already installed)
npm install -g expo-cli

# Create .env file
cat > .env << EOF
EXPO_PUBLIC_API_URL=http://your-machine-ip:5000/api
EXPO_PUBLIC_SOCKET_URL=http://your-machine-ip:5000
EOF
```

---

## ▶️ Running the Application

### **Windows Users (PowerShell)**

#### Option 1: Run All Services (Backend + Frontend)

```powershell
# From root directory (Man Prayanam RAT)
cd "ride-share-app"

# Using the setup script
.\start-app.ps1
```

#### Option 2: Run Services Manually

**Terminal 1 - Backend:**
```powershell
cd ride-share-app\backend
npm start
# Output: 🚀 Server running on port 5000
```

**Terminal 2 - Frontend:**
```powershell
cd ride-share-app\frontend
npm start
# Opens: http://localhost:3000
```

#### Option 3: Development Mode with Hot Reload

**Terminal 1 - Backend:**
```powershell
cd ride-share-app\backend
npm run dev  # Uses nodemon for auto-restart
```

**Terminal 2 - Frontend:**
```powershell
cd ride-share-app\frontend
npm start
```

### **Linux/Mac Users (Bash)**

```bash
# From root directory
cd "ride-share-app"

# Make scripts executable
chmod +x start-app.sh

# Run all services
./start-app.sh
```

### **Mobile App (Expo)**

```bash
cd ride-share-mobile

# Start Expo development server
expo start

# Press:
# 'w' - Open in web browser
# 'i' - Open in iOS simulator
# 'a' - Open in Android emulator
```

### Verification

After starting services, verify they're running:

**Backend Health Check:**
```bash
curl http://localhost:5000/api/health
# Expected response: {"status":"Server is running","socketConnections":0}
```

**Frontend:**
- Open browser: `http://localhost:3000`
- Should see login page

---

## 🔐 Authentication & Login/Register Flows

### Architecture Overview
The application has **separated login and registration concerns** into dedicated pages for better UX and code maintainability.

### Web Frontend Authentication (React)

#### **Login Page** (`frontend/src/pages/Login.js`)
**Two Authentication Methods Available:**

1. **Gmail OAuth Login**
   - Uses Google Identity Services (free)
   - Single-click authentication
   - No password storage required
   - Instant account creation if first-time user

2. **Email & Password Login**
   - Traditional email/password authentication
   - Secure password hashing with bcryptjs
   - JWT token generation
   - Error messages for invalid credentials

**UI Layout:**
```
┌──────────────────────────────────────┐
│  Left Panel (Green #27ae60)          │
│  - Branding: "Mana Prayanam"         │
│  - Description & Features            │
│  ├─────────────────────────────────┐ │
│  │ Right Panel                     │ │
│  │ - Title: "Welcome Back"         │ │
│  │ - [Gmail Login Button]          │ │
│  │ - Email Input Field             │ │
│  │ - Password Input Field          │ │
│  │ - [Login Button]                │ │
│  │ - "New? Create Account >>" Link │ │
│  └─────────────────────────────────┘ │
└──────────────────────────────────────┘
```

**Key Features:**
- ✅ Real-time form validation
- ✅ Loading states
- ✅ Error/success messaging
- ✅ Responsive design (desktop & tablet)
- ✅ Navigation to register page

#### **Registration Page** (`frontend/src/pages/Register.js`)
**Three Registration Methods Available:**

**Tab 1: Gmail OAuth** 🔍
```
One-click registration with Google
↓
Auto-creates account
↓
User can add vehicle details later
```

**Tab 2: Email & Password** 📧
```
Form Fields:
├─ Full Name
├─ Email
├─ Password
├─ Phone Number
├─ Company (optional)
└─ Vehicle Details (for drivers)
```

**Tab 3: Phone OTP** 📱
```
Step-by-Step:
1. Enter 10-digit phone number
2. Click "Send OTP"
3. Receive 6-digit code via SMS
4. Enter OTP in form
5. Account created automatically

Timer: 5-minute countdown
Max Attempts: 3 tries
```

**Registration Method Selector UI:**
```
When choosing signup method:
┌─ Registration Method ──────────────┐
│ ┌──────────┐  ┌──────────┐        │
│ │ 📧 Email │  │ 📱 OTP   │        │
│ └──────────┘  └──────────┘        │
│                                   │
│ Selected form appears:            │
│ [Form fields for chosen method]   │
└───────────────────────────────────┘
```

### Mobile App Authentication (React Native)

**Same methods available:**
- Gmail OAuth
- Email & Password
- Phone OTP

**Mobile-Specific Implementation:**
```
export const LoginScreen = () => {
  const [loginMode, setLoginMode] = useState('email'); // or 'otp'
  const [phone, setPhone] = useState('');
  const [otp, setOtp] = useState('');
  const [otpTimer, setOtpTimer] = useState(0);
  
  // OTP countdown effect
  useEffect(() => {
    if (otpTimer > 0) {
      const interval = setInterval(() => setOtpTimer(t => t - 1), 1000);
      return () => clearInterval(interval);
    }
  }, [otpTimer]);
  
  const handleSendOTP = async () => {
    // Call backend OTP endpoint
    // Start 5-minute timer
    setOtpTimer(300); // 5 minutes
  };
}
```

### Backend Authentication Flow

**Location:** `backend/routes/auth.js`  
**Key Services:**
- OTP Generation & Verification
- SMS Integration (Fast2SMS - Free tier)
- JWT Token Creation
- Password Hashing
- Google OAuth Validation

#### OTP Implementation Details

```javascript
// OTP Configuration
const OTP_EXPIRY_MS = 5 * 60 * 1000;      // 5 minutes
const MAX_OTP_ATTEMPTS = 3;               // 3 wrong tries allowed

// OTP Generation
function generateOTP() {
  return Math.floor(100000 + Math.random() * 900000).toString(); // 6-digit
}

// Cleanup Expired OTPs
function cleanExpiredOTPs() {
  const now = Date.now();
  for (const [phone, data] of otpStore.entries()) {
    if (now > data.expiresAt) otpStore.delete(phone);
  }
}
```

#### SMS Service (Free Tier)

**Provider:** Fast2SMS  
**Free Tier Features:**
- Free credits on signup
- OTP route is cheapest
- Works for Indian numbers (+91)
- API Key: Add to `.env` file

**Setup:**
```bash
1. Visit https://www.fast2sms.com
2. Sign up for free account
3. Copy your API key
4. Add to .env:
   FAST2SMS_API_KEY=your_api_key_here
```

**Development Mode:**
If no API key configured, OTP prints to console:
```
📱 [DEV MODE] OTP for +91 9876543210: 123456 (valid 5 min)
ℹ️  To send real SMS, sign up at https://www.fast2sms.com
```

### Authentication Flow Diagram

```
USER FLOW:

Login Flow:
  User Visits App
    ↓
  Choose: Gmail | Email+Password
    ↓
  Credentials Sent to Backend
    ↓
  Backend Validates & Creates JWT
    ↓
  Token Stored in localStorage
    ↓
  User Redirected to Dashboard


Registration Flow:
  User Clicks "Create Account"
    ↓
  Choose Method: Gmail | Email | OTP
    ↓
  If Gmail:
    Google OAuth Validation → Account Created
  If Email:
    Email+Password Form → Validation → Account Created
  If OTP:
    Phone Number → Send OTP → Verify OTP → Account Created
    ↓
  JWT Token Generated
    ↓
  User Logged In Automatically
    ↓
  Redirected to Profile Setup
```

### Token Management

```javascript
// JWT Token Structure
const token = jwt.sign(
  { 
    userId: user._id,
    email: user.email,
    role: user.role 
  },
  process.env.JWT_SECRET,
  { expiresIn: '30d' }  // 30-day expiration
);

// Every request header
Authorization: Bearer <token>

// Token Validation Middleware
function verifyToken(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'No token' });
  
  jwt.verify(token, process.env.JWT_SECRET, (err, decoded) => {
    if (err) return res.status(401).json({ error: 'Invalid token' });
    req.userId = decoded.userId;
    next();
  });
}
```

**Detailed Documentation:**
- See [LOGIN_REGISTER_FLOW.md](LOGIN_REGISTER_FLOW.md) for UX design decisions
- See [MOBILE_OTP_GUIDE.md](MOBILE_OTP_GUIDE.md) for OTP implementation details

---

## ✨ Features Overview

### 1. **User Authentication** 🔐
- Email/Password registration and login
- JWT token-based authentication
- Google OAuth integration
- OTP verification via SMS
- Secure password hashing with bcryptjs

### 2. **Ride Management** 🚗
- **Post Rides:** Drivers can post available rides with:
  - Route details (from & to locations)
  - Available seats
  - Departure time
  - Cost per seat
  - Vehicle information

- **Search & Book:** Passengers can:
  - Search rides by location and date
  - View ride details and driver profile
  - Book available seats
  - Cancel bookings

### 3. **User Profiles** 👤
- Personal information management
- Vehicle details (drivers)
- Profile verification
- Contact information
- Preferences
- Profile image upload (base64 or URL)

**Sample Profile Data:**
```json
{
  "name": "Rajesh Kumar",
  "email": "rajesh@company.com",
  "phone": "9876543210",
  "bio": "Friendly driver, non-smoking ride",
  "vehicle": {
    "number": "MH01AB1234",
    "model": "Honda Civic",
    "color": "Silver",
    "capacity": 4
  },
  "address": {
    "street": "123 Main St",
    "city": "Bangalore",
    "state": "Karnataka"
  },
  "preferences": {
    "smokingAllowed": false,
    "musicAllowed": true,
    "petsAllowed": false
  },
  "rating": {
    "average": 4.8,
    "totalRatings": 45
  }
}
```

### 4. **Real-Time Messaging** 💬
- Socket.io powered instant messaging
- User-to-user conversations
- Typing indicators
- Message history
- Online/offline status

### 5. **Ratings & Reviews** ⭐
- 5-star rating system
- Detailed written reviews (up to 500 characters)
- Rating categories:
  - Driving behavior
  - Vehicle cleanliness
  - Safety
  - Communication
- Automatic driver rating calculation

### 6. **Payment Integration** 💳
- **Payment Methods:**
  - Razorpay integration (credit/debit cards)
  - Wallet system (in-app balance)
  - Cash payment option
  
- **Features:**
  - Order creation and verification
  - Payment history
  - Transaction status tracking
  - Receipt generation

### 7. **Notifications** 🔔
- Real-time notifications for:
  - Ride updates
  - Booking confirmations
  - Payment receipts
  - New messages
  - Rating requests
  
- Push notifications (web & mobile)

### 8. **Environmental Impact Tracking** 🌱
- Track fuel saved
- Calculate carbon footprint reduction
- Community contribution statistics
- Environmental dashboard

---

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

#### Register User
```http
POST /auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "9876543210",
  "password": "securePassword123",
  "role": "passenger"  // or "driver"
}

Response: 
{
  "message": "Registration successful",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": { /* user object */ }
}
```

#### Login User
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securePassword123"
}

Response:
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": { /* user object */ }
}
```

#### Request OTP
```http
POST /auth/request-otp
Content-Type: application/json

{
  "phone": "9876543210"
}

Response:
{
  "message": "OTP sent successfully",
  "expiresIn": 300  // seconds
}
```

#### Verify OTP
```http
POST /auth/verify-otp
Content-Type: application/json

{
  "phone": "9876543210",
  "otp": "123456"
}

Response:
{
  "message": "OTP verified",
  "user": { /* user object */ }
}
```

### Rides Endpoints

#### Create Ride
```http
POST /rides
Authorization: Bearer {token}
Content-Type: application/json

{
  "from": "Mumbai Central",
  "to": "Powai IT Park",
  "departureTime": "2024-02-20T08:00:00Z",
  "availableSeats": 3,
  "costPerSeat": 50,
  "vehicleNumber": "MH01AB1234",
  "vehicleModel": "Honda Civic",
  "notes": "Non-smoking ride"
}

Response:
{
  "message": "Ride created successfully",
  "ride": { /* ride object */ }
}
```

#### Search Rides
```http
GET /rides/search?from=Mumbai&to=Powai&date=2024-02-20
Authorization: Bearer {token}

Response:
{
  "rides": [ /* array of ride objects */ ]
}
```

#### Book Ride
```http
POST /rides/:rideId/book
Authorization: Bearer {token}
Content-Type: application/json

{
  "seatsRequired": 1,
  "specialRequests": "Need window seat"
}

Response:
{
  "message": "Booking successful",
  "booking": { /* booking object */ }
}
```

#### Get My Rides
```http
GET /rides/my-rides
Authorization: Bearer {token}

Response:
{
  "rides": [ /* user's ride listings */ ]
}
```

### Ratings Endpoints

#### Add Rating
```http
POST /ratings/add
Authorization: Bearer {token}
Content-Type: application/json

{
  "rideId": "ride_123",
  "driverId": "driver_456",
  "rating": 5,
  "review": "Great driver, clean car, safe ride!",
  "categories": {
    "behavior": 5,
    "cleanliness": 5,
    "safety": 5,
    "communication": 4
  }
}

Response:
{
  "message": "Rating added successfully",
  "rating": { /* rating object */ }
}
```

#### Get User Ratings
```http
GET /ratings/user/:userId
Authorization: Bearer {token}

Response:
{
  "ratings": [ /* array of ratings */ ],
  "average": 4.8,
  "totalRatings": 45
}
```

### Messaging Endpoints

#### Send Message
```http
POST /messages/send
Authorization: Bearer {token}
Content-Type: application/json

{
  "recipientId": "user_456",
  "message": "Hi, I'm interested in your ride!",
  "rideId": "ride_123"
}

Response:
{
  "message": "Message sent",
  "messageObject": { /* message doc */ }
}
```

#### Get Conversations
```http
GET /messages/conversations
Authorization: Bearer {token}

Response:
{
  "conversations": [ /* list of conversations */ ]
}
```

#### Get Message History
```http
GET /messages/history/:userId
Authorization: Bearer {token}

Response:
{
  "messages": [ /* message history */ ]
}
```

### Payment Endpoints

#### Create Payment Order
```http
POST /payments/create-order
Authorization: Bearer {token}
Content-Type: application/json

{
  "rideId": "ride_123",
  "amount": 150,
  "method": "razorpay"  // or "wallet", "cash"
}

Response:
{
  "orderId": "order_123",
  "amount": 15000,  // in smallest unit (paise)
  "currency": "INR",
  "key": "razorpay_key_id"
}
```

#### Verify Payment
```http
POST /payments/verify
Authorization: Bearer {token}
Content-Type: application/json

{
  "orderId": "order_123",
  "paymentId": "pay_123",
  "signature": "signature_hash"
}

Response:
{
  "message": "Payment verified",
  "status": "completed"
}
```

#### Get Payment History
```http
GET /payments/history
Authorization: Bearer {token}

Response:
{
  "payments": [ /* payment records */ ]
}
```

### User Endpoints

#### Get User Profile
```http
GET /users/profile
Authorization: Bearer {token}

Response:
{
  "user": { /* complete user object */ }
}
```

#### Update Profile
```http
PUT /users/profile
Authorization: Bearer {token}
Content-Type: application/json

{
  "name": "John Doe",
  "phone": "9876543210",
  "bio": "Friendly driver",
  "profileImage": "base64_string"
}

Response:
{
  "message": "Profile updated",
  "user": { /* updated user object */ }
}
```

### Notifications Endpoints

#### Get Notifications
```http
GET /notifications
Authorization: Bearer {token}

Response:
{
  "notifications": [ /* user notifications */ ]
}
```

#### Mark as Read
```http
PUT /notifications/:notificationId/read
Authorization: Bearer {token}

Response:
{
  "message": "Marked as read"
}
```

---

## 🗄️ Database Models

### User Schema
```javascript
{
  _id: ObjectId,
  name: String,
  email: String (unique),
  phone: String (unique),
  password: String (hashed),
  role: String ("passenger" or "driver"),
  profileImage: String (base64 or URL),
  bio: String,
  isVerified: Boolean,
  rating: {
    average: Number,
    totalRatings: Number
  },
  vehicle: {  // Only for drivers
    number: String,
    model: String,
    color: String,
    capacity: Number
  },
  address: {
    street: String,
    city: String,
    state: String,
    postalCode: String
  },
  preferences: {
    smokingAllowed: Boolean,
    musicAllowed: Boolean,
    petsAllowed: Boolean
  },
  createdAt: Date,
  updatedAt: Date
}
```

### Ride Schema
```javascript
{
  _id: ObjectId,
  driverId: ObjectId (ref: User),
  from: String,
  to: String,
  departureTime: DateTime,
  availableSeats: Number,
  bookedSeats: Number,
  costPerSeat: Number,
  vehicleNumber: String,
  vehicleModel: String,
  description: String,
  status: String ("scheduled", "ongoing", "completed", "cancelled"),
  passengers: [
    {
      passengerId: ObjectId,
      seatsBooked: Number,
      status: String ("confirmed", "completed", "cancelled"),
      bookingTime: Date
    }
  ],
  rating: {
    averageRating: Number,
    totalRatings: Number
  },
  createdAt: Date,
  updatedAt: Date
}
```

### Rating Schema
```javascript
{
  _id: ObjectId,
  rideId: ObjectId (ref: Ride),
  driverId: ObjectId (ref: User),
  passengerId: ObjectId (ref: User),
  rating: Number (1-5),
  review: String,
  categories: {
    behavior: Number,
    cleanliness: Number,
    safety: Number,
    communication: Number
  },
  createdAt: Date
}
```

### Message Schema
```javascript
{
  _id: ObjectId,
  senderId: ObjectId (ref: User),
  recipientId: ObjectId (ref: User),
  rideId: ObjectId (ref: Ride),
  content: String,
  isRead: Boolean,
  readAt: Date,
  createdAt: Date
}
```

### Payment Schema
```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User),
  rideId: ObjectId (ref: Ride),
  amount: Number,
  currency: String,
  method: String ("razorpay", "wallet", "cash"),
  status: String ("pending", "completed", "failed", "cancelled"),
  orderId: String,
  paymentId: String,
  signature: String,
  description: String,
  createdAt: Date,
  updatedAt: Date
}
```

### Notification Schema
```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User),
  type: String ("booking", "message", "rating", "payment"),
  title: String,
  description: String,
  relatedId: ObjectId,
  isRead: Boolean,
  readAt: Date,
  createdAt: Date
}
```

---

## �️ Development Modes

### Demo Mode (No Database Required)

The application can run in **Demo Mode** without MongoDB, allowing you to test all features instantly.

**When to Use Demo Mode:**
- ✅ Initial setup and testing
- ✅ Building features before database is ready
- ✅ Demonstrating features to stakeholders
- ✅ Developing on systems without MongoDB access
- ✅ Learning and exploration

### How Demo Mode Works

**Activation:**
```bash
# Set in .env file
NODE_ENV=development

# Or automatically for development environments
```

**Affected Endpoints:**

#### 1. Authentication
```javascript
// Demo account (always works)
Email: test@example.com
Password: Test@123

// Any new registration creates mock user
// No error messages, everything succeeds
```

#### 2. Ride Operations
```javascript
// Create Ride (POST /api/rides/create)
Returns mock ride with auto-generated ID:
{
  _id: "mock_ride_" + timestamp,
  departure: "User Input",
  destination: "User Input",
  date: "User Input",
  departureTime: "User Input",
  vehicle: "Hyundai i20",
  totalSeats: 4,
  costPerPerson: 50,
  status: "active",
  driverInfo: { name: "Mock Driver", rating: 4.8 }
}

// Get Available Rides (GET /api/rides/available)
Returns 3 hardcoded mock rides:
1. Rajesh Kumar (Toyota Innova) - Whitefield → MG Road
2. Priya Singh (Maruti Swift) - Marathahalli → Indiranagar
3. Arjun Desai (Hyundai i20) - Indiranagar → Whitefield
```

#### 3. Booking Operations
```javascript
// Book Ride (POST /api/rides/:id/book)
// Decreases available seats, adds passenger
// Returns success message immediately

// Cancel Booking (DELETE /api/rides/:id/cancel)
// Increases available seats, removes passenger
// Returns success immediately
```

#### 4. Payments (Demo)
```javascript
// Create Order without Razorpay validation
{
  orderId: "mock_order_" + timestamp,
  amount: user_input,
  currency: "INR",
  status: "pending"
}

// Verify Payment (accepts any input)
{
  status: "completed",
  message: "Payment verified (mock)"
}
```

#### 5. Messages & Ratings (Demo)
```javascript
// Send Message
Returns success with mock timestamp

// Add Rating
Accepts any rating 1-5
Stores in memory (not persistent)
```

### Database Mode (MongoDB)

**When MongoDB is available:**
```javascript
// NODE_ENV=production
// MONGODB_URI=your_connection_string

// All operations use real database
// Data persists across sessions
// Real-time collaboration possible
```

### Switching Modes

**Development (Demo - No DB):**
```bash
# .env
NODE_ENV=development
```

**Production (With DB):**
```bash
# .env
NODE_ENV=production
MONGODB_URI=mongodb+srv://user:pass@cluster/.../database
MONGODB_URI=mongodb://localhost:27017/ride-share-db
```

### Testing the Demo Mode

**Step 1: Make sure NODE_ENV=development in .env**
```bash
cd ride-share-app/backend
cat .env | grep NODE_ENV
# Output: NODE_ENV=development
```

**Step 2: Start Backend**
```bash
npm start
# Server running on port 5000
```

**Step 3: Login with Demo Credentials**
```
Email: test@example.com
Password: Test@123
```

**Step 4: Test Features**
```
✓ Create new ride
✓ View available rides
✓ Book a ride
✓ Cancel booking
✓ Send message
✓ Add rating
✓ Process payment
```

**All operations work instantly without database!**

### Common Issues in Demo Mode

**Issue: Getting database errors even in demo mode**
```
Solution: Check NODE_ENV=development is set in .env
         Restart backend server after changing .env
```

**Issue: Data not persisting between sessions**
```
Expected behavior in demo mode!
Data is stored in memory only.
Refresh browser → demo data resets.
To persist data: Switch to production mode with MongoDB
```

**Detailed Documentation:**
- See [RIDE_CREATION_FIX.md](RIDE_CREATION_FIX.md) for demo mode troubleshooting

---

## 📱 Mobile App Details

### Setup Instructions

**Prerequisites:**
- Node.js installed
- Expo CLI: `npm install -g expo-cli`
- Expo Go app on mobile device (free from App Store/Play Store)

**Installation:**
```bash
cd ride-share-mobile

# Install dependencies
npm install

# Create .env file
cat > .env << EOF
EXPO_PUBLIC_API_URL=http://your-machine-ip:5000/api
EXPO_PUBLIC_SOCKET_URL=http://your-machine-ip:5000
EOF
```

**Important:** Replace `your-machine-ip` with your computer's IP address (not localhost)
```bash
# Find your IP
# Windows PowerShell
ipconfig | findstr "IPv4"

# macOS/Linux
ifconfig | grep inet
```

### Running Mobile App

```bash
# Start Expo development server
expo start

# Options:
# Press 'w' → Open in web browser
# Press 'i' → Open in iOS simulator (Mac only)
# Press 'a' → Open in Android emulator
# Scan QR code → Open in Expo Go app (physical device)
```

### Mobile Screen Structure

**Available Screens:**
```
├── LoginScreen.js
│   ├── Email/Password Login
│   ├── Gmail OAuth Integration
│   └── Phone OTP Registration
│
├── DashboardScreen.js
│   ├── Available Rides List
│   ├── Quick Actions
│   └── User Stats
│
├── FindRideScreen.js
│   ├── Location Search
│   ├── Date/Time Selection
│   └── Ride Filtering
│
├── OfferRideScreen.js
│   ├── Route Details
│   ├── Seat Management
│   └── Pricing
│
├── PaymentScreen.js
│   ├── Razorpay Integration
│   ├── Wallet System
│   └── Cash Payment Option
│
├── RatingsScreen.js
│   ├── Star Rating (1-5)
│   └── Review Text
│
└── MessagingScreen.js
    ├── Real-time Chat
    └── Message History
```

### Mobile App - OTP Flow

**Step-by-Step Process:**
```
1. User taps "Sign Up with OTP"
   ↓
2. Enters 10-digit phone number
   ↓
3. Taps "Send OTP"
   ↓
4. Receives SMS with 6-digit code
   ↓
5. Enters OTP in masked input
   ↓
6. 5-minute timer countdown visible
   ↓
7. Taps "Verify OTP"
   ↓
8. Account created automatically
   ↓
9. User logged in to dashboard
```

**UI Implementation:**
```javascript
// OTP Input Field
- Masked 6-digit number input
- Only accepts numbers (0-9)
- Character spacing for clarity
- Real-time validation

// Timer Display
- Format: MM:SS (e.g., 04:30)
- Green color (#27ae60) for active
- Disabled after countdown
- "Resend OTP" button appears after timeout
```

### Mobile Production Build

**For Android (APK):**
```bash
npm install -g eas-cli
eas login
eas init
npm install -g @react-native-async-storage/async-storage
eas build --platform android --profile production
```

**For iOS (IPA):**
```bash
eas build --platform ios --profile production
```

**Expected Output:**
- Android: `.apk` file ready for Play Store
- iOS: `.ipa` file ready for App Store

**See [PRODUCTION_BUILD_GUIDE.md](ride-share-mobile/PRODUCTION_BUILD_GUIDE.md) for detailed steps**

### Mobile-Specific Features

**Real-time Updates:**
- Socket.io integration for instant notifications
- Message delivery indicators
- Ride status updates

**Offline Capabilities:**
- AsyncStorage for local caching
- Works without API connection (read-only)
- Auto-sync when online

**Push Notifications:**
- Configured for Expo push service
- Alerts for new messages
- Ride updates

---

## �🔐 Advanced Authentication & Security

### JWT Token Flow

```
1. User Login/Register
        ↓
2. Server creates JWT token
        ↓
3. Token sent to frontend
        ↓
4. Frontend stores in localStorage
        ↓
5. Every request includes token in Authorization header
        ↓
6. Server validates token with middleware
        ↓
7. If valid → Process request
   If invalid → Return 401 Unauthorized
```

### JWT Structure
```
Header.Payload.Signature

Header: { "alg": "HS256", "typ": "JWT" }
Payload: { "userId": "...", "email": "...", "iat": "...", "exp": "..." }
Signature: HMACSHA256(Header.Payload, SECRET_KEY)
```

### Password Security
- Passwords hashed using bcryptjs (10 salt rounds)
- Never stored in plaintext
- Compared using bcrypt.compare()

### Environment Variables Security
- Critical credentials stored in `.env` file
- `.env` added to `.gitignore`
- Never commit sensitive data
- Different configs for development/production

### API Security Features
- CORS enabled for trusted domains
- Input validation on all endpoints
- Rate limiting on auth endpoints
- SQL injection prevention via Mongoose
- XSS prevention in React

---

## 👨‍💻 Development Workflow

### Local Development Setup

1. **Clone Repository**
```bash
git clone https://github.com/Tkrishnaprasad/Mana-Prayanam.git
cd "Man Prayanam RAT"
```

2. **Create Development Branch**
```bash
# Switch to main branch first
git checkout main

# Create your feature branch
git checkout -b feature/your-feature-name
# Example: git checkout -b feature/add-wallet-system
```

3. **Install Dependencies**
```bash
# Backend
cd ride-share-app/backend && npm install

# Frontend
cd ../frontend && npm install
```

4. **Create .env Files**
```
See "Setup & Installation" section above
```

5. **Start Development Servers**
```bash
# Terminal 1: Backend
cd ride-share-app/backend
npm run dev

# Terminal 2: Frontend
cd ride-share-app/frontend
npm start
```

### Making Changes

```bash
# Make code changes in your feature branch
# Test locally

# Stage changes
git add .

# Commit with clear message
git commit -m "feat: add wallet payment system"

# Push to your branch
git push origin feature/your-feature-name

# Create Pull Request on GitHub
```

### Branching Strategy

```
main (Production-ready code)
├── develop (Integration branch)
│   ├── Kp-rat---2026 (Developer branch - YOUR BRANCH)
│   ├── feature/new-feature
│   ├── bugfix/fix-issue
│   └── feature/another-feature
```

### Common Development Tasks

**View All Changes:**
```bash
git status
git diff
```

**Undo Changes:**
```bash
# Undo unstaged changes
git checkout -- filename

# Undo staged changes
git reset filename

# Undo last commit (keep changes)
git reset --soft HEAD~1
```

**View Commit History:**
```bash
git log --oneline
git log --graph --all --decorate
```

---

## 🚢 Deployment Guide

### Local Production Build

**Backend:**
```bash
cd ride-share-app/backend

# Update .env for production
NODE_ENV=production
PORT=5000

# Start server
npm start
```

**Frontend:**
```bash
cd ride-share-app/frontend

# Create production build
npm run build

# Build creates 'build/' folder with optimized files
# Deploy 'build/' folder to static hosting
```

### Deploy on Heroku (Backend Example)

```bash
# Install Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli

# Login to Heroku
heroku login

# Create Heroku app
heroku create mana-prayanam-api

# Add MongoDB URI environment variable
heroku config:set MONGODB_URI="your_mongodb_connection_string"
heroku config:set JWT_SECRET="your_jwt_secret"

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

### Deploy Frontend on Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Connect GitHub repository for auto-deployment

# Update .env.production with production API URL
REACT_APP_API_URL=https://mana-prayanam-api.herokuapp.com/api
```

### Environment-Specific Configuration

**Development (.env)**
```
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/ride-share-db
JWT_SECRET=dev-secret-123
```

**Production (.env)**
```
NODE_ENV=production
MONGODB_URI=mongodb+srv://production-user:pwd@cluster.mongodb.net/ride-share-db
JWT_SECRET=production-secret-very-long-and-secure
```

---

## 🌿 GitHub Branch Management

### Your Developer Branch: `Kp-rat---2026`

### Pushing Changes to Your Branch

#### Method 1: Using Git Commands

```bash
# 1. Navigate to project directory
cd "c:\Users\10699924\OneDrive - LTIMindtree\Desktop\Man Prayanam RAT"

# 2. Configure Git (first time only)
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"

# 3. Initialize if not already a repo
git init

# 4. Add remote repository
git remote add origin https://github.com/Tkrishnaprasad/Mana-Prayanam.git

# 5. Fetch latest changes
git fetch origin

# 6. Check out your developer branch
git checkout Kp-rat---2026

# 7. Stage all changes
git add .

# 8. Commit changes
git commit -m "Your commit message describing changes"

# 9. Push to your branch
git push origin Kp-rat---2026
```

#### Method 2: Using VS Code (GUI)

1. Open Source Control panel (Ctrl+Shift+G)
2. Initialize repository if needed
3. Stage changes (click + icon)
4. Enter commit message
5. Click Commit
6. Click sync/push button

#### Example Commit Messages

```
git commit -m "feat: add payment gateway integration"
git commit -m "fix: resolve ride booking bug"
git commit -m "docs: update API documentation"
git commit -m "refactor: optimize database queries"
git commit -m "test: add unit tests for auth module"
```

### Viewing Branch Status

```bash
# See current branch
git branch

# List all branches
git branch -a

# See commit history
git log --oneline

# See changes since last push
git status
```

### Pulling Latest Changes from Origin

```bash
# Update your branch with latest from remote
git pull origin Kp-rat---2026

# Or fetch first, then merge
git fetch origin
git merge origin/Kp-rat---2026
```

---

## 🔧 Troubleshooting

### Backend Issues

#### Port 5000 Already in Use
```bash
# Windows PowerShell
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Linux/Mac
lsof -i :5000
kill -9 <PID>
```

#### MongoDB Connection Error
```
Error: MongoDB connection could not be established

Solution:
1. Verify .env MONGODB_URI is correct
2. Check if IP is whitelisted in MongoDB Atlas
3. Ensure internet connection active
4. Restart backend server
```

#### JWT Token Expired
```
Error: Invalid token

Solution:
1. Clear browser localStorage
2. Login again to get fresh token
3. Check JWT_SECRET matches in .env
```

### Frontend Issues

#### Port 3000 Conflict
```bash
# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Linux/Mac
kill -9 $(lsof -t -i:3000)
```

#### CORS Error
```
Error: Access to XMLHttpRequest blocked by CORS policy

Solution:
1. Verify backend CORS is enabled
2. Check API_URL in frontend config matches backend
3. Backend and frontend should be on same machine for local testing
```

#### npm Dependencies Issue
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Mobile App Issues

#### Expo Start Error
```bash
# Clear Expo cache
expo start --clear

# Or
expo start -c
```

#### API Connection from Physical Device
```
Update .env with your machine's IP address (not localhost)
EXPO_PUBLIC_API_URL=http://192.168.x.x:5000/api
```

### Git Issues

#### Git Not Recognized
```
Solution: Install Git from https://git-scm.com/download/win
Restart PowerShell/Terminal after installation
```

#### Authentication Failed When Pushing
```bash
# Use SSH keys (Recommended)
1. Generate SSH key: ssh-keygen -t ed25519
2. Add to GitHub: https://github.com/settings/keys
3. Clone using SSH: git clone git@github.com:...

# Or use Personal Access Token (PAT)
1. Create PAT: https://github.com/settings/tokens
2. Use as password when prompted
```

#### Merge Conflicts
```bash
# View conflicts
git status

# Manually edit files with <<<<<, =====, >>>>>

# After fixing
git add .
git commit -m "Resolve merge conflicts"
git push origin branch-name
```

---

## 📞 Support & Resources

### Documentation Files
- [COMPLETE_SETUP.md](COMPLETE_SETUP.md) - Full setup guide
- [FEATURES_SUMMARY.md](FEATURES_SUMMARY.md) - Detailed features
- [LOGIN_REGISTER_FLOW.md](LOGIN_REGISTER_FLOW.md) - Auth process
- [MOBILE_OTP_GUIDE.md](MOBILE_OTP_GUIDE.md) - OTP implementation
- [RIDE_CREATION_FIX.md](RIDE_CREATION_FIX.md) - Known issues & fixes

### External Resources
- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Manual](https://docs.mongodb.com/manual/)
- [React Documentation](https://react.dev/)
- [Socket.io Documentation](https://socket.io/docs/)
- [JWT.io](https://jwt.io/)

### Useful Links
- GitHub Repository: https://github.com/Tkrishnaprasad/Mana-Prayanam
- MongoDB Atlas: https://www.mongodb.com/cloud/atlas
- Razorpay Docs: https://razorpay.com/docs/
- Google OAuth: https://developers.google.com/identity

---

## 📊 Project Statistics

| Metric | Value |
|--------|-------|
| **Total Files** | 100+ |
| **Lines of Code** | 10,000+ |
| **Database Collections** | 7 |
| **API Endpoints** | 30+ |
| **Features** | 8+ |
| **Platforms** | 3 (Web, Mobile, Backend) |
| **Tech Stack Version** | Node 14+, React 18, MongoDB 5+ |
| **Current Status** | Production Ready |

---

## 📝 Changelog

### Version 2.0 (Current - February 2026)
- ✅ Mobile app integration (React Native Expo)
- ✅ Payment gateway (Razorpay)
- ✅ Real-time messaging (Socket.io)
- ✅ Ratings & reviews system
- ✅ OTP authentication
- ✅ Notification system
- ✅ Environmental impact tracking

### Version 1.0 (Initial Release)
- ✅ User authentication (JWT)
- ✅ Ride posting & search
- ✅ Ride booking system
- ✅ User profiles
- ✅ Basic ride management

---

## 👥 Contributors

- **Lead Developer:** Kp9959060606
- **GitHub:** [Tkrishnaprasad](https://github.com/Tkrishnaprasad)
- **Branch:** `Kp-rat---2026`

---

**Last Updated:** February 16, 2026  
**Document Version:** 2.0  
**Status:** Complete & Ready for Development

---

## 📚 Additional Resources

### Official Documentation Files

These detailed guides complement this master guide:

| Document | Purpose | Location |
|----------|---------|----------|
| **LOGIN_REGISTER_FLOW.md** | Comprehensive login/register architecture & UX design decisions | [Read](LOGIN_REGISTER_FLOW.md) |
| **MOBILE_OTP_GUIDE.md** | Detailed OTP implementation, SMS integration, and mobile-specific setup | [Read](MOBILE_OTP_GUIDE.md) |
| **RIDE_CREATION_FIX.md** | Demo mode explanation, troubleshooting, and test scenarios | [Read](RIDE_CREATION_FIX.md) |
| **MOBILE_APP_UPDATE_SUMMARY.md** | Mobile app updates, dual registration methods, method selector UI | [Read](MOBILE_APP_UPDATE_SUMMARY.md) |
| **FEATURES_SUMMARY.md** | Feature-by-feature breakdown: Payments, Ratings, Messaging | [Read](FEATURES_SUMMARY.md) |
| **COMPLETE_SETUP.md** | Quick start guide, current status, installation options | [Read](COMPLETE_SETUP.md) |
| **QUICK_REFERENCE.md** | Quick commands, access points, API endpoints, key files | [Read](QUICK_REFERENCE.md) |

### Key Implementation Guides

**Authentication:**
- [LOGIN_REGISTER_FLOW.md](LOGIN_REGISTER_FLOW.md) - Login/Register page architecture
- [MOBILE_OTP_GUIDE.md](MOBILE_OTP_GUIDE.md) - OTP implementation details

**Mobile Development:**
- [MOBILE_APP_UPDATE_SUMMARY.md](MOBILE_APP_UPDATE_SUMMARY.md) - Mobile app features
- [PRODUCTION_BUILD_GUIDE.md](ride-share-mobile/PRODUCTION_BUILD_GUIDE.md) - Mobile build & deployment

**Feature Specifications:**
- [FEATURES_SUMMARY.md](FEATURES_SUMMARY.md) - Payments, Ratings, Messaging

**Troubleshooting:**
- [RIDE_CREATION_FIX.md](RIDE_CREATION_FIX.md) - Demo mode and bug fixes

### External Resources

**Technology Documentation:**
- [Express.js Docs](https://expressjs.com/) - Backend framework
- [MongoDB Manual](https://docs.mongodb.com/manual/) - Database
- [React Documentation](https://react.dev/) - Frontend framework
- [React Native Docs](https://reactnative.dev/) - Mobile framework
- [Socket.io Docs](https://socket.io/docs/) - Real-time communication
- [JWT.io](https://jwt.io/) - JSON Web Tokens

**API Integration:**
- [Razorpay Documentation](https://razorpay.com/docs/) - Payment gateway
- [Google OAuth](https://developers.google.com/identity) - Authentication
- [Fast2SMS API](https://www.fast2sms.com/) - OTP/SMS service

**Deployment:**
- [Heroku Deployment](https://devcenter.heroku.com/articles/heroku-cli) - Backend hosting
- [Vercel Docs](https://vercel.com/docs) - Frontend hosting
- [Docker Documentation](https://docs.docker.com/) - Containerization
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) - Database hosting

### Project Repository

**GitHub Repository:**
- URL: https://github.com/Tkrishnaprasad/Mana-Prayanam
- Main Branch: `main` (Production)
- Developer Branch: `Kp-rat---2026` (Your branch)
- Issue Tracker: [GitHub Issues](https://github.com/Tkrishnaprasad/Mana-Prayanam/issues)

### Quick Links by Use Case

**I want to...**

| Task | Resource |
|------|----------|
| **Understand the architecture** | [Architecture section](#project-architecture) in this guide |
| **Set up the project** | [Setup & Installation](#setup--installation) |
| **Learn about authentication** | [Authentication & Login/Register Flows](#authentication--loginregister-flows) + [LOGIN_REGISTER_FLOW.md](LOGIN_REGISTER_FLOW.md) |
| **Implement OTP** | [Development Modes - Demo Mode](#-development-modes) + [MOBILE_OTP_GUIDE.md](MOBILE_OTP_GUIDE.md) |
| **Build mobile app** | [Mobile App Details](#-mobile-app-details) + [PRODUCTION_BUILD_GUIDE.md](ride-share-mobile/PRODUCTION_BUILD_GUIDE.md) |
| **Add new feature** | [Development Workflow](#-development-workflow) + [Features Overview](#-features-overview) |
| **Deploy to production** | [Deployment Guide](#-deployment-guide) |
| **Fix errors** | [Troubleshooting](#-troubleshooting) + [RIDE_CREATION_FIX.md](RIDE_CREATION_FIX.md) |
| **Push to GitHub** | [GitHub Branch Management](#-github-branch-management) |
| **Test without database** | [Development Modes](#-development-modes) + [RIDE_CREATION_FIX.md](RIDE_CREATION_FIX.md) |

---

**End of Document**
