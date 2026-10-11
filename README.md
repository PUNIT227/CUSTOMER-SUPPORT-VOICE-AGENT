# WordBridge English Academy — Inbound Voice Agent (`Ashley`)

[![ElevenLabs](https://shields.io)](https://elevenlabs.io)
[![License: MIT](https://shields.io)](https://opensource.org)

This repository contains the configuration, runtime architecture, and schema files for **Ashley**, an autonomous AI Enrollment Advisor built for **WordBridge English Academy**. 

Ashley operates as an inbound customer service representative designed to welcome prospective students, answer program inquiries with deterministic compliance, book trial spots, and route live hot-leads to human sales teams.

---

## 🎧 Agent Blueprint & Core Tech Stack

*   **Orchestration Engine:** ElevenLabs Conversational AI 
*   **Large Language Model:** `qwen36-35b-a3b` (Configured at `temperature: 0` for zero-hallucination compliance)
*   **Text-to-Speech (TTS):** `eleven_v4_turbo` (Voice Token ID: `ZUrEGyu8GFMwnHbvLhv2`)
*   **Automatic Speech Recognition (ASR):** `scribe_realtime` (High-fidelity, low-latency audio processing)
*   **Audio Sample Delivery:** `pcm_16000` bi-directional input/output streaming

---

## 🛠️ Workflows & Tool Definitions

The agent configuration handles two functional, action-oriented webhooks to automate lead routing and operations:

### 1. Saturday Demo Class Registration (`addToGoogleSheet`)
When a user expresses interest in attending a trial class, the agent initiates data harvesting:
*   **Required Inputs:** Captures `name` and parses `phone_number` digit-by-digit.
*   **Fallback Logic:** In case of API failure, the agent transitions seamlessly to verbal notes assurance rather than breaking the stream context.

### 2. High-Intent Lead Transfer (`transferCall`)
When a caller confirms readiness for instant enrollment:
*   **Action:** Triggers a PSTN/SIP warm-transfer out of the conversational engine layer directly to the human enrollment queue.

---

## 📂 Project Architecture

```text
wordbridge-voice-agent/
├── .gitignore          # Prevents tracking of .env files and API keys
├── agent.json          # Production configuration payload (prompts, rules, tools)
└── README.md           # Repository documentation and deployment workflows
```

---

## 🚀 Getting Started & Local Management

To update, track, or sync this repository directly with your live ElevenLabs agent dashboard, use the official ElevenLabs CLI suite.

### Prerequisite Setup
Ensure you have the required runtime binaries installed locally.

```bash
# Install the ElevenLabs command line tools
npm install -g elevenlabs-cli
```

### Authentication
Retrieve your API secret keys from your ElevenLabs Profile Settings panel and inject them into your local shell:

```bash
# Linux/macOS
export ELEVENLABS_API_KEY="your_secret_api_key"

# Windows (Command Prompt)
set ELEVENLABS_API_KEY="your_secret_api_key"
```

### Syncing Changes
If you modify Ashley's prompt, guardrails, or behavior parameters directly in the local `agent.json` file, push the structural updates instantly using:

```bash
elevenlabs agent push --id agent_3101m4jqqentfptb7bqf3chm2ctr
```

If modifications were made directly inside the web UI dashboard, pull the latest stable JSON config back down to sync your code workspace:

```bash
elevenlabs agent pull --id agent_3101m4jqqentfptb7bqf3chm2ctr --output agent.json
```

---

## 🛡️ Operational Guardrails

This configuration strictly enforces systemic safeguards:
*   **Zero Inventory Fabrication:** Cannot invent program tiers or fee structures absent from the active system prompt context or knowledge base arrays.
*   **Data Integrity:** Restricts visibility over other students' personal records.
*   **Low Pressure:** Maintained to act purely as an informative guide to safeguard conversions.

---


# CUSTOMER-SUPPORT-VOICE-AGENT
