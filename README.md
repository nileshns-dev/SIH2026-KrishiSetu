# 🌾 KrishiSetu

### Smart Agricultural Procurement & Queue Management Platform

**Smart India Hackathon 2026 — Prototype**

KrishiSetu is a digital platform designed to improve the agricultural procurement experience for farmers and procurement-centre staff.

The system provides a unified interface for **farmer registration, procurement slot booking, AI-assisted scheduling, live queue tracking, procurement processing, DBT payment workflow, notifications, and market-level analytics**.

---

## 🎯 Problem

Farmers visiting procurement centres can face:

* Long and uncertain waiting times
* Lack of predictable procurement slots
* Unclear queue status
* Repeated visits to procurement centres
* Limited visibility into the procurement process
* Inefficient coordination between farmers and procurement-centre staff

At the procurement-centre level, staff also need better tools to manage incoming farmers, track procurement progress, process weighments, and monitor payments.

KrishiSetu aims to bring these workflows into a single digital platform.

---

## 💡 Core Idea

KrishiSetu follows a simple workflow:

> **Register → Schedule → Arrive → Process → Pay → Track**

### For Farmers

Farmers can:

1. Register using their name and mobile number
2. Verify their registration using an OTP workflow
3. Select an APMC market
4. Select their crop
5. Enter the quantity they intend to sell
6. Receive an AI-assisted market/date recommendation
7. Book a procurement slot
8. Receive a digital procurement pass
9. Track their procurement status
10. View their booking history
11. Receive procurement-related alerts

The prototype currently supports crops including **Wheat, Rice, Cotton, Maize, Bajra, Jowar, and Sugarcane**.

---

# 👨‍🌾 Farmer Portal

The Farmer Portal is designed to provide a simple procurement experience from registration through payment.

### Registration

The prototype includes:

* Name validation
* 10-digit Indian mobile number validation
* Returning-user session handling
* OTP verification workflow
* Registered-mobile-number checks

For demonstration purposes, the OTP is currently fixed to:

```text
1234
```

The authentication flow is implemented entirely inside the prototype and is not connected to a real SMS/OTP provider.

### Slot Booking

Farmers can select:

* APMC market
* Crop
* Quantity in kilograms
* Procurement date/slot

The current prototype includes APMC options for:

* Gandhinagar
* Ahmedabad
* Rajkot
* Surat

It also provides predefined procurement time slots ranging from **8–9 AM through 7–8 PM**.

---

# 🤖 AI-Assisted Recommendation

The booking interface contains an AI Optimizer workflow.

Based on the prototype's simulated forecasting logic, the system can recommend a suggested selling date and display an estimated additional return per kilogram.

The farmer can then choose between:

* **Book Suggested Date**
* **Book for Today**

The current UI presents this as an ML/AI recommendation and is intended as a prototype demonstration rather than a production market-price prediction service.

---

# 🎫 Digital Procurement Pass

After booking, the farmer receives a digital procurement pass containing information such as:

* Token number
* Procurement date
* Time slot
* APMC market
* Farmer name
* Crop
* Quantity
* Estimated waiting time
* Crop-supply information
* Encoded token/barcode representation

The pass acts as the farmer's digital representation of their procurement appointment.

---

# 📍 Live Procurement Tracker

Farmers can track the progress of their procurement request through a three-stage workflow:

```text
🎫 Slot Booked
       │
       ▼
⚖️ Crop Weighed
       │
       ▼
🏦 Payment Sent
```

The tracker updates according to actions performed by the procurement-centre staff.

This allows the farmer to understand where their procurement currently stands without relying entirely on manual communication.

---

# 🏢 Mandi Administration

KrishiSetu provides a separate administrative gateway for procurement-centre operations.

The gateway contains two administrative roles:

### Mandi Staff / Worker

Responsible for:

* Calling tokens
* Managing the queue
* Recording weighment
* Quality-related actions
* Authorizing DBT payment

### Super Admin

Responsible for:

* Monitoring a selected APMC market
* Viewing procurement analytics
* Monitoring transactions
* Viewing crop distribution
* Monitoring centre workers

The prototype explicitly separates these two administrative workflows.

---

# 👷 Mandi Worker Dashboard

The worker dashboard provides a live queue-management interface.

It displays statistics such as:

