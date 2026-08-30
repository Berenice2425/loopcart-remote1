# LoopCart
LoopCart is a Python application that delivers personalised welcome messages to users.

## Project Purpose
This lab covers: cloning a repo, creating a feature branch, writing and testing code, committing with meaningful messages, pushing and opening a Pull Request, applying code review feedback, merging to main, and triggering a CI/CD pipeline.

## Prerequisites
- Git installed and configured
- Git installed and configured
- Python 3 installed
- Terminal access (Windows users: use Git Bash)

## Getting Started
Clone the repository: git clone <repo-url> loopcart
Enter the folder: cd loopcart
Run the app: python3 app.py

## Contributing
1. Create a feature branch: git checkout -b feat/your-feature
2. Commit your changes: git commit -m feat: describe your change
3. Push the branch: git push -u origin feat/your-feature
4. Open a Pull Request and request a review
5. Apply feedback then merge to main

## License
MIT



# VShield - Complete Documentation

## For Google Africa Applied AI Lab Application

---

## 1. Executive Summary

**VShield** is an AI-powered biometric vehicle immobilization system designed to combat Nigeria's escalating car theft crisis. The platform combines facial recognition, fingerprint authentication, and real-time threat detection with a tamper-proof hardware module that operates entirely offline—ensuring vehicles remain secure even in areas with poor internet connectivity.

**Market Opportunity:** Nigeria faces a persistent vehicle theft epidemic with over 1,500 vehicles reported stolen annually (Nigeria Police Force, 2024). Traditional security measures like manual locks and basic GPS trackers are easily bypassed by sophisticated criminal networks.

**Thematic Fit:** This application directly addresses the **"Future of Knowledge"** and **"Software Development"** themes of the Google Africa Applied AI Lab, leveraging AI to solve a critical safety challenge uniquely African in nature.

**Key Features:**
- Biometric Authentication (Face + Fingerprint)
- Offline Operation (No Internet Required)
- Tamper-Proof Design (Camera removal = Immobilized)
- Multi-Car Management (Unlimited Vehicles)
- AI Threat Detection (Google Gemini Integration)
- Real-Time Alerts & Monitoring

---

## 2. Problem Statement

### The Nigerian Vehicle Security Crisis

Vehicle theft remains a major concern in major Nigerian cities, with organized criminal networks targeting both private and commercial vehicles. According to the Nigeria Police Force e-CMR platform, over 1,500 stolen vehicles were recovered in 2024, representing only a fraction of actual thefts.

**Key Challenges:**
- Traditional GPS trackers are easily disabled by thieves
- Basic alarms provide no deterrence against determined criminals
- Key fob relay attacks allow thieves to steal vehicles without breaking windows
- Most security systems require constant internet connectivity (unreliable in Nigeria)
- Existing biometric systems are expensive and not widely available

**Current Market Solutions & Gaps:**

| Feature | Traditional GPS | Basic Biometric | VShield |
|---------|----------------|-----------------|---------|
| Real-time Location | ✅ | ❌ | ✅ |
| Facial Recognition | ❌ | ❌ | ✅ |
| Fingerprint Auth | ❌ | Partially | ✅ |
| Offline Operation | ❌ | ✅ | ✅ |
| Tamper-Proof | ❌ | ❌ | ✅ |
| AI Threat Detection | ❌ | ❌ | ✅ |
| Multi-Car Management | ❌ | ❌ | ✅ |

---

## 3. Solution Overview

VShield is a complete vehicle security ecosystem comprising:

1. **Mobile App** (iOS & Android) - User interface and control center
2. **VShield Brain** - Hardware module installed in the vehicle (ESP32-S3 + Camera + Fingerprint Sensor)
3. **AI Engine** - Google Gemini for threat detection and biometric authentication
4. **Cloud Platform** - For fleet management and remote analytics (optional)

### Core Features

