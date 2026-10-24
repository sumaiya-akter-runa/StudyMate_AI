<div align="center">

<img src="docs/logo.jpg" alt="StudyMate AI logo" width="150">

# StudyMate AI

**An AI study assistant that answers from your own PDFs, shows the page it used, and turns your notes into quizzes.**

![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?logo=django&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)

[**Download APK**](https://github.com/sumaiya-akter-runa/StudyMate_AI/releases/latest) · [Backend repository](https://github.com/sumaiya-akter-runa/studymate-backend)

</div>

---

## The Problem

Before exams, students spend hours searching long PDFs and notes for one answer. General AI chatbots can explain things, but they answer without evidence, so it is hard to know when to trust them.

- Finding the right page in a long PDF takes too much time
- AI answers are not linked to the student's own study material
- There is no easy way to see which topics need more practice

## The Solution

StudyMate AI reads the student's own PDFs and answers only from them. Every answer shows the page it came from, so the student can check it in one tap. The app also builds quizzes from the same PDFs and tracks weak topics.

> **Answers come from your PDF, not from guesses.**
> The AI is told to treat PDF text as data and to say so when the answer is not in the document.

## How It Works

```mermaid
flowchart LR
    A[Student uploads<br/>a PDF] --> B[Backend reads and<br/>splits the text]
    B --> C[Each piece becomes<br/>a meaning vector<br/>in pgvector]
    C --> D[Student asks<br/>a question]
    D --> E[Closest pieces<br/>are found]
    E --> F[Groq AI answers<br/>and cites the pages]
```

PDF processing runs in the background (Celery and Redis), so the app never freezes while a file is being prepared.

## Features

| Module | What it does |
|---|---|
| **AI Tutor** | Chat about any topic. Markdown answers with tables and code, copy, read aloud, regenerate and voice input |
| **Chat history** | Saved conversations that can be reopened or deleted |
| **PDF Q&A** | Ask questions about a PDF. Answers show page tags, and a tap shows the original text |
| **Summary** | Summary, key points with page tags and important terms. Saved and can be regenerated |
| **Quiz** | Multiple-choice quizzes from a PDF. Choose 5, 10 or 15 questions and easy, medium or hard |
| **Retry wrong answers** | Practice only the questions you missed. It never changes your stats |
| **Progress** | Overall score, recent scores, strong topics, weak topics and quiz history |
| **Practice weak topics** | A quiz built around your weak topics, taken from the PDF where you struggled most |
| **Account** | Register, login, edit name, change password, delete account, light and dark mode |

## Screenshots

<p align="center">
  <img src="docs/screenshots/home.jpg" width="200" alt="Home">
  <img src="docs/screenshots/tutor.jpg" width="200" alt="AI Tutor">
  <img src="docs/screenshots/chat.jpg" width="200" alt="Answer with copy and listen">
  <img src="docs/screenshots/history.jpg" width="200" alt="Chat history">
</p>
<p align="center">
  <img src="docs/screenshots/upload.jpg" width="200" alt="Upload PDF">
  <img src="docs/screenshots/summary.jpg" width="200" alt="Summary">
  <img src="docs/screenshots/points.jpg" width="200" alt="Key points with page tags">
  <img src="docs/screenshots/askquiz.jpg" width="200" alt="Ask and create a quiz">
</p>
<p align="center">
  <img src="docs/screenshots/quiz.jpg" width="200" alt="Taking a quiz">
  <img src="docs/screenshots/retry.jpg" width="200" alt="Retry wrong answers">
  <img src="docs/screenshots/progress1.jpg" width="200" alt="Progress">
  <img src="docs/screenshots/progress2.jpg" width="200" alt="Strong topics and history">
</p>

## Installation

1. Open the [latest release](https://github.com/sumaiya-akter-runa/StudyMate_AI/releases/latest) and download `app-release.apk`
2. Open it on an Android phone (allow *Install from unknown sources* if asked)
3. Register, upload a PDF and start asking questions

> The server runs on a free plan, so the first request after a quiet period can take up to a minute.

### Run from source

```bash
git clone https://github.com/sumaiya-akter-runa/StudyMate_AI.git
cd StudyMate_AI
flutter pub get
```

Set the backend address in `lib/config.dart`:

```dart
class AppConfig {
  static const String baseUrl = "https://your-backend.onrender.com";
}
```

Then run `flutter run`. For local testing use your computer's IP, for example `http://192.168.0.10:8000`.

## Tech Stack

| Layer | Technology |
|---|---|
| Mobile app | Flutter, Dart |
| Backend | Django, Django REST Framework |
| Database | PostgreSQL with pgvector |
| Background jobs | Celery, Redis |
| AI | Groq API (Llama) for chat, quizzes and summaries. Gemini embeddings for PDF search |
| Deployment | Docker on Render |
| Security | JWT authentication, tokens in Android secure storage, each user sees only their own data, PDF file checks |

## Known Limitations

- Scanned PDFs (photos of pages) are not supported yet, only text PDFs
- For very long PDFs the summary is built from pieces spread across the document
- Android only
- The free server can be slow on the first request

## Future Work

- Flashcards from PDFs
- Study streak and reminders
- Bangla and English answer toggle
- Timed exam mode

## Author

**Sumaiya Akter Runa**
