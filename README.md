# 🛡️ SAATHI (साथी) — Real-Time Emergency Helpline Decision Support

<div align="center">

[![Test Suite](https://img.shields.io/badge/Safety_Suite-21%2F21_PASS_(100%25)-059669?style=for-the-badge&logo=checkmarx&logoColor=white)](#-automated-safety-acceptance-tests)
[![DPDP Act Compliant](https://img.shields.io/badge/DPDP_Act_2023-COMPLIANT-2563EB?style=for-the-badge&logo=shield&logoColor=white)](#-privacy--dpdp-act-2023-compliance)
[![React](https://img.shields.io/badge/React_19-TypeScript-61DAFB?style=for-the-badge&logo=react&logoColor=black)](#-system-architecture)
[![Android Ready](https://img.shields.io/badge/Capacitor_8-Android_APK-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#-mobile-app--android-apk)
[![Speech AI](https://img.shields.io/badge/Sarvam_AI-Bilingual_Hinglish-FF6B6B?style=for-the-badge&logo=openai&logoColor=white)](#-streaming-hinglish-speech-intelligence)
[![Build](https://img.shields.io/badge/Vite_8-Production_Verified-8B5CF6?style=for-the-badge&logo=vite&logoColor=white)](#-getting-started)

**Next-Generation Computer-Aided Dispatch (CAD) Decision Support & Silent Citizen Distress Platform for India's 181 Women Helpline & 112 ERSS.**

*Built for the caller who cannot say it out loud.*

[Explore Architecture](#-system-architecture) • [Core Innovations](#-core-innovations) • [Citizen & CAD Workflows](#-dual-persona-system) • [Running Tests](#-automated-safety-acceptance-tests) • [Android Setup](#-mobile-app--android-apk)

</div>

---

## 📌 The Problem & Opening Pitch

> *"When a woman calls 181, the person she fears may be standing right next to her. She whispers, she speaks in code, or she claims 'sab theek hai' under duress. Most emergency dispatch systems fail because they only process what a caller articulates explicitly. **SAATHI is engineered for the caller who cannot speak freely.**"*

In high-stakes domestic violence and stalking emergencies:
- **Legacy CAD is reactive:** Operators are forced to ask intrusive, identifying questions (*"Who is hurting you? Speak louder."*) that immediately endanger the caller.
- **Duress causes false de-escalation:** An abuser enters the room, the victim hastily says *"galti se lag gaya, sab theek hai"*, and legacy systems downgrade or close the ticket.
- **Fragmented location data:** Callers in distress speak in hyper-local colloquial landmarks (*"Peele school ke peeche, gali 4"*) rather than formal postal addresses.
- **Connectivity drop-offs:** Cellular data disconnects in basements, elevators, or rural fringes, leaving victims stranded without fallback communication.

**SAATHI solves all four failure modes** through deterministic safety invariants, real-time Hinglish speech processing, coded-call detection, and zero-internet emergency fallbacks.

---

## 💡 Core Innovations

### 1. 🍕 Coded-Call Pattern Recognition
Under intimate partner surveillance, callers often disguise their distress as mundane interactions—such as ordering food (*"Bhaiya ek paneer roll bhej do, address wahi hai"*), calling an imaginary relative, or making an appointment.
- **Instant Pattern Match:** Detects conversational discrepancies and flags the incident as **Possible Coded Call (P2 Urgent)**.
- **Tactical Operator Guidance:** CAD immediately instructs the operator: *"She may not be able to speak freely. Do not repeat her words back or ask her to explain. Use yes/no questions only."*
- **Discreet Safe Inquiries:** Prompts safe, single-touch questions to verify danger without blowing her cover.

### 2. 🔒 Invariant Urgency Floors (Anti-Duress Lock)
In domestic violence situations, threat levels can never be safely downgraded based on verbal denial alone.
- **Hard Danger Invariant:** Once hard evidence of violence (e.g. `chaku` / weapon, physical assault, forced perimeter breach, threat to life) is recognized, an **irreversible priority floor (P1 Immediate / P2 Urgent)** is locked.
- **Denial Resistance:** If the caller subsequently says *"nahi nahi, sab theek hai"* or abruptly goes silent, the priority floor **remains locked at P1**.
- **Contradiction Registry:** The system flags the denial as an active contradiction (*"Floor held: A later denial does not undo a weapon disclosure"*) and records it in the immutable audit trail.

### 3. 🚦 SafeSignal Protocol (10 Invariant Question Safety Rules)
Every automated prompt and operator suggestion is vetted through strict programmatic safety guardrails before display:

| Rule | Guardrail Invariant | Purpose |
| :--- | :--- | :--- |
| **R1** | **Strict Yes/No Only** | Caller must answer with 1 tap or a single binary whisper. |
| **R2** | **Length Cap (≤ 14 Words)** | Prevents cognitive overload during adrenaline surges. |
| **R3** | **No Abuser or Weapon Names** | Never asks *"Did your husband bring a knife?"* to prevent provoking the abuser. |
| **R4** | **No Movement or Volume Commands** | Strictly forbids *"Speak louder"* or *"Run outside"*, which causes physical harm. |
| **R5** | **No Unsafe Callback / SMS Promises** | Never sends unprompted return calls or SMS that can be discovered on her screen. |
| **R6** | **Single Question at a Time** | Zero compound or confusing questions. |
| **R7** | **Zero Explicit PII in Questions** | Masks caller names, phone numbers, and identifying details. |
| **R8** | **No Unverified Promises of Arrival** | CAD reports transparent dispatch status (*"Units notified"*, never false guarantees). |
| **R9** | **Plain Hinglish / Roman Script** | Matches spoken cadences without bureaucratic jargon. |
| **R10**| **Explicit Safety Escalation** | Every query contains a clear, safe route to request immediate police intervention. |

### 4. 🎙️ Streaming Hinglish Speech Intelligence
- **34 Emergency Categories:** Deep lexical coverage across Hindi, Urdu, Punjabi, and Roman Hinglish (physical violence, stalking, forced confinement, child endangerment, legal aid, medical trauma).
- **Conversational Transliteration:** Handles natural spoken phonetic variants (`wo`, `ye`, `maarra`, `chaku`, `bachao`, `darwaza peet raha`).
- **Hybrid STT Engine:** Browser Web Speech API for zero-lag instant rendering, paired with Sarvam AI (`saaras:v4` / `saarika:v2`) for high-fidelity bilingual phonetic capture.

---

## 🏛️ System Architecture

```
+----------------------------------------------------------------------------------------------------+
|                                    CITIZEN SMARTPHONE PLATFORM                                     |
|   * Progressive Web App (PWA) + Native Android Bridge (Capacitor 8)                                |
|   * Stealth Disguise Calculator Screen · Silent Emergency SOS (3s Hold)                            |
|   * Live Voice Waveform Stream · 1-Tap "Haan" / "Nahi" Responses · Live GPS Pinning                |
+----------------------------------------------------------------------------------------------------+
                         |                                              |
               (Continuous Audio Stream)                         (Encrypted JSON / GPS)
                         v                                              v
+------------------------------------------------+     +---------------------------------------------+
|            SPEECH INGESTION ADAPTER            |     |         STATE SYNCHRONIZATION GATEWAY       |
|  * Chromium Web Speech (Zero-Latency Local)    |     |  * Bi-directional State Sync (MQTT / WS)    |
|  * Sarvam AI Bilingual STT (saaras:v4)         |     |  * High-Accuracy Geolocation Tracker        |
+------------------------------------------------+     +---------------------------------------------+
                         \                                             /
                          \---------------------+---------------------/
                                                |
                                                v
+----------------------------------------------------------------------------------------------------+
|                                  SAATHI REAL-TIME TRIAGE ENGINE                                     |
|  1. Hinglish Lexical Normalizer (Root Words, Contraction Variants, Smart Normalization)            |
|  2. Coded-Call Pattern Matcher (Disguised food orders, false numbers, whispers)                    |
|  3. Monotonic Urgency Floor Guardrail (Anti-duress denial lock, immutable priority floor)           |
|  4. Tactical Landmark & Address Parser (Colony, gali, landmark, pin code resolution)               |
|  5. Incident Continuity Engine (Caller hash pattern correlation across historical dockets)         |
+----------------------------------------------------------------------------------------------------+
                                                |
                                                v
+----------------------------------------------------------------------------------------------------+
|                                 OPERATOR CAD WORKSTATION CONSOLE                                   |
|  Col 1: Live Ingestion & Audio   ·  Col 2: Real-Time Triage & SafeSignal  ·  Col 3: Tactical Map   |
|  Multi-Agency Dispatch Handoff:  Police 112 · Ambulance 108 · Shelter 181 OSC · DLSA Legal Aid   |
|  Incident Continuity Modal       ·  Stress Lab Testing Sandbox            ·  Shift Wallboard       |
+----------------------------------------------------------------------------------------------------+
```

---

## 👥 Dual-Persona System

### 📱 1. Citizen Smartphone App (User Device)
Designed for extreme stealth, immediate action, and complete safety when under active surveillance:
- **Disguise Calculator Mode:** Tap "Quick Exit" to immediately mask the application into a functional digital calculator.
- **Silent Distress Chat:** Conversational interface with zero audio output, zero vibration, and high-contrast 1-touch **Haan / Nahi** response pills.
- **Hardware Trigger (Android):** Trigger silent microphone transmission in the background using hardware volume button shortcuts via Android Accessibility Services.
- **Zero-Internet Emergency Fallbacks:**
  - **Native SMS 112 URI:** Generates standard RFC 5724 pre-filled SMS messages with live GPS coordinates for 1-tap dispatch without cellular internet.
  - **WhatsApp SOS Mirroring:** Instant emergency transmission link dispatched directly to registered trusted guardians.

### 🖥️ 2. Operator CAD Decision-Support Console
Built to meet authentic Indian Government emergency dispatch standards (ERSS 112 / Delhi 181):
- **Column 1 — Ingestion Stream:** Live streaming transcription, acoustic distress indicators, caller verification, and audio playback.
- **Column 2 — Invariant Triage & SafeSignal:** Real-time threat classification, irreversible urgency badges (P1 Critical, P2 High, P3 Medium, P4 Routine), evidence quote linkages, and pre-screened SafeSignal question recommendations.
- **Column 3 — Tactical Map & Multi-Agency Dispatch:**
  - Interactive Leaflet / OpenStreetMap GIS showing live citizen location, accuracy radius, and nearest emergency facilities.
  - 1-Click coordinated dispatch to **Delhi Police 112**, **Ambulance 108**, **Sakhi One-Stop Centre 181**, and **DLSA Legal Aid**.
- **Incident Continuity Engine:** Automatically hashes caller phone numbers with HMAC-SHA256 to correlate repeat distress patterns across 30 days without exposing citizen PII to operators until verified.
- **Stress Lab Sandbox:** Allows supervisors and operators to stress-test the triage engine against edge cases (noise, dialect switching, duress reversals).

---

## 🧪 Automated Safety Acceptance Tests

SAATHI features a comprehensive, deterministic acceptance test suite validating 21 mission-critical safety rules and guardrails:

```bash
npm test
```

```
====================================================
RUNNING SAATHI EMERGENCY SAFETY ACCEPTANCE TESTS
====================================================

[Suite 1: Negation & Context Awareness]
  ✓ PASS: Recognizes past threat as safe & non-imminent (Negation Awareness)
  ✓ PASS: Recognizes active perimeter breach and forced entry as imminent emergency

[Suite 2: Safety Floor Guardrail Invariants]
  ✓ PASS: Safety Floor Rule SF-02 triggers on child present + perimeter breach (Enforced: CRITICAL)

[Suite 3: Human Priority Override]
  ✓ PASS: Human operator can override AI classification with logged audit trail

[Suite 4: Zero-Internet Emergency 112 Fallbacks]
  ✓ PASS: Native SMS 112 URI generated with prefilled reviewable body (RFC 5724)

[Suite 5: Verified Public Helplines Directory]
  ✓ PASS: Verified Indian emergency directory configured (112, 108, 1091, 181, 1098)

[Suite 6: Honest Delivery & Report Lifecycle]
  ✓ PASS: Report does not claim "Police notified" upon initial submission (Honest Delivery)
  ✓ PASS: Operator acknowledgment transitions state and syncs to citizen transparently

[Suite 7: Rate Limiting & Duplicate Detection]
  ✓ PASS: Rate limiting suppresses accidental rapid double clicks (<2s)

[Suite 8: Reference Engine & Lexicon Parity]
  ✓ PASS: Scenario 0 parses deterministically (direct physical violence)
  ✓ PASS: Scenario 1 parses deterministically (indirect coercion / coded call)
  ✓ PASS: Scenario 2 parses deterministically (non-emergency inquiry)
  ✓ PASS: Scenario 3 parses deterministically (interrupted call / unclear)
  ✓ PASS: Scenario 4 parses deterministically (denial under duress)
  ✓ PASS: Scenario 5 parses deterministically (stalking)
  ✓ PASS: Scenario 6 parses deterministically (legal query)
  ✓ PASS: Scenario 7 parses deterministically (indirect coercion)
  ✓ PASS: Scenario 8 parses deterministically (trafficking / confinement)

[Suite 9: Floor Invariant & Denial Resistance]
  ✓ PASS: Denial ("sab theek hai") after weapon disclosure cannot lower Critical floor

[Suite 10: SafeSignal 10 Rules Compliance]
  ✓ PASS: All predefined Hinglish SafeSignal bank questions pass all 10 safety rules
  ✓ PASS: All dangerous and identifying questions are blocked by the safety rules filter

====================================================
TOTAL ACCEPTANCE TESTS PASSED: 21 / 21 (100%)
====================================================
```

---

## 🔒 Privacy & DPDP Act 2023 Compliance

SAATHI is architected in accordance with India's **Digital Personal Data Protection (DPDP) Act 2023**:
- **Zero Raw PII Storage:** Caller phone numbers are masked in operator views by default (`+91 98*** **412`).
- **Cryptographic Hashing:** Identity cross-referencing for repeat harassment complaints uses one-way HMAC-SHA256 hashes with revolving daily salt.
- **Ephemeral Audio Blobs:** Raw audio recordings are stored in client-side IndexedDB with strict session-only retention, auto-purging upon incident docket closure.
- **Honest Delivery Protocol:** The system never displays fabricated status messages (*"Police on the way"*). State transitions only occur when an authorized operator verifies agency transmission.

---

## 🛠️ Tech Stack & Engineering Standards

| Layer | Technologies | Role & Highlights |
| :--- | :--- | :--- |
| **Frontend Core** | React 19, TypeScript, Vite 8 | Ultra-low latency UI, strict typing, zero CSS framework bloat. |
| **Mobile Layer** | Capacitor 8, Android SDK (Java) | Native Android bridge, SMS/WhatsApp intents, hardware accessibility trigger. |
| **Styling & Design** | Pure Vanilla CSS (Variables & Tokens) | GovTech high-contrast theme, semantic P1–P4 color tokens, zero neon fluff. |
| **Speech & AI** | Web Speech API, Sarvam AI (`saaras:v4`) | Real-time streaming bilingual STT, 34 emergency categories, phonetic normalizer. |
| **Mapping & GIS** | Leaflet, OpenStreetMap, Nominatim | Interactive tactical maps, caller GPS radius, nearby facility routing. |
| **Sync & Comms** | MQTT, WebSockets, IndexedDB | Cross-device citizen-to-CAD sync, offline queue, local report storage. |
| **Testing & Quality**| Node.js CJS Test Runners, Oxlint | 21/21 safety invariant unit tests, zero lint warnings. |

---

## 🚀 Getting Started

### Prerequisites
- **Node.js**: `v20.0.0` or higher
- **npm**: `v10.0.0` or higher

### 1. Clone & Install
```bash
git clone https://github.com/devdash01/Saathi-CAD.git
cd Saathi-CAD
npm install
```

### 2. Run Local Development Server
```bash
npm run dev
```
Navigate to `http://localhost:5173` to access both the Citizen Phone Pane and the Operator CAD Console side by side.

### 3. Run Test Suites
```bash
# Run the 21 Safety Acceptance Invariant tests
npm test

# Run the Emergency Contact & SMS/WhatsApp SOS tests
node test_emergency_contact.cjs
```

### 4. Build for Production
```bash
npm run build
```

---

## 📱 Mobile App & Android APK

Saathi can be compiled directly into a downloadable Android APK using Capacitor:

```bash
# 1. Build web assets and sync native Android bridge
npm run cap:sync

# 2. Open project in Android Studio
npm run cap:open

# 3. Or build headless debug APK via Gradle
cd android
./gradlew assembleDebug
```
The compiled APK will be generated at `android/app/build/outputs/apk/debug/app-debug.apk`.

---

