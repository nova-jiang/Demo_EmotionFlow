# 🗂️ Firebase Structure for EmotionFlow

This document outlines the current data architecture for EmotionFlow, using Firebase Firestore as the primary database, along with Firebase Authentication and optional Firebase Functions for secure processing.

---

## 🔐 Authentication

We use Firebase Authentication to manage users.

Each user is uniquely identified by a `uid`.


## 📚 Firestore Structure

/users/{uid}
├─ displayName: "Nova"
├─ email: "nova@email.com"
├─ createdAt: timestamp
├─ preferences: {
│ language: "en",
│ emotionLabelStyle: "basic" | "detailed"
│ }
└─ journals/
└─ {journalId}
├─ content: "I felt really stressed about my exam today..."
├─ createdAt: timestamp
├─ emotionAnalysis: {
│ emotions: ["Stress", "Anxiety"],
│ triggers: ["Exams", "Deadlines"],
│ intensity: 4,
│ summary: "You felt stressed today mainly due to academic pressure."
│ }
└─ GPTResponseRaw: { ... } (optional, for debugging or visualization)


## 📈 Weekly/Monthly Summary
/users/{uid}/summaries/{summaryId}
├─ type: "weekly" | "monthly"
├─ period: { start: timestamp, end: timestamp }
├─ topEmotions: ["Overwhelm", "Motivation"]
├─ mostCommonTriggers: ["GPA", "Sleep"]
├─ GPTSummary: "This week you experienced a lot of emotional ups and downs..."
└─ graphData: { nodes: [...], edges: [...] } (optional for emotion graphs)



## 📊 Emotion Graph 
/users/{uid}/emotion_graph
├─ nodes: [
│ { id: "Stress", count: 14 },
│ { id: "Joy", count: 6 },
│ ...
│ ]
└─ edges: [
{ source: "Stress", target: "Guilt", weight: 3 },
{ source: "Joy", target: "Hope", weight: 5 }
]


## 🌐 GPT Request/Response Logging (Private)
/gpt_logs/{logId}
├─ uid: "..."
├─ timestamp: ...
├─ prompt: "..."
├─ response: "..."
├─ type: "emotion_analysis" | "chat" | "summary"

> Stored in a separate collection for analytics or debugging.
> Access to this data should be strictly limited via Firestore rules and/or Cloud Functions.


## 🔐 Security Rules (Summary)

- Users can **only access their own data**
- Journals and summaries are read/write only by the authenticated user
- GPT logs (if stored) are not user-readable unless explicitly enabled


## 📌 Future Extensions

- Push notification tokens
- Emotion-based reminders (e.g., “write when stressed”)
- Friend/support sharing settings
- Offline storage sync

## 👩‍💻 Made by 

Nova, Final-year CS student @ VU Amsterdam, passionate about building tech that supports mental well-being.