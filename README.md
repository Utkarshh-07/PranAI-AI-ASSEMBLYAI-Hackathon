# 🌊 PranAI — AI Mental Wellness for Students

**PranAI** is Sanskrit, roughly: "intelligence that nurtures your life energy."

## 📌 A Note for Judges, Upfront

**TOO ACCESS CODE PLS VISIT PRANA FOLDER**
Everything marked "✅ Demo Ready" below is genuinely built and working — the UI, the navigation flows, the gamification system, the parent dashboard, the safety-alert logic, and the voice input, all of it runs live in this build.

Two things are intentionally simplified for this submission, and I'd rather tell you exactly what and why than have you guess:

**AI responses are currently rule-based, not live LLM-generated.** The architecture is built to plug in GPT-5.4 Mini directly — the integration point already exists in the codebase — but for this hackathon I used keyword-based emotional detection instead of a live API call, so the demo stays fast and reliable for judging without API latency or cost getting in the way.

**Push notifications are simulated via local notifications, not FCM.** The real-time alert *logic* — what triggers an alert, what a parent sees versus what stays private — is fully implemented and demonstrated. The actual cross-device delivery mechanism (Firebase Cloud Messaging) is the next build step.

One thing that is **not** simplified: voice input runs on AssemblyAI's actual real-time streaming API over a live WebSocket connection — not a mocked transcript, not on-device speech recognition. What you'll see in the demo is the real thing.

<div align="center">

