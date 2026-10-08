# 🏡 StayEase — Airbnb Clone

A full-stack web application inspired by Airbnb where users can explore property listings, create their own listings, leave reviews, and securely authenticate using traditional login and Google OAuth.

The project demonstrates real-world backend architecture including authentication, authorization, session management, cloud image storage, database relationships, MVC architecture, and secure route protection.

---

📂 **GitHub Repository**
https://github.com/Anant23-27

---

# 📌 Project Overview

**StayEase** is a full-stack property listing platform inspired by Airbnb.

The application allows users to discover and explore properties, create their own property listings, upload property images, and share their experiences through reviews.

The platform implements secure authentication and authorization mechanisms to ensure that users can only perform actions they are permitted to perform.

The project was developed to understand how real-world full-stack applications work internally, including:

* User authentication
* Google OAuth
* Session-based authentication
* Authorization and access control
* CRUD operations
* MongoDB relationships
* Cloud-based image storage
* MVC architecture
* Server-side rendering
* Error handling and validation

---

# ✨ Features

## 1. User Authentication System

StayEase supports both traditional authentication and Google OAuth authentication.

### Local Authentication

Users can create an account using a username and password.

Features include:

* User signup
* User login
* User logout
* Secure password hashing
* Persistent login sessions
* Session storage using MongoDB

Password authentication is handled using **Passport.js** and **passport-local-mongoose**.

### Google OAuth Authentication

Users can also sign in using their Google account.

### Google OAuth Flow

1. User clicks **Login with Google**
2. User is redirected to Google's authentication page
3. Google authenticates the user
4. Google sends the authentication response to the application's callback route
5. Passport verifies the user
6. The application creates or finds the corresponding user
7. A session is created
8. The user is logged into StayEase

---

# 🏠 2. Property Listing Management

StayEase allows users to explore existing properties and create their own listings.

### Listing Features

Users can:

* View all available properties
* View individual property details
* Create new property listings
* Edit their own listings
* Delete their own listings
* Upload property images

Each listing contains information such as:

* Title
* Description
* Price
* Location
* Country
* Image

Listings are stored in **MongoDB** and associated with the user who created them.

---

# ⭐ 3. Review & Rating System

Users can share their experience by reviewing properties.

Review functionality includes:

* Add reviews
* Give ratings
* Add comments
* View reviews on property pages
* Delete their own reviews

Each review maintains relationships with:

* The property/listing
* The user who created the review

This demonstrates the use of relationships between MongoDB documents using **Mongoose references**.

---

# 🔐 4. Authorization & Access Control

StayEase implements authorization middleware to protect resources.

Authentication answers:

> **"Who is the user?"**

Authorization answers:

> **"Is this user allowed to perform this action?"**

### Listing Authorization

Only the owner of a listing can:

* Edit the listing
* Delete the listing

### Review Authorization

Only the author of a review can:

* Delete their review

This prevents unauthorized users from modifying or deleting resources belonging to other users.

---

# 🖼 5. Image Upload & Cloud Storage

StayEase allows users to upload images when creating property listings.

The application uses:

* **Multer** → handles file uploads
* **Cloudinary** → stores images in the cloud
* **multer-storage-cloudinary** → connects Multer with Cloudinary

Instead of storing images directly on the application server, images are uploaded to cloud storage.

This makes the application more suitable for deployment and scalable web applications.

---

# 💬 6. Flash Messages

StayEase uses **connect-flash** to provide temporary feedback messages to users.

Examples include:

* Login successful
* Signup successful
* Listing created successfully
* Listing updated successfully
* Listing deleted
* Unauthorized access
* Review-related notifications

These messages improve the user experience by providing immediate feedback after an action.

---

# ⚠️ 7. Error Handling

The application includes centralized error handling.

### ExpressError

A custom `ExpressError` class is used to create structured application errors.

### wrapAsync

A `wrapAsync` utility is used to handle errors from asynchronous Express route handlers.

This helps avoid repetitive `try/catch` blocks and ensures errors are passed to the centralized Express error-handling middleware.

---

# 🏗 Project Architecture

StayEase follows the **MVC (Model-View-Controller)** architecture.

This separates database models, application/business logic, routes, and presentation.

---

## 📦 Models

Located inside:

```text
/models
```

Models define the structure of the application's database documents.

### User

Stores user-related information and authentication data.

### Listing

Stores property information and its relationship with the property owner.

### Review

Stores review information and references both the listing and the user.

---

## 🎮 Controllers

Located inside:

```text
/controllers
```

Controllers contain the main application/business logic.

They handle operations related to:

* Listings
* Reviews
* Users

This keeps the route files cleaner and separates routing from business logic.

---

## 🛣 Routes

Located inside:

```text
/routes
```

Routes define the application's endpoints and connect incoming requests with the appropriate controller functions.

Major route groups include:

* Listing routes
* Review routes
* User authentication routes
* Google OAuth routes

---

## 🖥 Views

Located inside:

```text
/views
```

StayEase uses **EJS** for server-side rendering.

The view layer contains:

* Listing pages
* Listing creation forms
* Listing editing forms
* Authentication pages
* Review sections
* Layouts
* Reusable partials

**EJS Mate** is used to simplify layout and reusable view structures.

---

# 🛠 Tech Stack

## Backend

### Node.js

Used as the JavaScript runtime for executing the server-side application.

### Express.js

Used to build the web server, routes, middleware, and REST-style endpoints.

---

## 🗄 Database

### MongoDB

Used as the application's NoSQL database.

MongoDB stores:

* Users
* Listings
* Reviews
* Relationships between these entities

### Mongoose

Used as an ODM (Object Data Modeling) library for MongoDB.

