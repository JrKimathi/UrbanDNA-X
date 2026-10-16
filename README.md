# UrbanDNA X

### The City Doctor for the Built Environment

Infrastructure intelligence platform that connects citizens, GIS, AI, and authorities to keep cities safe.

[![Expo SDK](https://img.shields.io/badge/Expo-54.0-000020?logo=expo)](https://expo.dev)
[![React Native](https://img.shields.io/badge/React%20Native-0.81-61DAFB?logo=react)](https://reactnative.dev)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?logo=fastapi)](https://fastapi.tiangolo.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15%20%2B%20PostGIS-336791?logo=postgresql)](https://www.postgresql.org)
[![Firebase](https://img.shields.io/badge/Firebase-Auth%20%2B%20Firestore-FFCA28?logo=firebase)](https://firebase.google.com)
[![Google Cloud](https://img.shields.io/badge/Google%20Cloud-Run%20%2B%20SQL-4285F4?logo=googlecloud)](https://cloud.google.com)

[![Latest Release](https://img.shields.io/github/v/release/JrKimathi/UrbanDNA-X?color=007AFF&label=latest%20release)](https://github.com/JrKimathi/UrbanDNA-X/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/JrKimathi/UrbanDNA-X/total?color=28a745)](https://github.com/JrKimathi/UrbanDNA-X/releases)

---

## Download the App

> **Ready to try UrbanDNA X on your Android phone?**

> **[Download the latest APK](https://github.com/JrKimathi/UrbanDNA-X/releases/download/v1.0.0/urbanDNA.apk)**


>
> **File:** `urbanDNA.apk` · **Size:** ~90 MB · **Requires:** Android 8.0 (Oreo) or later

### Installation

1. Tap the download link above on your Android phone.
2. If prompted, allow installation from this source.
3. Open the downloaded file and tap **Install**.
4. Launch **UrbanDNA X** and sign up.

> **Note:** You may see Android's "Install from unknown sources" warning because this APK is distributed outside the Play Store. This is normal for pre-release builds.

All versions: [view all releases →](https://github.com/JrKimathi/UrbanDNA-X/releases/download/v1.0.0/urbanDNA.apk)

---

## Table of Contents

1. [Overview](#overview)
2. [How It Works](#how-it-works)
3. [Features](#features)
4. [Architecture](#architecture)
5. [Technology Stack](#technology-stack)
6. [Getting Started](#getting-started)
7. [Roadmap](#roadmap)
8. [Acknowledgements](#acknowledgements)

---

## Overview

UrbanDNA X helps cities **observe, assess, prioritize, manage, and learn** from infrastructure conditions. It connects citizen observations, GIS data, AI, and engineering information to close the loop between reporting a problem and verifying the outcome.

The MVP focuses on **roads** and demonstrates one complete working loop from a citizen's report to a verified repair.

The architecture is intentionally generic, so bridges, buildings, drainage, and other infrastructure types can be added later without a rewrite.

---

## How It Works

```text
Citizen reports road problem
            |
            v
System identifies road asset (PostGIS)
            |
            v
Evidence is assessed (AI + engineer)
            |
            v
Issue receives preliminary priority
            |
            v
Authority manages intervention
            |
            v
Citizen tracks progress and provides feedback
```

---

## Features

### Citizens

- Report road issues through a 5-step wizard: category, photo, GPS, description, review
- Attach photos, stored in Google Cloud Storage
- Capture GPS automatically and match it to the nearest road segment with PostGIS
- Track each report through the full workflow
- View nearby reports on an interactive map
- Give feedback on the outcome after resolution

### Engineers

- Dashboard with KPI overview of reports and interventions
- Browse all reports with status and category filters plus search
- Verify reports and review evidence
- Schedule inspections and set preliminary priority
- Explore an infrastructure map showing reports and assets

### Admins

- System-wide dashboard with reports grouped by status
- Full asset management: create, edit, and delete assets with photos
- User management with role changes between citizen, engineer, and admin
- Intervention lifecycle management: create, assign, complete, and verify outcome
- Category management
- Audit log of all admin actions

---

## Architecture

```text
                +-----------------------------+
                |         MOBILE APP          |
                |   React Native + Expo SDK   |
                |    Firebase Auth (client)   |
                +--------------+--------------+
                               |
              +----------------+----------------+
              |                |                |
         HTTPS/REST       Firebase SDK     Firestore SDK
              |                |                |
              v                v                v
     +----------------+  +-----------+  +--------------+
     |   CLOUD RUN    |  | Firebase  |  |  Firestore   |
     | FastAPI Backend|  |   Auth    |  |   (mirror)   |
     +-------+--------+  +-----------+  +--------------+
             |
     +-------+---------+---------------+
     |       |         |               |
     v       v         v               v
 +--------+ +-------+ +-----------+ +-----------------+
 |Cloud   | |  GCS  | | Firebase  | | Secret Manager  |
 |SQL +   | |(media)| | Admin SDK | |                 |
 |PostGIS | +-------+ | (claims)  | +-----------------+
 +--------+           +-----------+
```

---

## Technology Stack

| Layer | Technology |
|---|---|
| Mobile | React Native 0.81, Expo SDK 54, TypeScript |
| Navigation | React Navigation v7 (Stack and Bottom Tabs) |
| State | Zustand 4.4 |
| Auth | Firebase Auth (Email/Password and Google) |
| Backend | FastAPI 0.115, Python 3.11 |
| ORM and migrations | SQLAlchemy 2.0, Alembic |
| Database | PostgreSQL 15 with PostGIS 3.6 |
| Storage | Google Cloud Storage |
| Hosting | Google Cloud Run and Cloud SQL |
| Maps | react-native-maps (Google Maps and Apple Maps) |
| Media and location | expo-image-picker, expo-location |

---

## Getting Started
Download the .apk and install it on any Android device.

## Roadmap

Planned capabilities beyond the MVP:

- [ ] Real-time push notifications (Firebase Cloud Messaging)
- [ ] Support for bridges, buildings, and drainage assets
- [ ] Real image classification model (fine-tuned MobileNet)
- [ ] Duplicate report clustering (PostGIS and embeddings)
- [ ] Signed URLs for GCS media, replacing public read
- [ ] SMS and USSD reporting channel
- [ ] Offline-first mobile support (SQLite queue)
- [ ] Digital-twin visualisation (3D city)
- [ ] Predictive maintenance analytics
- [ ] Public API for third-party city integrations

---

## Acknowledgements

- **PostGIS** for world-class geospatial tooling
- **FastAPI** for making Python APIs a joy to build
- **Expo** for making React Native accessible
- **Firebase** for serverless auth and identity
- **Google Cloud** for the serverless infrastructure
- The citizens and city engineers whose feedback shaped this MVP
