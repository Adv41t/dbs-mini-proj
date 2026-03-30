# Event Registration and Attendance Management System

![DBSL Mini Project](erdiagram.png) *(ER Diagram above - see included files for more details)*

## 📑 Project Overview

The **Event Registration and Attendance Management System** is a comprehensive full-stack application designed to streamline the management of university or organizational events. Built for a Database Management Systems Laboratory (DBSL) Mini Project, this system effectively handles users with varying roles, event schedules, ticketing, registrations, attendances, payments, and feedback collection. 

It provides an intuitive frontend for participants to browse, register, and pay for events, while offering a powerful administrative dashboard for organizers to track statistics, attendance, and revenue in real-time.

---

## 🛠️ Tech Stack & Architecture

### **Frontend (Client-Side)**
* **Framework:** React 19 (via Vite)
* **Routing:** React Router DOM (v7)
* **Styling:** Tailwind CSS + PostCSS
* **HTTP Client:** Axios for API requests

### **Backend (Server-Side)**
* **Framework:** Node.js with Express.js
* **Middleware:** CORS & Express JSON parser
* **Database Driver:** `oracledb` (Node-Oracle DB integration)

### **Database Layer**
* **Database Management System:** Oracle Database (XE / XEPDB1)
* **Schema Design:** Fully normalized relational SQL schema

---

## 📂 Project Structure

```text
dbs-mini-proj/
│
├── backend/                       # Node/Express API Server
│   ├── package.json               # Backend dependencies
│   └── server.js                  # Main server logic & route controllers
│
├── database/                      # Database Schema and Seeds
│   └── 01_schema_and_data.sql     # Complete DB schema (Tables, Indexes, Sample Data)
│
├── event-frontend/                # React/Vite Frontend Application
│   ├── public/                    # Static assets
│   ├── src/                       # Frontend source code
│   │   ├── assets/                # Images and styles
│   │   ├── components/            # Reusable UI components
│   │   ├── context/               # React Context for global state 
│   │   ├── mock/                  # Mock data for prototyping
│   │   ├── pages/                 # Full-page React views
│   │   │   ├── Admin.jsx          # Admin dashboard & management
│   │   │   ├── Dashboard.jsx      # Participant portal
│   │   │   ├── EventDetails.jsx   # Specific event info page
│   │   │   ├── Events.jsx         # Event catalog/listing
│   │   │   ├── Feedback.jsx       # Event feedback submission
│   │   │   ├── Login.jsx          # User authentication
│   │   │   └── Payment.jsx        # Payment processing UI
│   │   ├── services/              # API and backend service interactions
│   │   ├── App.jsx                # Core application routing
│   │   └── main.jsx               # React entry point
│   ├── package.json               # Frontend dependencies
│   ├── tailwind.config.js         # Tailwind styling configuration
│   └── vite.config.js             # Vite build configuration
│
├── DBSL_MiniProj.pdf              # Official Problem Statement/Assignment 
├── erdiagram.png                  # Entity-Relationship diagram illustration
└── structure of table.png         # Database table layout visual reference 
```

---

## ✨ Key Features & Functionalities

### 1. **Role-Based Access Control (RBAC)**
The system accommodates five distinct roles: `Admin`, `Organizer`, `Student`, `Volunteer`, and `Faculty`. 

### 2. **Authentication System**
* **Registration & Login:** Secure system allowing new users to sign up and existing users to authenticate.

### 3. **Event & Venue Management**
* **Event Catalogs:** Browse upcoming categorised events (Workshops, Seminars, Hackathons, Cultural Events, Sports).
* **Multi-Session Tracking:** Single events can have multiple sub-sessions (e.g., Opening Ceremony, Keynote, Final Presentation).
* **Venue Allocations:** Assign events to distinct geographical venues with capacity constraints enforced.

### 4. **Registration & Ticketing**
* **Multiple Ticket Tiers:** Support for various ticket varieties (Standard Pass, Premium Pass, VIP, Teams, Student Discount) with individual pricing and quantity tracking.
* **Waitlisting System:** Handles overcapacity gracefully by pushing participants into a categorized waitlist queue. 