Mongoose provides:

* Schemas
* Models
* Validation
* Database relationships
* Querying MongoDB

---

# 🔑 Authentication

Authentication is implemented using **Passport.js**.

Libraries used include:

* `passport`
* `passport-local`
* `passport-local-mongoose`
* `passport-google-oauth20`

The application supports:

1. Username/password authentication
2. Google OAuth authentication

---

# 🔄 Session Management

StayEase uses:

* `express-session`
* `connect-mongo`

Sessions allow the application to remember authenticated users across requests.

Instead of keeping session data only in server memory, sessions are stored in MongoDB.

This makes session management more suitable for a deployed application.

---

# ☁️ Image Storage

StayEase uses **Cloudinary** for storing property images.

Technologies used:

* Multer
* Cloudinary
* multer-storage-cloudinary

The flow is:

```text
User
  ↓
Upload Image
  ↓
Multer
  ↓
Cloudinary
  ↓
Image URL
  ↓
MongoDB Listing
```

The listing stores the image information/URL instead of storing the actual image file inside the project.

---

# 🎨 Frontend

The frontend uses:

* EJS
* EJS Mate
* HTML
* CSS
* JavaScript

EJS allows dynamic server-side rendering of property and user information.

---

# 🧰 Other Libraries

StayEase also uses several supporting libraries:

| Library         | Purpose                                     |
| --------------- | ------------------------------------------- |
| Joi             | Server-side schema validation               |
| method-override | Enables PUT/DELETE requests from HTML forms |
| connect-flash   | Temporary success/error messages            |
| dotenv          | Environment variable management             |
| cookie-parser   | Cookie parsing                              |
| nodemailer      | Email-related functionality                 |

---

# 🔐 Authentication & Authorization Flow

## Authentication Flow

For local authentication:

```text
User
 ↓
Signup/Login
 ↓
Passport
 ↓
Verify Credentials
 ↓
Create Session
 ↓
User Authenticated
```

For Google authentication:

```text
User
 ↓
Login with Google
 ↓
Google OAuth
 ↓
Google Authentication
 ↓
OAuth Callback
 ↓
Passport
 ↓
Find/Create User
 ↓
Create Session
 ↓
User Logged In
```

---

# 🛡 Authorization Flow

When a user attempts to modify a listing:

```text
User Request
     ↓
Authentication Check
     ↓
Is User Logged In?
     ↓
Ownership Check
     ↓
Is User the Listing Owner?
     ↓
Allow / Deny Request
```

This ensures that authentication alone is not enough to modify protected resources.

---

# 📂 Project Folder Structure

```text
StayEase
│
├── config
│   ├── db.js
│   ├── passport.js
│   └── passportGoogle.js
│
├── controllers
│   ├── allListings.js
│   ├── reviews.js
│   └── users.js
│
├── models
│   ├── listing.js
│   ├── review.js
│   └── user.js
│
├── routes
│   ├── listing.js
│   ├── review.js
│   ├── user.js
│   └── auth.js
│
├── utils
│   ├── ExpressError.js
│   ├── sendEmail.js
│   └── wrapAsync.js
│
├── public
│   ├── css
│   └── js
│
├── views
│   ├── includes
│   ├── layouts
│   ├── listings
│   └── users
│
├── middleware.js
├── cloudConfig.js
├── app.js
├── package.json
└── .env
```

---

# ⚙️ Environment Variables

Create a `.env` file and configure the required environment variables:

```env
MONGO_URI=

SESSION_SECRET=

CLOUDINARY_CLOUD_NAME=
CLOUDINARY_KEY=
CLOUDINARY_SECRET=

GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

EMAIL_USER=
EMAIL_PASS=
```

> Environment variables contain sensitive credentials and should never be committed to GitHub.

---

# 🔮 Future Improvements

Potential future improvements for StayEase include:

### 🖼 Multiple Image Upload

Allow property owners to upload multiple images for a single listing.

### 🗺 Map Integration

Integrate a map service to display the geographical location of properties.

### 🖼 Image Gallery

Add an interactive image gallery with next/previous navigation.

### 💬 Contact Property Owner

Allow users to directly communicate with property owners.

### 🔎 Advanced Search & Filtering

Add filters for:

* Price
* Location
* Property type
* Rating
* Availability

### 📅 Booking System

Introduce property availability and booking functionality.

### 💳 Payment Integration

Integrate a payment gateway to allow users to securely pay for reservations.

---

# 📚 What I Learned

Through the development of StayEase, I gained practical understanding of:

* Full-stack web application architecture
* Node.js and Express.js
* MongoDB and Mongoose
* MVC architecture
* CRUD operations
* User authentication
* Passport.js
* Google OAuth
* Session-based authentication
* Authorization middleware
* Cloudinary image storage
* File uploads using Multer
* Server-side validation
* Error handling in Express
* MongoDB document relationships
* EJS server-side rendering
* Deployment of full-stack applications
* Environment variable management

---

# 🎯 Key Technical Concepts Demonstrated

StayEase demonstrates several concepts commonly used in real-world web applications:

**Authentication**

```text
Passport.js + Local Authentication + Google OAuth
```

**Authorization**

```text
Authentication + Ownership Verification
```

**Database Relationships**

```text
User
 ↓
Listing
 ↓
Review
```

**Cloud Storage**

```text
Multer → Cloudinary → Listing
```

**Architecture**

```text
Routes → Controllers → Models → MongoDB
                 ↓
               Views
```

---

# 👨‍💻 Author

Anant Nigam

CSE Student

GitHub:
https://github.com/Anant23-27

---

# ⭐ Support

If you found **StayEase** useful or interesting, consider giving the project a ⭐ on GitHub.