| Feature | Description |
|---------|-------------|
| **Biometric Authentication** | Face + fingerprint verification for engine start |
| **Tamper-Proof Design** | Camera removal or disabling instantly immobilizes vehicle |
| **Offline Operation** | No internet required for core authentication |
| **Multi-Car Management** | Manage unlimited vehicles from one app |
| **AI Threat Detection** | Predicts and alerts on suspicious activity using Gemini |
| **Geofencing** | Virtual boundaries with instant notifications |
| **Key Sharing** | Securely share access with family or fleet drivers |

---

## 4. Use Case Diagram

```
+=============================================================+
|                     VSHIELD SYSTEM                          |
+=============================================================+
|                                                             |
|  +-------------------+   +-------------------+              |
|  |   CAR OWNER       |   |   FLEET MANAGER  |              |
|  +-------------------+   +-------------------+              |
|  | 1. Register Acc.  |   | 1. View Fleet    |              |
|  | 2. Add Vehicle    |   | 2. Arm All       |              |
|  | 3. Register Face  |   | 3. Gen Reports   |              |
|  | 4. Register FP    |   | 4. Monitor       |              |
|  | 5. Arm Vehicle    |   +-------------------+              |
|  | 6. Authenticate   |                                     |
|  | 7. Start Engine   |   +-------------------+              |
|  | 8. View Alerts    |   |   INTRUDER       |              |
|  | 9. Share Key      |   +-------------------+              |
|  |10. Manage Veh.    |   | 1. Break Window  |              |
|  +-------------------+   | 2. Rip Camera    |              |
|           |              | 3. Hotwire       |              |
|           v              | 4. Attempt Start |              |
|  +--------------------------------------------------+      |
|  |                 VSHIELD BRAIN                     |      |
|  |  - Camera Module (Face Capture)                   |      |
|  |  - Fingerprint Sensor                             |      |
|  |  - Starter Relay (Engine Kill)                    |      |
|  |  - Fuel Pump Relay (Immobilizer)                  |      |
|  |  - Tamper Detection (Physical + Software)         |      |
|  +--------------------------------------------------+      |
|           |                                               |
|           v                                               |
|  +--------------------------------------------------+      |
|  |              AI ENGINE (Gemini)                   |      |
|  |  - Threat Detection & Prediction                  |      |
|  |  - Facial Recognition                             |      |
|  |  - Distraction Detection                          |      |
|  |  - Route Pattern Analysis                         |      |
|  +--------------------------------------------------+      |
|                                                             |
+=============================================================+
```

### Use Case Relationships

| Relationship | Description |
|--------------|-------------|
| **Authenticate → Register Face** | <<include>> Must have registered face |
| **Authenticate → Register FP** | <<include>> Must have registered fingerprint |
| **Arm Vehicle → Add Vehicle** | <<include>> Must have added vehicle first |
| **Start Engine → Authenticate** | <<include>> Must authenticate first |
| **Detect Tamper → Immobilize** | <<extend>> If tamper detected, immobilize |
| **Detect Tamper → Send Alert** | <<extend>> If tamper detected, alert owner |
| **Break Window → Detect Tamper** | <<trigger>> Window break triggers detection |
| **Rip Camera → Detect Tamper** | <<trigger>> Camera removal triggers detection |

---

## 5. AI Features (Google Gemini Integration)

### AI Feature 1: Predictive Threat Detection

Uses Google Gemini to analyze vehicle context and predict theft risk.

```python
class ThreatDetector:
    def __init__(self):
        self.model = genai.GenerativeModel('gemini-1.5-pro')
    
    def analyze_context(self, location, time, movement_pattern):
        prompt = f"""
        Analyze security context:
        Location: {location}
        Time: {time}
        Movement: {movement_pattern}
        Return JSON: {{"risk_score": 0-1, "reasoning": string, "recommendation": string}}
        """
        result = self.model.generate_content(prompt)
        return json.loads(result.text)
```

### AI Feature 2: Facial Recognition

Uses Google Gemini Vision for driver verification.