### 5. **Payment Gateway Simulation**
* Secure tracking of payment statuses (`Pending`, `Completed`, `Failed`).
* Monitors revenue generation via multiple payment channels (Card, NetBanking, etc.).

### 6. **Attendance & Feedback**
* Verify and register `Present`/`Absent` statuses tracking per sub-session.
* Post-event feedback collection system with a 5-star rating scale and written review options.

### 7. **Administrative Dashboard View**
* Comprehensive metrics showing Total Users, Total Events, Overall Registrations, and gross Real-time Revenue.
* Granular tables for reviewing registrations, payments, session attendances, and feedback. 

---

## 🗄️ Database Schema & Entities

The project is driven by a highly structured relational database. Below is the entity breakdown:

1. **`Role`**: Maintains user privilege levels.
2. **`Users`**: Primary authentication and participant identity table.
3. **`Venue`**: Stores physical location constraints (Building, Capacity).
4. **`Event_Category`**: Tags to classify events.
5. **`Event`**: The core application table linking organizers, venues, and categories.
6. **`Event_Session`**: Time-boxed periods occurring during an overarching Event.
7. **`Ticket_Type`**: Cost and quantity definitions mapped to an Event.
8. **`Registration`**: Links a User to an Event through a selected Ticket. 
9. **`Payment`**: Financial ledger tracking transaction statuses for a respective Registration.
10. **`Attendance`**: The junction maintaining whether an individual attended a particular Session.
11. **`Feedback`**: Quantitative metrics linked to a specific Registration footprint.

*(Indexed properly for scaled query performance.)*

---

## 🚀 Setup & Installation Guide

To run this project locally, follow these sequential steps:

### Prerequisites:
* **Node.js** (v18 or higher)
* **Oracle Database** (XE / XEPDB1) Express Edition installed locally.
* **Oracle Instant Client** (if required by your OS for `oracledb`).

### Step 1: Database Initialization
1. Open your Oracle DBMS tool (e.g., SQL Developer or SQL*Plus).
2. Create/Log into your desired schema/user (`system`, password: `dipen_b23` as configured out-of-the-box).
3. Execute the entire contents of `database/01_schema_and_data.sql`. This will orchestrate table creations, insert vital seed data, and build necessary indexes.

### Step 2: Backend Setup
1. Open a terminal and navigate to the backend directory:
   ```bash
   cd dbs-mini-proj/backend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Update connection bindings (if necessary) in `server.js`:
   ```javascript
   const dbConfig = {
     user: "system",
     password: "your_password",
     connectString: "localhost:1521/XEPDB1"
   };
   ```
4. Start the Express server:
   ```bash
   node server.js
   ```
   *Server will run on `http://localhost:5000`.*

### Step 3: Frontend Setup
1. Open a fresh terminal and navigate to the frontend directory:
   ```bash
   cd dbs-mini-proj/event-frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the Vite development server:
   ```bash
   npm run dev
   ```
4. Access the web App on your local browser (usually `http://localhost:5173`).

---

## 🔗 API Route Endpoints Reference

### **Authentication**
- `POST /login` - Authenticate an existing user.
- `POST /register` - Register a new user into the database.
- `GET /users` - Retrieve a collection of users.

### **Events & Transactions (Participant)**
- `POST /events/:eventId/register` - Create a registration instance tied to a ticket.
- `POST /payment` - Process checkout balances linked to a registration.
- `POST /feedback` - Submit an event evaluation mapping to a registration ID.
- `GET /users/:userId/registrations` - Acquire historical registrations based on the specific Participant user ID.

### **Administrative Insights**
- `GET /admin/stats` - Pull aggregate scalar statistics (totals & revenue).
- `GET /admin/events` - Retrieve comprehensive event tables.
- `GET /admin/registrations` - Fetch robust tracking data encompassing registration and matching status.
- `GET /admin/payments` - Monitor complete payment ledger.
- `GET /admin/feedback` - Read structured reviews collected from events.
- `GET /admin/attendance` - Inspect the granular session-based attendance validation list.

---

> **Note:** This project is a demonstration of Database Management Systems principles, utilizing normalized entities, foreign key constraints natively enforced at the DB level, and complex join queries rendering real-world data models.
