# PillCare: A Responsible AI Agent for Daily Medication Monitoring

**Category**: Best in Python / Responsible AI / Azure AI Agent Service\
**Team**: Alex Rozenberg\
**Platform**: Azure AI Agents + Custom Vision + Cosmos DB + Twilio WhatsApp + Colab

---

## Overview

PillCare is a fully automated AI agent that assists elderly users in tracking and adhering to their daily medication routines. It combines Azure AI Agent reasoning, Custom Vision image analysis, CosmosDB memory, and Twilio WhatsApp messaging into one cohesive healthcare assistant.

The solution was designed and tested using Python in Google Colab and integrates deeply with Azure cloud infrastructure.

---

## Key Features

### 1. **Responsible AI Agent Interaction (Azure OpenAI)**

- Empathetic, natural-language replies to seniors
- Dual-language support (English + Romanian)
- Transparent decision-making for users and caregivers

### 2. **Photo-Based Pill Recognition (Azure Custom Vision)**

- User sends a photo of daily pills
- Model detects and tags visible medications

### 3. **Prescription Parsing with LLM**

- Extracts structured data from scanned PDF prescriptions
- LLM converts text to a `{pill: quantity}` dictionary

### 4. **Intelligent Comparison & Memory Logging**

- Compares expected vs detected pills
- Logs each day’s results into CosmosDB
- Stores image, PDF, reply, and chart in Blob Storage

### 5. **Escalation Logic & Trend Analysis**

- Agent evaluates 7-day behavior history
- Decides when to escalate to a caregiver
- Generates weekly dashboards

### 6. **Human-in-the-Loop via WhatsApp (Twilio)**

- Two-way communication with user
- WhatsApp alerts for missed pills or photo
- Escalations sent to verified family member

---

## Technical Architecture

```mermaid
graph TD
  A[User takes pill photo] --> B[Photo uploaded to Azure Blob]
  B --> C[Custom Vision detects pills]
  D[PDF prescription] --> E[LLM parses to {pill: count}]
  C & E --> F[Compare expected vs detected]
  F --> G[LLM generates reply]
  G --> H[Twilio WhatsApp alert]
  F --> I[Save result in Cosmos DB]
  I --> J[Weekly Dashboard PNG]
  J --> K[Upload dashboard to Blob & notify user]
  I --> L[Behavior summary]
  L --> M[LLM: Should escalate?]
  M --> N[Caregiver Alert (if needed)]
```

---

## How to Run (Colab)

1. Upload this repo to Google Colab
2. Install required packages:

```python
!pip install azure-cosmos azure-storage-blob PyPDF2 twilio matplotlib
```

3. Upload a daily pill photo and prescription PDF:

```python
run_daily_pillcare_check("Alex", "/content/pill_photo.jpeg", "/content/prescription.pdf")
```

---

## Submission Checklist

-

---

## Example WhatsApp Output

**User:** Sends photo + prescription

**Agent:**

> Today I detected: Dexamol, Advil. Expected: Dexamol(2), Advil(3). Missing: Dexamol(1), Advil(2).
>
> You’ve missed pills for 3 of the last 7 days. Please try to improve. Also in Romanian: Vă rugăm să vă asigurați că luați toate medicamentele prescrise.

**Escalation:**

> 🚨 Escalation triggered. Please check on your loved one.

---

## License & Credits

This submission is part of the Microsoft AI Agents Hackathon. Code and design by Alex Rozenberg. All services used are free-tier or under the Azure free trial program.

---

## Questions?

Feel free to reach out to [alexrozenberg.ai@gmail.com](mailto\:alexrozenberg.ai@gmail.com) or connect via LinkedIn.