```python
def verify_driver(face_image, registered_hash):
    model = genai.GenerativeModel('gemini-1.5-pro-vision')
    result = model.generate_content([
        "Compare this face with registered hash. Return match: true/false, confidence: 0-1",
        {"inline_data": {"data": face_image, "mime_type": "image/jpeg"}}
    ])
    return json.loads(result.text)
```

### AI Feature 3: Driver Distraction Detection

Detects phone usage, fatigue, and seatbelt compliance.

### AI Feature 4: Smart Geofencing

AI-powered boundary monitoring with anomaly detection.

### AI Feature 5: Crowd Threat Verification

For events with 50,000+ attendees, verifies threats using crowdsourced phone data.

---

## 6. Technical Architecture

### System Architecture

```
+---------------------------------------------------------+
|               MOBILE APP (React Native)                  |
|  - Dashboard  - Vehicle Control  - Biometric Setup      |
|  - Fleet Mgt  - Alerts          - Key Sharing           |
+-------------------------+-------------------------------+
                          | BLE/NFC (Offline)
                          v
+---------------------------------------------------------+
|              VSHIELD BRAIN (ESP32-S3)                    |
|  - Camera (OV5640)  - Fingerprint (GT-521F52)           |
|  - Relays (Starter + Fuel)  - Tamper Detection           |
|  - Supercapacitor Backup (5 sec)                        |
+-------------------------+-------------------------------+
                          | Optional
                          v
+---------------------------------------------------------+
|              BACKEND (Node.js + PostgreSQL)              |
|  - Auth Service  - Fleet Management  - AI Processing     |
|  - Redis Cache   - Twilio SMS       - FCM Push          |
+-------------------------+-------------------------------+
                          |
                          v
+---------------------------------------------------------+
|              AI ENGINE (Google Gemini)                   |
|  - Threat Detection  - Facial Recognition               |
|  - Distraction Detection  - Route Analysis              |
+---------------------------------------------------------+
```

### Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| Mobile | React Native | Cross-platform app |
| Backend | Node.js + Express | API server |
| AI | Google Gemini 1.5 Pro | Threat detection, vision |
| Database | PostgreSQL | User, vehicle, log data |
| Cache | Redis | Real-time status caching |
| Hardware | ESP32-S3 | Vehicle brain |
| Cloud | Google Cloud Platform | Hosting, AI models |
| Notifications | Firebase + Twilio | Push + SMS alerts |

---

## 7. Database Schema

### Core Tables

```sql
-- Users
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(20) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    fcm_token VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW()
);

-- Vehicles
CREATE TABLE vehicles (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    plate_number VARCHAR(20) NOT NULL,
    make VARCHAR(50) NOT NULL,
    model VARCHAR(50) NOT NULL,
    year INTEGER NOT NULL,
    status VARCHAR(20) DEFAULT 'park',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    UNIQUE(user_id, plate_number)
);

-- Biometrics (stored as hashed data only)
CREATE TABLE biometrics (
    id SERIAL PRIMARY KEY,
    vehicle_id INTEGER REFERENCES vehicles(id) ON DELETE CASCADE,
    biometric_type VARCHAR(20) NOT NULL, -- face, fingerprint
    data_hash TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    UNIQUE(vehicle_id, biometric_type)
);

-- Threat Analyses (Gemini results)
CREATE TABLE threat_analyses (
    id SERIAL PRIMARY KEY,
    vehicle_id INTEGER REFERENCES vehicles(id) ON DELETE CASCADE,
    location VARCHAR(255),
    risk_score DECIMAL(3,2),
    risk_level VARCHAR(20),
    reasoning TEXT,
    recommendation VARCHAR(20),
    analysis_data JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Authentication Logs
CREATE TABLE authentication_logs (
    id SERIAL PRIMARY KEY,
    vehicle_id INTEGER REFERENCES vehicles(id) ON DELETE CASCADE,
    success BOOLEAN DEFAULT FALSE,
    face_match BOOLEAN DEFAULT FALSE,
    fingerprint_match BOOLEAN DEFAULT FALSE,
    timestamp TIMESTAMP DEFAULT NOW()
);

-- Key Shares (Digital key sharing)
CREATE TABLE key_shares (
    id SERIAL PRIMARY KEY,
    vehicle_id INTEGER REFERENCES vehicles(id) ON DELETE CASCADE,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    access_level VARCHAR(20),
    expires_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    UNIQUE(vehicle_id, user_id)
);
```