* Total tokens
* Waiting farmers
* Farmers at the counter
* Processed/paid farmers

Workers can also filter the queue by crop.

The queue contains information including:

* Token and mandi
* Farmer details
* Estimated processing time
* Current status
* Available actions

---

# ⚖️ Procurement Processing

The worker can progress a farmer through the procurement workflow.

### Weighment

A worker can mark a booking as:

```text
WEIGHED
```

The system then updates the farmer's procurement status and generates a notification.

### Quality Rejection

A procurement request can be marked:

```text
REJECTED
```

The prototype provides a QC failure notification explaining that the rejection is associated with a moisture/quality mismatch.

### Payment

After successful processing, the worker can select:

```text
Approve & Pay
```

The booking status becomes:

```text
PAID
```

and the prototype generates a DBT payment notification.

---

# 📱 Notification System

KrishiSetu contains an SMS-style notification interface.

Notifications can be generated for events such as:

* Slot confirmation
* Successful weighment
* QC rejection
* DBT payment

The prototype displays these notifications inside the application using an SMS-style inbox/banner.

For example:

```text
[KrishiSetu Mandi Alert]

Your slot is confirmed...
```

The current implementation is a **simulated notification system** and is not connected to a real SMS gateway.

---

# 🛡️ Super Admin Command Center

The Super Admin interface provides market-specific operational monitoring.

The dashboard supports different time horizons:

* Day-wise
* Week-wise
* Season-wise

It includes sections for:

### Procurement Analytics

* Gross procurement
* DBT disbursed
* Centre workers
* QC rejections
* Crop distribution
* Transaction ledger

### Worker Management

The interface also provides a worker/credential management view for the selected market.

The Super Admin console is designed around **single-market control**, meaning the selected APMC market is treated as the administrative scope of the dashboard.

---

# 🌐 Multilingual Interface

The prototype includes a built-in translation system.

The currently exposed language selector includes:

* 🇬🇧 English
* 🇮🇳 Hindi
* ગુજરાતી Gujarati
* తెలుగు Telugu
* தமிழ் Tamil

The interface dynamically updates labels, crop names, mandi names, tracker states, and other UI elements when the language is changed.

---

# 👓 Elder Mode

KrishiSetu includes an accessibility-focused **Elder Mode**.

When enabled, the interface switches to a high-contrast presentation with:

* Larger text
* Heavier typography
* High-contrast colours
* Larger form controls
* Stronger borders

The prototype uses a black/yellow high-contrast configuration for this mode.

The goal is to make the system more usable for elderly farmers and users with limited visual accessibility.

---

# 💾 Data Storage

The current prototype uses the browser's **LocalStorage** as its persistence layer.

Stored information includes:

* Bookings
* Farmer sessions
* Token sequence
* Registered phone numbers
* Demo worker information

For example:

```text
krishi_db_bookings
krishi_session_farmer
krishi_token_seq
krishi_db_registered_phones
krishi_db_workers
```

This allows the prototype to retain data during a browser session without requiring an external database.

---

# 🏗️ Current Prototype Architecture

The current version is intentionally a browser-based prototype.

```text
┌─────────────────────────────────────────┐
│              KrishiSetu UI              │
│            HTML + Tailwind CSS          │
├─────────────────────────────────────────┤
│                                         │
│  Farmer Portal     Mandi Worker Portal  │
│        │                    │           │
│        └──────────┬─────────┘           │
│                   │                     │
│            Application Logic            │
│              JavaScript                 │
│                   │                     │
│                   ▼                     │
│              LocalStorage               │
│                                         │
└─────────────────────────────────────────┘
```

The current prototype is contained in a single HTML application with its UI, styling, state management, authentication flows, translations, booking logic, dashboards, and browser storage logic implemented within the same prototype.

The next development stage is to modularize this architecture into a proper frontend/backend application.

---

# 🛠️ Technology Used in the Prototype

### Frontend

* HTML5
* JavaScript
* Tailwind CSS
* Font Awesome
* Google Fonts

### Client-side Data

* Browser LocalStorage

### UI / Accessibility

* Responsive layouts
* Multilingual interface
* Elder Mode
* Toast notifications
* SMS-style notifications
* Digital procurement pass

The prototype loads Tailwind CSS and Font Awesome through CDN resources.

