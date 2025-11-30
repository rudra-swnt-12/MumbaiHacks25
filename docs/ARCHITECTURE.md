# System Architecture

Arogya Saathi utilizes a low-latency, event-driven architecture designed to process voice data in real-time. The system is divided into three logical pillars.

## 1. The Phygital Bridge (Input Layer)

This layer handles the conversion of analog telephony signals into digital WebSocket streams.

* **Input:** Standard PSTN Phone Call.
* **Gateway:** Twilio Voice API receives the call and establishes a bi-directional media stream.
* **Transport:** Ngrok tunnels the secure WebSocket (WSS) traffic to the local FastAPI backend.
* **Router:** `call_socket.py` handles the raw audio bytes, managing buffering and stream synchronization.

## 2. The Agentic Swarm (Processing Layer)

This is the core intelligence engine running on the backend. It employs parallel processing to minimize latency (The "Fast Stack").

### Parallel Process A: Safety & Biomarkers

* **Component:** `audio_analysis.py` (Librosa)
* **Function:** Analyzing raw PCM bytes for jitter, shimmer, and pitch variance.
* **Trigger:** If anomalies (e.g., slurred speech) are detected, an interrupt signal is sent to the L2 Escalation module immediately, bypassing the conversational LLM.

### Parallel Process B: Conversational Intelligence

* **STT:** Deepgram Nova-2 converts audio to text with optimization for Hinglish code-mixing.
* **Semantic Cache:** An in-memory dictionary intercepts common phrases (greetings, confirmations) to provide sub-100ms responses.
* **LLM Router (Groq):** Routes the dialogue context to specific specialized agents:
  * **Onboarding Agent:** Uses strict Pydantic introspection to extract identity data (Name, Age, Location).
  * **Check-in Agent:** Executes clinical triangulation logic (3 Ps) to assess risk levels.
* **TTS:** ElevenLabs generates high-fidelity audio, streamed back to the telephony gateway.

### Parallel Process C: Post-Call Intelligence

* **Agent:** SOAP Scribe
* **Trigger:** WebSocket Disconnect event.
* **Function:** Aggregates the chat history and generates a structured clinical summary (SOAP Note) and calculates a numerical risk score.

## 3. Persistence & Action (Output Layer)

This layer ensures data durability and enables human-in-the-loop intervention.

* **Database (Supabase/PostgreSQL):** Stores patient profiles, consultation logs, and doctor configurations.
* **L2 Escalation Protocol:** Integrates with Twilio SMS to dispatch emergency alerts to registered next-of-kin or community leaders.
* **Doctor Portal:** A React-based dashboard that polls the database for real-time patient analytics and displays generated SOAP notes.
