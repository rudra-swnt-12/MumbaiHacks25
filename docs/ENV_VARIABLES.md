# Environment Configuration

The application requires the following environment variables to be set in the `backend/.env` file.

## Core Configuration

| Variable | Description | Required |
| :--- | :--- | :--- |
| `DATABASE_URL` | PostgreSQL connection string (Supabase transaction pooler). | Yes |
| `NGROK_URL` | Public HTTPS URL forwarding to localhost:8000 (for Twilio). | Yes |

## Intelligence Services

| Variable | Description | Service |
| :--- | :--- | :--- |
| `GROQ_API_KEY` | Access key for Llama-3 inference via LPU. | Groq |
| `DEEPGRAM_API_KEY` | Access key for Nova-2 Streaming STT. | Deepgram |
| `ELEVENLABS_API_KEY`| Access key for Neural TTS generation. | ElevenLabs |
| `ELEVENLABS_VOICE_ID`| Specific Voice ID (Model: eleven_multilingual_v2). | ElevenLabs |

## Telephony & Alerts

| Variable | Description | Service |
| :--- | :--- | :--- |
| `TWILIO_ACCOUNT_SID` | Twilio Account Identifier. | Twilio |
| `TWILIO_AUTH_TOKEN` | Twilio Authentication Token. | Twilio |
| `TWILIO_PHONE_NUMBER` | The virtual number that dials the patient. | Twilio |
| `NEIGHBOR_PHONE_NUMBER`| The hardcoded emergency contact for L2 Escalation demo. | System |

## Security

| Variable | Description | Default |
| :--- | :--- | :--- |
| `SECRET_KEY` | Cryptographic key for session signing. | (Generate UUID) |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Session duration. | 30 |