[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue)]()
[![Firebase](https://img.shields.io/badge/Firebase-Demo-orange)]()
[![AssemblyAI](https://img.shields.io/badge/AssemblyAI-Realtime%20STT-purple)]()
[![Status](https://img.shields.io/badge/Status-Prototype-yellow)]()

</div>

---

## 📋 Table of Contents

1. [The Problem](#-the-problem)
2. [The Solution](#-the-solution-pranai)
3. [Tech Stack](#-tech-stack)
4. [What's Demonstrated](#-whats-demonstrated)
5. [A Real Example](#-a-real-example)
6. [Demo Flow](#-demo-flow)
7. [Project Structure](#-project-structure)
8. [Demo Credentials](#-demo-credentials)
9. [Demo Video](#-demo-video)
10. [Local Setup](#-local-setup)
11. [What Makes PranAI Different](#-what-makes-pranai-different)
12. [Roadmap](#-roadmap)
13. [Team](#-team)
14. [License](#-license)

---

## 🎯 The Problem

87% of students report exam-related anxiety. 1 in 4 teenagers feel persistently sad or hopeless. 70% never seek help, mostly out of stigma or fear — and when they do look for it, therapy runs ₹1,500–3,000 a session, which most families can't treat as routine.

**The gap:** it isn't that parents don't care. It's that parents are left in the dark, and students are scared to be the one who breaks the silence first.

Voice matters here specifically: a student mid-crisis, exhausted at 1am, is often far more willing to *talk* than to type. Typing takes effort and gives a moment to second-guess and delete. Speaking is faster, and closer to how people actually reach out when they're overwhelmed.

---

## 💡 The Solution: PranAI

| Feature | Description | Status |
|---|---|---|
| 🤖 **AI Companions** | 24/7 AI friends, four different personalities | ✅ Demo Ready |
| 🎤 **Voice Input** | Speak instead of type, with live real-time transcription | ✅ Demo Ready |
| 👨‍👩‍👧‍👦 **Parent Alerts** | Real-time notifications for emotional patterns | ✅ Demo Ready |
| 🎮 **Gamified Wellness** | Shell collection, streaks, achievements | ✅ Demo Ready |
| 🛡️ **Safety System** | 5-tier emotional risk detection & escalation | ✅ Demo Ready |
| 📊 **Daily Summaries** | AI-generated wellbeing insights for parents | ✅ Demo Ready |

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Flutter / Dart |
| **Backend** | Firebase (Auth, Firestore) |
| **Voice Input** | AssemblyAI Realtime STT (Universal-3 Pro, WebSocket streaming) |
| **AI / ML** | Rule-based responses (demo) / GPT-5.4 Mini (planned) |
| **Notifications** | Local notifications (demo) / FCM (planned) |

---

## 📱 What's Demonstrated

### 👤 Student Side
AI chat interface with four distinct personalities (Alex, Jordan, Taylor, Casey), keyword-based emotional analysis, a calming ocean-themed UI, shell collection for positive habits, and daily streak tracking.

### 🎤 Voice Input (AssemblyAI)
Tap the mic instead of typing. Audio streams live to AssemblyAI's real-time WebSocket API, with partial captions appearing on-screen as you speak — the same way live subtitles work. When you pause, the finalized transcript is automatically submitted through the exact same pipeline a typed message goes through, so every downstream feature (emotional analysis, the 5-tier alert system, parent notifications) works identically whether the student typed or spoke.

### 👨‍👩‍👧 Parent Side
Real-time alerts when a concerning pattern shows up, an insight dashboard for emotional wellness trends, specific "here's something you could say tonight" suggestions instead of vague reassurance, quick access to emergency helplines, and AI-generated daily summaries.

### 🛡️ Safety System
A 5-tier escalation path — from a quiet logged note, up to an immediate alert with helplines surfaced for high-risk language. Higher tiers require parent contact to be actioned; this isn't a single flat "check-in," it actually changes what a parent knows and when. This pipeline is voice-input-aware: a spoken message triggers the same risk analysis as a typed one.

---

## 💬 A Real Example

This is the actual Parent Bridge translation, not a hypothetical.

**Student types (private — this never leaves the app):**
> "I have 3 exams next week. I'm so scared I'll fail. I can't sleep. Mom will be so disappointed."

**What the parent actually sees:**
> Your child had a difficult day emotionally. They're feeling scared about upcoming exams and worried about disappointing you.
>
> **Tonight, try this:** "I love you no matter what marks you get."

Nothing in the top box reaches the parent. The raw words stay private — what gets translated across is the feeling underneath them, plus one specific thing to say. That's the whole product in one exchange. The same is true whether that first message was typed or spoken aloud.

---

## 🔄 Demo Flow

### Scenario 1: Voice-First Check-In
1. Student logs in → opens AI chat with Alex
2. Taps the mic button instead of typing
3. Speaks: "I'm really stressed about my upcoming exams"
4. Live captions appear in real time as AssemblyAI transcribes
5. On pause, the finalized transcript auto-submits
6. AI responds with an empathetic message, exactly as it would for a typed message

### Scenario 2: Student Stress → Parent Alert
1. Student types or speaks: "I'm really stressed about my upcoming exams"
2. AI responds with an empathetic message
3. Parent receives a notification instantly
4. Parent views the insight and an actionable suggestion

### Scenario 3: Student Achievement → Parent Celebration
1. Student shares: "I finally finished my project!"
2. AI detects the positive pattern
3. Parent receives a celebration alert instead of a concern alert
4. Suggested response: "I'm proud of your hard work!"

---

## 📂 Project Structure

lib/
├── screens/
│ ├── ai_chat/ # AI companion chat system + voice input UI
│ ├── parent/ # Parent dashboard & alerts
│ ├── chat/ # Student chat system
│ └── auth/ # Authentication flows
├── services/ # Firebase, AI, AssemblyAI STT, Notifications
├── models/ # Data models
└── widgets/ # Reusable components


---

## 🚀 Demo Credentials

| Role | Email | Password |
|---|---|---|
| 👨‍🎓 **Student** | test@test.com | test123 |
| 👨‍👩‍👧 **Parent** | test@test.com | test123 |

> **Note:** Demo accounts for testing. All data is mock data.

---

## 🎥 Demo Video

[▶️ Watch the PranAI + voice demo](PASTE_YOUR_NEW_VIDEO_LINK_HERE)

**Covers:**
- ✅ Voice input via AssemblyAI real-time transcription
- ✅ Student login & dashboard
- ✅ AI chat with emotional support
- ✅ Parent notification system
- ✅ Parent dashboard & insights
- ✅ Complete feature walkthrough

---

## 🛠️ Local Setup

```bash
git clone https://github.com/YOUR_NEW_HACKATHON_REPO.git
cd PranAI
flutter pub get
flutter run
```


---

## 🎯 What Makes PranAI Different

Most student wellness apps stop at the student — they're a private journal or a chatbot, and the parent never enters the picture. PranAI is built around the opposite bet: that the person best positioned to help a struggling student is usually already in the house, and just doesn't know tonight is the night to say something.

| Feature | Other Apps | **PranAI** |
|---|---|---|
| Parent involvement | ❌ No | ✅ **Yes** |
| Voice-first input | ❌ Rare | ✅ **Real-time AssemblyAI STT** |
| Real-time alerts | ❌ No | ✅ **Yes** |
| Privacy protection | ❌ Compromised | ✅ **Parents never see chats** |
| Indian context | ❌ Western focus | ✅ **Designed for Indian students** |
| Cost | 💰 Expensive | 🆓 **Free** |

---

## 🔮 Roadmap

- [ ] **Phase 1:** Real GPT-5.4 Mini API integration
- [ ] **Phase 2:** Text-to-speech so AI companions can speak their replies aloud
- [ ] **Phase 3:** Video call support with AI characters
- [ ] **Phase 4:** Peer support groups for students
- [ ] **Phase 5:** Professional counselor integration
- [ ] **Phase 6:** Regional language support (Hindi, Tamil, Telugu) — a natural extension of voice input, since code-switching mid-sentence is common among Indian students

---

## 👥 Team

**Utkarsh Pawar** — solo developer 🧑‍💻, full-stack Flutter + Firebase.

---

## 📝 License

Protected Source License — see [LICENSE](LICENSE) file.

---

<div align="center">

**Made with ❤️ for Students**

*"Mental wellness is not a luxury, it's a necessity."*

</div>
