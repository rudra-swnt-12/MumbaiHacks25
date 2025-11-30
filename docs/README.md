# Arogya Saathi

Arogya Saathi is an autonomous, voice-first health ecosystem designed to bridge the digital divide for rural populations. The system enables patients to interact with AI medical agents via standard telephony, utilizing acoustic biomarkers for risk detection and autonomous protocols for emergency escalation.

## Problem Statement

Traditional telemedicine relies on smartphones, internet access, and literacy—barriers that exclude approximately 800 million rural Indians. Critical conditions often go undetected due to the inability to navigate complex digital interfaces during emergencies.

## Core Solution

A software-only infrastructure that transforms standard phone calls into medical lifelines. The system utilizes a multi-agent AI swarm to handle patient onboarding, symptom triage, and medical record generation without requiring apps or hardware on the patient side.

## Key Features

1. **Phygital Bridge:** Connectivity via standard PSTN telephony using Twilio, requiring no internet or smartphone for the patient.
2. **Acoustic Biomarkers:** Real-time analysis of raw audio to detect physiological indicators (e.g., dysarthria/slurred speech) indicating stroke or neurological distress.
3. **Clinical Triangulation:** Logic-driven symptom mapping (e.g., Polyuria + Polydipsia) to infer vital risks like hyperglycemia.
4. **Autonomous L2 Escalation:** Automatic triggering of SMS alerts to community contacts upon detection of critical biomarkers.
5. **Automated SOAP Scribing:** Post-call generation of structured medical notes (Subjective, Objective, Assessment, Plan) for doctor review.

## Technology Stack

* **Orchestration:** Python (FastAPI), AsyncIO
* **Telephony:** Twilio Programmable Voice
* **Speech Pipeline:** Deepgram Nova-2 (STT), ElevenLabs (TTS)
* **Intelligence:** Groq (Llama-3.1-8b)
* **Signal Processing:** Librosa
* **Database:** PostgreSQL (Supabase)
* **Frontend:** React, Vite, TypeScript

## Repository Structure

* `backend/`: FastAPI application containing the agent swarm, websocket routers, and database logic.
* `frontend/`: React application for the Doctor Portal and administration dashboard.

## Quick Start

For detailed installation instructions, please refer to the README files located in the `backend` and `frontend` directories respectively.

### Prerequisites

* Python 3.12+
* Node.js 18+
* Twilio Account (SID/Auth Token)
* Supabase Project
* Deepgram & ElevenLabs API Keys
* Groq API Key

### Deployment Overview

1. Initialize and seed the PostgreSQL database.
2. Start the FastAPI backend server.
3. Establish an Ngrok tunnel to expose the local WebSocket.
4. Configure the Twilio Webhook to point to the Ngrok URL.
5. Launch the React frontend.

## License

Proprietary and Confidential.