---

## 8. API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login user |
| GET | `/api/auth/me` | Get user profile |

### Vehicle Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/vehicles` | Add vehicle |
| GET | `/api/vehicles` | Get all vehicles |
| GET | `/api/vehicles/:id` | Get vehicle details |
| PUT | `/api/vehicles/:id` | Update vehicle |
| DELETE | `/api/vehicles/:id` | Delete vehicle |

### Biometrics

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/biometrics/face/:vehicleId` | Register face |
| POST | `/api/biometrics/fingerprint/:vehicleId` | Register fingerprint |
| POST | `/api/biometrics/verify/:vehicleId` | Verify biometrics |

### AI & Commands

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/ai/analyze-threat` | Analyze threat context |
| POST | `/api/ai/crowd-verify` | Crowd threat verification |
| POST | `/api/ai/distraction` | Driver distraction detection |
| POST | `/api/brain/command/:vehicleId` | Send command to VShield Brain |
| GET | `/api/dashboard/stats` | Dashboard statistics |

---

## 9. Hardware Specifications

### VShield Brain Components

| Component | Specification | Function |
|-----------|---------------|----------|
| **Microcontroller** | ESP32-S3 | Main processor, Bluetooth 5.0 |
| **Camera** | OV5640 | Facial recognition, night vision |
| **Fingerprint** | GT-521F52 | Fingerprint authentication |
| **Relays** | 2x Latching (30A) | Starter + Fuel pump kill |
| **Backup** | 5F Supercapacitor | 5-second tamper routine |
| **Secure Element** | ATECC608A | Cryptographic key storage |
| **IMU** | MPU-6050 | Movement/tamper detection |
| **SD Card** | MicroSD | Local video storage |

### Key Pin Mapping

```
ESP32-S3 → Camera (GPIO 4-21)
ESP32-S3 → Fingerprint (GPIO 2,3)
ESP32-S3 → Relay 1 (GPIO 22) - Starter
ESP32-S3 → Relay 2 (GPIO 23) - Fuel Pump
ESP32-S3 → Tamper Switch (GPIO 36)
ESP32-S3 → IMU (GPIO 32,33)
ESP32-S3 → SD Card (GPIO 4)
```

### Firmware State Machine

```
IDLE → ARMED → ALERT → IMMOBILIZED
IDLE → AUTHENTICATING → DRIVING → IDLE
ARMED → TAMPER_DETECTED → IMMOBILIZED
DRIVING → TAMPER_DETECTED → IMMOBILIZED
```

---

## 10. Security & Privacy

### 4-Layer Security Architecture

| Layer | Security Measures |
|-------|-------------------|
| **Physical** | Tamper-proof housing, breakaway mount, supercapacitor backup |
| **Hardware** | Secure boot, encrypted BLE, ATECC608A crypto chip |
| **Application** | JWT authentication, challenge-response protocol, biometric hashing |
| **Cloud** | AES-256 encryption, TLS 1.3, zero-knowledge architecture |

### Privacy Principles

- Biometric data is **hashed and encrypted on-device** - never stored raw
- Raw biometric data **never leaves** the phone or VShield Brain
- No biometric data is stored in the cloud
- Users can request **data deletion** at any time
- Full compliance with **NDPR (Nigeria Data Protection Regulation)**

### Challenge-Response Authentication (Offline)

