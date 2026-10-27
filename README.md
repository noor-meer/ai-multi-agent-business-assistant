# 🤝 AI Multi-Agent Business Assistant with Voice

An AI-powered business assistant built with **n8n, OpenAI, and Vapi** that automates customer enquiries, appointment management, business knowledge retrieval, and human escalation through voice and integrated workflows.

## ☀️ Overview

This project brings multiple business operations into one automated system. It understands customer requests, identifies their intent, and routes them to the appropriate workflow, connecting AI models with business tools to reduce repetitive manual work.

The **ClarityWorks Receptionist**, powered by Vapi, provides a voice-based interface for customers to interact with the assistant. Behind the scenes, n8n coordinates the relevant AI processing, appointment operations, record updates, and notifications.

## ✨ Key Features

- 🧠 **AI Intent Classification:** Identifies customer intent and extracts relevant information to determine the appropriate workflow.
- 📚 **Knowledge Assistant (RAG):** Retrieves relevant business information from Pinecone and generates context-grounded answers using OpenAI.
- 📅 **Appointment Management:** Checks Google Calendar availability, creates bookings, and supports appointment rescheduling and cancellation.
- 📞 **Voice Receptionist:** Enables customers to speak with the ClarityWorks Receptionist through Vapi, with requests processed by the connected n8n workflow.
- 📧 **Automated Notifications:** Sends appointment confirmation emails through Gmail and maintains appointment records in Google Sheets.
- 🧑‍💼 **Human Support Escalation:** Routes requests requiring additional assistance to the support team through Slack.
- ✅ **Input Validation:** Detects missing booking information and requests the details required before proceeding.
- ⚠️ **Error Handling:** Uses a dedicated n8n error workflow to notify the configured recipient when workflow errors occur.

## ⚙️ How It Works

1. **Customer Interaction:** A customer submits a request through the connected text or voice interface.
2. **AI Processing:** OpenAI identifies the customer's intent and extracts relevant details.
3. **Input Validation:** The workflow checks whether the required customer and appointment information is available.
4. **Request Routing:** n8n directs the request to the appropriate process, including knowledge retrieval, availability checking, booking, rescheduling, cancellation, or human escalation.
5. **Business Operations:** The workflow interacts with Google Calendar, Google Sheets, Gmail, Pinecone, or Slack as required.
6. **Response Delivery:** The workflow returns a structured result, and the voice assistant communicates the outcome to the customer.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| OpenAI API | Intent classification and AI-powered response generation |
| Vapi | Voice assistant and conversational interface |
| Pinecone | Vector database for business knowledge retrieval |
| Google Calendar | Appointment availability and event management |
| Google Sheets | Appointment recordkeeping |
| Gmail | Confirmation emails and notifications |
| Slack | Human support escalation |
| Postman | Webhook and workflow testing |
| ngrok | Local development webhook exposure |

## 🧪 Testing and Validation

The core workflow paths have been tested, including:

- Appointment booking and confirmation email delivery
- Availability checks for available and occupied time slots
- Appointment rescheduling and cancellation
- Missing booking information handling
- Business-information enquiries
- Human support escalation
- Rescheduling requests without a matching appointment
- End-to-end voice booking, including Google Calendar event creation and confirmation email delivery

Further testing is recommended for simultaneous booking requests, external service failures, and other production edge cases.

## 🔐 Security Considerations

- Store API keys and access credentials securely using n8n's credential manager.
- Never publish private webhook URLs, API keys, passwords, or customer information.
- Review connected account permissions and restrict access to the resources required by the workflow.
- Validate incoming webhook requests and apply suitable access controls before public deployment.
- Use sanitized workflow exports and sample data when sharing the project publicly.

## 📌 Project Status

The core workflow paths and end-to-end voice booking flow have been tested successfully. The project demonstrates how AI-powered request handling, voice interaction, and workflow automation can work together to streamline appointment management and customer support.

Further reliability testing and deployment-specific security hardening are recommended before production use.

---

**Developed as an AI automation project** demonstrating practical integration of AI, voice-based customer interaction, business workflows, and automated communication.
