# Agentic Logic & Protocols

Arogya Saathi employs a deterministic state machine combined with probabilistic LLM generation to ensure safety and accuracy.

## 1. Onboarding Agent (`onboarding_agent.py`)

**Goal:** Zero-hallucination data extraction.

* **Logic:** Uses schema introspection to identify missing fields (`name`, `age`, `location`) in the `Patient` Pydantic model.
* **Behavior:**
* Iteratively prompts the user only for missing information.
  * Validates input types (e.g., converts "bees saal" to `Integer: 20`).
  * **Safety Rail:** Does not commit to the database until the profile completeness score reaches 100%.

## 2. Check-in Agent (`checkin_agent.py`)

**Goal:** Clinical Triangulation using "Soft Sensors."

* **Logic:** Implements the "3 Ps" protocol for Hyperglycemia detection.
* **Triangulation Algorithm:**
  * `IF (Polydipsia == True) AND (Polyuria == True) -> RISK_SCORE = HIGH`
  * `IF (Polyphagia == True) -> RISK_SCORE = MODERATE`
* **State Management:**
  * Tracks checklist completion: [Medication, Symptoms, Diet].
  * Allows flexible interruption: If a patient reports a Priority 1 symptom (e.g., Chest Pain), the agent overrides the checklist to focus on the emergency.

## 3. Acoustic Biomarker Analysis (`audio_analysis.py`)

**Goal:** Physical signal processing.

* **Logic:** Runs `librosa` on raw PCM audio bytes (8kHz sample rate).
* **Metrics Tracked:**
  * **Jitter:** Pitch perturbation (Detects vocal tremors).
  * **Shimmer:** Amplitude perturbation (Detects breathiness/weakness).
  * **Spectral Flatness:** Detects monotony (indicative of neurological issues).
* **Threshold:** If metrics deviate >15% from the baseline, an interrupt signal triggers L2 Escalation.

## 4. SOAP Scribe (`soap_agent.py`)

**Goal:** Medical Documentation.

* **Trigger:** Activates post-call via Celery background task or AsyncIO.
* **Transformation:** Converts Hinglish conversational transcripts into professional English medical terminology.
* **Format:**
  * **S:** Subjective (Patient's stated symptoms).
  * **O:** Objective (Detected biomarkers).
  * **A:** Assessment (AI's risk stratification).
  * **P:** Plan (Escalation actions taken).
