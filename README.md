# Rapid Crisis Response  by CodingChai
## Real-time Emergency Coordination Across Users, Hotels, and Emergency Services
### Built by [@NiyaSingh](https://github.com/NiyaSinghShekhawat), [@SampradaReddy](https://github.com/SampradaReddy) and [@ShreyanSamal](https://github.com/Shreyan2745)


Rapid Crisis Response is a multi-dashboard emergency response platform designed for **speed, coordination, and life-saving escalation**.  
It connects three stakeholders in one live workflow:

- **User Dashboard** (where emergencies are raised) [Access GitHub](https://github.com/SampradaReddy/User-end-Emeregency-app)
- **Hotel Dashboard** (where incidents are acknowledged and managed) [Access GitHub](https://github.com/NiyaSinghShekhawat/HotelDash)
- **Emergency Services Dashboard** (where police/hospital/fire teams receive escalations) [Access GitHub](https://github.com/Shreyan2745/emergency-response-dashboard)

The goal is simple: **reduce response time and coordination failure during critical incidents**.

---

## Why This Project Matters

In emergencies, delays happen because:
- people cannot provide full information immediately,
- alerts do not reach the right team fast enough,
- hotel teams and public responders work in disconnected systems,
- ownership and status are unclear across stakeholders.

Rapid Crisis Response addresses this by enabling:
1. **Minimal-input emergency reporting**
2. **Real-time shared incident visibility**
3. **Severity-based auto-escalation to authorities**
4. **Clear assignment and resolution lifecycle**

---

## Core Idea in One Line

> **Report fast with minimal details, enrich later, and coordinate everyone through one live incident record.**

---

## Dashboards Overview

## 1) User Dashboard (Incident Intake)

This is the first touchpoint where an emergency is created.

### User can submit:
- **Location** *(required)*
- **Emergency type** *(required)*
- **Severity: Major / Minor** *(required)*
- **Additional details** *(optional)*

### Design philosophy:
- Keep friction low during panic situations.
- Don’t block emergency creation if full details are unavailable.

### Output:
- Emergency is created in Firebase (`distressCalls`) and immediately visible to other dashboards.

---

## 2) Hotel Dashboard (Operational Control)

This repository contains the hotel-side dashboard, the operational command center for internal responders.

### Hotel team can:
- View incoming incidents in real time
- Acknowledge alerts
- Add/complete missing guest and contact details
- Track incident status and response progress
- Coordinate with assigned external authorities (for major cases)
- Mark incidents as resolved

### Why this is critical:
Hotels often become the first organized response layer before police/medical teams arrive.  
This dashboard enables immediate local action while maintaining synchronization with external responders.

---

## 3) Emergency Services Dashboard (External Response)

This dashboard is used by police/hospital/fire response teams.

### For major incidents:
- Teams receive dispatch alerts
- One authority can accept the case
- Assignment is locked to avoid duplicate/conflicting ownership
- Assignment status syncs back to all dashboards

### Benefit:
Creates a single source of truth for **who is responding, when they accepted, and current case status**.

---

## End-to-End Process Flow

1. User submits emergency with minimum required fields  
2. Emergency is stored in Firestore (`distressCalls`)  
3. Incident is streamed live to hotel and emergency services dashboards  
4. Hotel acknowledges and starts local response  
5. Hotel enriches missing details if needed  
6. System checks severity:
   - **Minor** -> handled primarily by hotel team  
   - **Major** -> automatic authority dispatch is triggered  
7. Authority accepts dispatch (first accept wins)  
8. Hotel + authority coordinate response  
9. Incident is marked resolved and timeline is preserved

---

## Key Features

- **Tri-dashboard architecture** for role-based coordination
- **Real-time incident sync** across all stakeholders
- **Severity-aware escalation logic**
- **Progressive data capture** (report now, enrich later)
- **Authority dispatch + acceptance workflow**
- **Case lifecycle tracking** (`Active -> Assigned -> Resolved`)
- **Timestamped accountability** for audit and transparency
- **Scalable cloud backend with Firebase**

---

## USP (Unique Selling Proposition)

Rapid Crisis Response combines:
- **low-friction emergency intake**,  
- **live multi-party coordination**, and  
- **automatic major-incident escalation**  

into a single emergency operations platform tailored for hospitality and shared infrastructures.

Unlike traditional hotline-only systems or single-department tools, this solution provides a **continuous, synchronized response loop** from reporting to closure.

---

## Technical Architecture (High Level)

### Client Layer
- User Dashboard
- Hotel Dashboard
- Emergency Services Dashboard

### Backend Layer
- Firebase Firestore (real-time data store)
- Firebase Authentication (role-based access, optional/expandable)
- Cloud Functions (optional for advanced dispatch automation)
- FCM / notification services (optional for push alerts)

### Data Layer
- `distressCalls` (primary incident collection)
- `messages` subcollection (optional communication timeline)
- assignment fields, authorities metadata, timestamps, status fields

---

## Data Model (Conceptual)

Each emergency record includes:
- `id`
- `location`
- `type`
- `severity` (`major` / `minor`)
- `status` (`active` / `assigned` / `resolved`)
- `timestamp` / `completedAt`
- `additionalInfo` (notes + guest details)
- `targetAuthorities` (for major escalations)
- `assignment` (accepted responder details)

---

## Problem-Solution Fit

### Problem
Emergency response in hotels often suffers from:
- fragmented communication,
- delayed escalation,
- incomplete first reports,
- unclear ownership.

### Solution
A real-time coordination platform that:
- captures incidents quickly,
- shares them instantly,
- escalates major events automatically,
- and tracks responsibility through closure.

### Impact
- Lower response latency
- Better coordination quality
- Higher operational clarity
- Improved chance of timely life-saving intervention

---

## Current Scope

This codebase focuses on the **Hotel Dashboard**, including:
- live incident subscription,
- emergency listing and detail views,
- acknowledgement/handling UI,
- reporter details enrichment,
- resolution flow integration.

---

## Future Enhancements

- Geo-mapped incident visualization
- SLA timer and breach alerts
- Automated call/SMS integration to authorities
- Incident analytics dashboard (response time, closure rate)
- Multi-property / chain-wide tenant support
- AI-assisted severity recommendation (optional)

---

## Setup (Development)

> Ensure environment variables are configured for Firebase before running.

### Commands
```bash
npm install
npm run dev
npm run build
