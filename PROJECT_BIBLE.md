# PROJECT BIBLE

**ComedKares – Multilingual AI Appointment Booking Agent**

## 1. Project Vision

Build a plug-and-play, multilingual, voice-first Agentic AI receptionist for healthcare clinics.

Patients should be able to book, reschedule and cancel appointments through natural voice or text conversations in English, Hindi and Kannada.

The platform must integrate with different clinic booking systems without requiring clinics to replace their existing infrastructure.

## 2. Core Features

### A. Multilingual Voice Agent
- English, Hindi and Kannada.
- Automatic language detection where supported.
- Speech-to-Text and Text-to-Speech.
- Text fallback.
- Natural conversational interaction.
- Minimal questioning and contextual information extraction.

### B. Appointment Management
- Doctor and service selection.
- Real-time availability.
- Temporary slot holds.
- Atomic booking and double-booking prevention.
- Appointment confirmation.
- Rescheduling and cancellation.

### C. Waitlist Management
- Register patients when preferred slots are unavailable.
- FIFO-based allocation.
- Automatic notification when slots become available.
- Temporary offer/hold expiry.
- Patient confirmation before final booking.

### D. Consent and Privacy
- Explicit consent before personal-data collection.
- Multilingual consent notice.
- Consent version and timestamp storage.
- Consent withdrawal handling.
- Data minimization and access controls.

### E. Verification and Payments
- Mobile OTP verification.
- Razorpay sandbox integration.
- Server-side payment verification.
- Idempotent payment processing.
- Confirmation only after verified payment success.

### F. Plug-and-Play Integration
- Embeddable website widget.
- Google Calendar adapter.
- Mock Clinic REST API adapter.
- Standardized booking interface.
- Clinic-specific configuration and branding.

### G. Audit and Human Escalation
- Log every important booking action.
- Maintain protected audit records.
- Detect uncertain or unsupported requests.
- Create staff handover tickets.
- Emergency escalation without attempting diagnosis.

## 3. Technology Stack

| Layer | Technology |
| --- | --- |
| Frontend | Next.js, TypeScript |
| Styling | Tailwind CSS |
| Backend | Python FastAPI |
| Database | PostgreSQL (Local) |
| AI | LLM with tool calling |
| Voice | STT + TTS APIs |
| Payments | Razorpay (Sandbox) |
| Calendar | Google Calendar API |
| Version Control | GitHub |

## 4. Architecture Rules

1. The AI agent must never directly modify booking records.
2. All booking operations must go through backend APIs.
3. PostgreSQL is the source of truth for platform-managed booking states.
4. Slot reservation must be atomic.
5. Temporary holds must expire automatically.
6. Payment must be verified server-side.
7. Every critical action must generate an audit event.
8. Personal information must not be collected before required consent.
9. Clinic integrations must implement a common adapter contract.
10. The AI must hand over uncertain cases to clinic staff.
11. Never invent appointment availability or booking confirmation.
12. Emergency symptoms must trigger immediate safety instructions.

## 5. Repository Structure

```text
comedkares-ai-agent/
│
├── PROJECT_BIBLE.md
├── README.md
├── .gitignore
├── .env.example
│
├── frontend/
│   ├── app/
│   ├── components/
│   ├── features/
│   ├── hooks/
│   ├── services/
│   └── public/
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── agents/
│   │   ├── integrations/
│   │   ├── booking/
│   │   ├── waitlist/
│   │   ├── consent/
│   │   ├── audit/
│   │   ├── payments/
│   │   └── escalation/
│   ├── tests/
│   └── requirements.txt
│
├── database/
│   ├── migrations/
│   └── seed/
│
├── widget/
│
├── docs/
│   ├── ARCHITECTURE.md
│   ├── API_CONTRACTS.md
│   └── DATABASE_SCHEMA.md
│
└── tests/
```

## 6. Team Ownership

- **Member 1:** AI agent, multilingual conversations, voice and tool calling.
- **Member 2:** FastAPI, PostgreSQL, appointment booking, concurrency and waitlist.
- **Member 3:** Next.js, patient interface, embeddable widget and admin dashboard.
- **Member 4:** Google Calendar, mock clinic API, OTP, payments, audit and testing.

All members must follow shared API contracts.

## 7. Development Strategy

1. Establish repository, project structure and architecture.
2. Define database schema and API contracts.
3. Implement core booking and slot-safety logic.
4. Implement AI conversation and voice pipeline.
5. Build patient interface and clinic dashboard.
6. Implement consent, waitlist and audit logging.
7. Integrate OTP and payment gateway.
8. Implement clinic adapters.
9. Implement human escalation.
10. Run integration, concurrency and end-to-end tests.
11. Deploy and prepare hackathon demonstration.

## 8. Git Collaboration Rules

- `main` must always contain a stable, tested version.
- Every member works on a separate feature branch.
- No direct commits to `main`.
- Changes must be submitted through Pull Requests.
- Do not modify shared database schemas or API contracts without coordination.
- Pull and merge updates regularly.
- Run relevant tests before merging.
- Never commit API keys, passwords or `.env` files.

## 9. Quality Requirements

The application must demonstrate:
- One complete voice-based appointment booking journey.
- English, Hindi and Kannada support.
- Explicit consent.
- OTP verification.
- Payment sandbox integration.
- Two different clinic adapters.
- One successful booking when 20 simultaneous requests compete for one available slot.
- Waitlist registration and allocation.
- Audit logs.
- Human handover.