```
1. VShield Brain generates 6-digit random challenge
2. Brain sends challenge via BLE to phone
3. Phone encrypts challenge using biometric hash
4. Phone sends response back via BLE
5. Brain verifies response using secure element
6. If valid → Engage relays → Start engine
7. If invalid → Immobilize → Alert owner
```

---

## 11. Go-to-Market Strategy

### Target Market - Nigeria

| Segment | Description | Size |
|---------|-------------|------|
| **Personal** | Urban professionals in Lagos, Abuja, PH | Largest segment |
| **Family** | Multi-vehicle households | Growing |
| **Fleet** | Logistics, delivery, corporate fleets | High-value |
| **Corporate** | Banks, telecoms, insurance companies | Strategic |

### Pricing Strategy (Naira)

| Plan | Price | Features |
|------|-------|----------|
| **Personal** | ₦50,000 | 1 vehicle, biometrics, tamper-proof |
| **Family** | ₦120,000 | 3 vehicles, key sharing, biometrics |
| **Fleet** | Custom | Unlimited vehicles, fleet dashboard, API |

### Distribution Channels

1. **Online Sales:** Website with payment integration
2. **Auto Dealerships:** Partnerships with Toyota, Honda, Kia Nigeria
3. **Insurance Partners:** Bundled with vehicle insurance
4. **Corporate Sales:** B2B fleet solutions

### Marketing Strategy

- **Social Media:** Instagram, Facebook, Twitter (targeting vehicle owners)
- **Influencers:** Nigerian auto influencers and tech reviewers
- **Events:** Auto shows, trade fairs, conferences
- **Referrals:** Discount programs for referrals
- **Insurance:** Co-marketing with insurance providers

---

## 12. Google Africa Applied AI Lab Application Checklist

| Requirement | Status | How VShield Meets It |
|-------------|--------|---------------------|
| **Use Google AI** | ✅ | Gemini 1.5 Pro for threat detection, facial recognition, distraction detection |
| **Drive Impact in Africa** | ✅ | Addresses Nigeria's vehicle theft crisis affecting thousands annually |
| **Software Development Theme** | ✅ | Complete full-stack application with AI integration |
| **Technical Proficiency** | ✅ | Demonstrated through complete code implementation |
| **Application Deadline** | August 31, 2026 | ✅ Ready for submission |

### Why VShield for Google Africa Applied AI Lab

1. **Real Problem, Real Solution:** Vehicle theft is a daily reality for millions of Nigerians
2. **Google AI Integration:** Uses Gemini for threat detection and facial recognition
3. **African Context:** Designed for Nigeria's connectivity challenges (offline operation)
4. **Technical Excellence:** Full-stack implementation with hardware integration
5. **Scalability:** Works for individuals, families, and fleets

---

## 13. Conclusion

VShield is a comprehensive AI-powered vehicle security solution designed specifically for the Nigerian market. By leveraging Google Gemini AI, it provides advanced threat detection, biometric authentication, and tamper-proof security that works offline—a critical feature for Nigeria's connectivity landscape.

The application addresses a real and pressing problem in Nigeria, aligns with Google's AI for social impact mission, and demonstrates technical proficiency through complete implementation of both software and hardware components.

**Application Summary:**
- ✅ Problem: Vehicle theft in Nigeria (1,500+ reported annually)
- ✅ Solution: AI-powered biometric vehicle immobilizer
- ✅ Google AI: Gemini 1.5 Pro + Vision
- ✅ Technology: React Native + Node.js + ESP32
- ✅ Market: Nigeria (personal, family, fleet)
- ✅ Impact: Reduced vehicle theft, safer communities

---

**Team Information:**

| Name | Role | LinkedIn | GitHub |
|------|------|----------|--------|
| [Your Name] | [Your Role] | [Your LinkedIn] | [Your GitHub] |

---

**Contact Information:**
- Email: [your-email]
- Phone: [your-phone]
- Website: [your-website]

---

**VShield - Securing Nigeria's roads, one vehicle at a time.** 🇳🇬

---

*Document Version: 1.0*
*Date: August 2026*