---

# 📋 Supported Workflow

The complete demonstrated workflow can be summarized as:

```text
                     ┌──────────────┐
                     │    Farmer    │
                     └──────┬───────┘
                            │
                            ▼
                    Farmer Registration
                            │
                            ▼
                       OTP Verify
                            │
                            ▼
                    Select APMC Market
                            │
                            ▼
                     Select Crop + Qty
                            │
                            ▼
                  AI-assisted Recommendation
                            │
                            ▼
                      Book Slot
                            │
                            ▼
                  Digital Procurement Pass
                            │
                            ▼
                      Live Tracking
                            │
                            ▼
              ┌─────────────────────────┐
              │   Mandi Worker Desk     │
              └────────────┬────────────┘
                           │
                           ▼
                     Call / Process
                           │
                           ▼
                       Weighment
                           │
                    ┌──────┴──────┐
                    │             │
                    ▼             ▼
                 Approved       Rejected
                    │
                    ▼
                 DBT Payment
                    │
                    ▼
              Farmer Notification
```

---

# 📍 Demo APMC Markets

The prototype currently provides four demonstration markets:

| Market           | Availability |
| ---------------- | ------------ |
| Gandhinagar APMC | ✅            |
| Ahmedabad APMC   | ✅            |
| Rajkot APMC      | ✅            |
| Surat APMC       | ✅            |

---

# 🌾 Supported Crops

| Crop      |
| --------- |
| Wheat     |
| Rice      |
| Cotton    |
| Maize     |
| Bajra     |
| Jowar     |
| Sugarcane |

The prototype also contains configurable MSP-rate values for these crops.

---

# 🔐 Authentication

The current implementation contains separate demonstration authentication flows for:

### Farmer

```text
Name + Mobile Number
        ↓
     OTP
        ↓
     Login
```

### Mandi Worker

```text
APMC Market
     +
Official Email
     +
Password
     ↓
Worker Dashboard
```

### Super Admin

```text
APMC Market
     +
Admin ID / Email
     +
Security Key
     ↓
Market Command Center
```

The current authentication system is **prototype/demo authentication**, not production-grade security.

---

# ⚠️ Prototype Disclaimer

KrishiSetu is currently a **Smart India Hackathon prototype**.

Several components are simulated for demonstration purposes.

This includes:

* OTP verification
* SMS notifications
* DBT payment
* Government authentication
* Worker credentials
* Market analytics
* AI recommendations
* Browser-based persistence

The prototype should therefore **not be interpreted as a production government procurement system** or as being directly integrated with government, banking, Aadhaar, or telecom infrastructure.

Production deployment would require secure backend authentication, encrypted data storage, real identity verification, authorized government integrations, payment infrastructure, notification providers, and appropriate security/compliance controls.

---

# 🚀 Future Development

The prototype is intended to evolve into a modular full-stack application.

Planned improvements include:

* [ ] React-based frontend
* [ ] Node.js backend
* [ ] PostgreSQL database
* [ ] REST APIs
* [ ] Secure authentication
* [ ] Production-grade role-based access control
* [ ] Real SMS/notification integration
* [ ] Real payment/DBT integration
* [ ] Production ML pipeline
* [ ] Real procurement-centre data
* [ ] Dynamic queue prediction
* [ ] Automated no-show handling
* [ ] Intelligent rescheduling
* [ ] Multi-centre scheduling optimization
* [ ] Expanded language support
* [ ] Deployment and monitoring

---

# 📌 Project Status

**Current stage: Functional Hackathon Prototype**

The current prototype demonstrates the major user journeys for:

```text
Farmer
  ↓
Registration
  ↓
Slot Booking
  ↓
AI Recommendation
  ↓
Digital Pass
  ↓
Live Tracking
  ↓
Mandi Processing
  ↓
Weighment / QC
  ↓
Payment
  ↓
Notification
```

The next major engineering milestone is converting the prototype from a monolithic client-side application into a maintainable, modular full-stack system.

---

# 👥 Team

**KrishiSetu**

Developed for:

**Smart India Hackathon 2026**

---

<p align="center">
  🌾 <b>KrishiSetu</b><br>
  <i>Making agricultural procurement more predictable, transparent and accessible.</i>
</p>
