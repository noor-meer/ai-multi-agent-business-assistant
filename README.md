# 🤝 AI Multi-Agent Business Assistant with Voice

An AI-powered business assistant built with **n8n, OpenAI, and Vapi** that automates customer inquiries, appointment management, business knowledge retrieval, and human escalation through voice and integrated workflows.

## 🌟 Overview

This project brings multiple business operations into one automated system. It understands customer requests, identifies their intent, and routes them to the appropriate workflow, connecting AI models with real business tools to reduce repetitive manual work.

## ✨ Key Features

- 🧠 **AI Intent Classification:** Understands customer requests and extracts relevant details.
- 📚 **Knowledge Assistant (RAG):** Retrieves business information from Pinecone and generates context-grounded answers using OpenAI.
- 📅 **Appointment Management:** Checks availability, creates bookings, and supports rescheduling and cancellation through Google Calendar.
- 📞 **Voice Receptionist:** Connects a Vapi voice assistant to n8n for conversational customer interactions.
- 📧 **Automated Notifications:** Sends appointment emails through Gmail and maintains records in Google Sheets.
- 🚨 **Human Escalation:** Sends requests requiring human attention to Slack.
- 🛡️ **Error Handling:** Includes a dedicated workflow for operational error notifications.

## 🏗️ Architecture

```text id="f3v8pa"
Customer / Vapi Voice Assistant
              |
              v
         n8n Webhook
              |
              v
     AI Intent Classification
              |
              v
       Intent-Based Routing
              |
      +-------+--------+
      |       |        |
      v       v        v
  Knowledge Booking  Escalation
    (RAG)  Workflow    (Slack)
      |       |
   Pinecone   +------ Google Calendar
   + OpenAI          |
                     v
               Google Sheets
                     |
                     v
                   Gmail
```

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation |
| OpenAI GPT-4o / GPT-4o-mini | Classification and response generation |
| Vapi | Voice assistant |
| Pinecone | Vector database for RAG |
| `text-embedding-3-small` | Text embeddings |
| Google Calendar | Appointment management |
| Google Sheets | Appointment tracking |
| Gmail | Email notifications |
| Slack | Human escalation |
| Postman and ngrok | API testing and webhook access |

## 🔄 How It Works

1. **Receive:** A customer submits a request through the webhook or voice assistant.
2. **Understand:** OpenAI classifies the request and extracts relevant information.
3. **Route:** n8n directs the request to the appropriate workflow.
4. **Process:** The system retrieves knowledge, checks availability, manages appointments, or escalates the request.
5. **Respond:** The workflow returns a response and triggers the relevant notifications.

## 📌 Project Status

The core workflow has been configured for knowledge retrieval, appointment availability, booking, rescheduling, cancellation, voice interaction, and human escalation.

The booking workflow has successfully created a Google Calendar event, recorded the appointment in Google Sheets, and executed the Gmail confirmation step. End-to-end testing of all branches, voice transcription accuracy, and failure scenarios remains pending.

## 🎥 Demo

Watch the project walkthrough:

**[View Project Demo](https://github.com/noor-meer/ai-multi-agent-business-assistant)**

## 👩‍💻 Author

**Noor ul Ain**

Agentic AI Developer | AI Automation | Python | n8n | RAG


