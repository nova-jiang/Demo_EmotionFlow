# 🤖 ChatGPT Integration in EmotionFlow

EmotionFlow leverages the power of OpenAI’s GPT API to create a reflective, personalized emotional support experience. This document outlines how ChatGPT is integrated into the app’s user journey, technical workflow, and future extensions.

---

## 🔧 Use Cases of GPT in EmotionFlow

1. **Emotion Detection from Journals**
   - When a user submits a journal entry (typed or spoken), the entry is sent to ChatGPT with a carefully designed system prompt asking it to:
     - Detect the user’s **primary emotion(s)**.
     - Identify possible **emotion triggers** (e.g., "grades", "friend conflict", "family support").
     - Optionally, rate **emotion intensity** on a scale (1–5).

2. **Personalized GPT Conversation**
   - Users can start a direct conversation with GPT using voice or text.
   - GPT plays the role of an emotionally intelligent listener and reflection guide—not a therapist.
   - Prompts are customized to:
     - Encourage users to reflect on patterns.
     - Ask gentle, open-ended questions.
     - Offer self-awareness strategies (e.g., journaling prompts, grounding techniques).

3. **Emotion Summary Generation**
   - At the end of each week or month, GPT generates:
     - A short **natural language summary** of emotion patterns.
     - Optional encouragements or affirmations based on the user’s mood trends.

---

## 🤖 Input and Output in structured JSON

{
  "role": "user",
  "content": "I feel so overwhelmed lately. My thesis isn’t going well, and I’m constantly comparing myself to my classmates. I don’t even feel like leaving my room."
}

{
  "emotions": ["Overwhelm", "Insecurity", "Low Motivation"],
  "triggers": ["Thesis", "Broke my promise to friend Ammy"],
  "intensity": 4
}


## 📡 Technical Setup

- API: OpenAI Chat Completions API (GPT-4 or GPT-3.5-turbo)

- Authentication: Firebase Auth to manage access

- Calls made via: Cloud Functions or in-app HTTPS request with safety throttles

- Rate Limiting: Basic usage guardrails (e.g., max X requests/hour)

## 🔐 Privacy & Safety Considerations

- No journal content is stored without encryption.

- User journal data is anonymized when sent to GPT API.

- EmotionFlow is not a therapeutic app, and GPT outputs include disclaimers reminding users of this.

## 🔮 Future Plans

- Response Personalization: Use Firebase-stored user preferences to customize GPT tone.

- LoRA / Fine-tuning (optional): Training a smaller model on emotion-focused dialogues for cost-efficient offline inference.

- Other features. Welcome to discuss!

## 📎 Related Docs

- concept_overview.md – App concept & feature flow

- firebase_structure.md – Data architecture & schema (TBD)

- ui_flow_diagram.png – Sketch of journal → GPT → feedback flow (Coming soon)

## 👩‍💻 Made by 

Nova, Final-year CS student @ VU Amsterdam, passionate about building tech that supports mental well-being.