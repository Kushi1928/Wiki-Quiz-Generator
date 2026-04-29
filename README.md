# 🧠 Wiki Quiz Generator — AI-Powered Wikipedia Quiz Generator

**Wiki Quiz Generator** is a full-stack web application that automatically generates quiz questions from Wikipedia articles using Artificial Intelligence (AI).  
It bridges the gap between knowledge and interactivity by transforming static Wikipedia content into dynamic, self-assessing quizzes.  

---

## 🧾 Abstract

In today’s digital era, online information sources like **Wikipedia** serve as massive repositories of knowledge. However, passive reading often leads to low retention.  
Wiki Quiz Generator addresses this by introducing an **AI-powered learning companion** that automatically generates **multiple-choice quizzes** from Wikipedia content, enabling users to **test their understanding instantly**.

The project leverages **FastAPI** for backend logic, **React** for an interactive UI, and **Google Gemini (AI Model)** to intelligently generate relevant questions, answers, and explanations.

---

## 🎯 Objectives

- Automate quiz generation from **Wikipedia** URLs using AI.  
- Allow users to **view, store, and retake quizzes** anytime.  
- Provide **explanations** for each answer to enhance learning.  
- Record and display **quiz scores and attempt timestamps**.  
- Offer a clean, user-friendly **web interface** with real-time updates.  

---

## 🧩 Problem Statement

Traditional learning platforms rely heavily on static reading material and manual question preparation.  
Learners often lack immediate tools to assess how much they understood from an article.  
Creating quizzes manually is time-consuming and subjective.

---

## 💡 Proposed Solution

Wiki Quiz Generator automates the entire quiz creation process:
1. Users provide a **Wikipedia article URL**.  
2. The system scrapes the page content (summary, key entities, and sections).  
3. An **AI model (Google Gemini)** processes this data to generate questions and answers.  
4. The quiz is saved locally for review and analysis.  
5. Users can view, delete, or reattempt quizzes, and their scores are recorded for future tracking.  

---

## ⚙️ System Architecture

```

User (React Frontend)
↓
Frontend API Request (Axios)
↓
FastAPI Backend (Quiz Routes)
↓
Scraper Module → Extracts Wikipedia content
↓
Quiz Generator → Uses Gemini AI to form Q&A
↓
SQLite Database → Stores quiz data, score, timestamp
↓
Frontend → Displays quiz, history, and score

```

---

## 🧰 Technology Stack

| Layer | Technology |
|-------|-------------|
| **Frontend** | React.js, Axios, HTML5, CSS3 |
| **Backend** | FastAPI (Python) |
| **Database** | SQLite (SQLAlchemy ORM) |
| **AI/ML Integration** | Google Gemini / LangChain |
| **Styling** | TailwindCSS (optionally plain CSS) |
| **Server** | Uvicorn |
| **Other Tools** | Pydantic, Requests, Python-dotenv |

---

## 📁 Folder Structure

```

Wiki Quiz Generator/
│
├── backend/
│   ├── .vscode/
│   │   └── settings.json
│   ├── app/
│   │   ├── crud.py
│   │   ├── database.py
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   ├── routes/
│   │   │   └── quiz.py
│   │   ├── scripts/
│   │   │   ├── debug_quiz_generator.py
│   │   │   └── normalize_quiz_questions.py
│   │   └── utils/
│   │       ├── prompt_templates.py
│   │       ├── quiz_generator.py
│   │       └── scraper.py
│   ├── requirements.txt
│   ├── .env
│   └── venv/
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Modal.jsx
│   │   │   ├── QuizDisplay.jsx
│   │   │   ├── Tab1-Generate.jsx
│   │   │   └── Tab2-History.jsx
│   │   ├── styles/
│   │   │   ├── App.css
│   │   │   ├── Modal.css
│   │   │   ├── QuizDisplay.css
│   │   │   ├── Tab1.css
│   │   │   └── Tab2.css
│   │   ├── App.js
│   │   ├── index.js
│   │   ├── logo.svg
│   │   └── setupTests.js
│   ├── package.json
│   └── package-lock.json
│
└── README.md

````

---

## ⚙️ Installation & Setup Guide

### 🧱 Prerequisites
- Python 3.10+
- Node.js 18+
- npm or yarn
- Internet connection (for AI API calls)

---

### 🧩 Backend Setup (FastAPI)
```bash
cd backend
python -m venv venv
venv\Scripts\activate      # Windows
# source venv/bin/activate # Linux/Mac

pip install -r requirements.txt
````

Create a `.env` file:

```
GEMINI_API_KEY=your_gemini_api_key_here
DATABASE_URL=sqlite:///./app.db
```

Run the backend:

```bash
uvicorn app.main:app --reload
```

Visit: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

### 💻 Frontend Setup (React)

```bash
cd frontend
npm install
npm start
```

Frontend URL → [http://localhost:3000](http://localhost:3000)

---

## 🔗 API Endpoints Overview

| Method   | Endpoint                 | Description                           |
| -------- | ------------------------ | ------------------------------------- |
| `POST`   | `/api/quiz/generate`     | Generates a quiz from a Wikipedia URL |
| `GET`    | `/api/quiz/history`      | Lists all quizzes                     |
| `GET`    | `/api/quiz/history/{id}` | Retrieves quiz details                |
| `POST`   | `/api/quiz/submit`       | Records user’s quiz score             |
| `DELETE` | `/api/quiz/history/{id}` | Deletes a quiz from database          |

---

## 🧠 AI Quiz Generation Workflow

1. **Scraper Module (`scraper.py`)**

   * Extracts Wikipedia title, summary, and key sections.
   * Cleans and structures text for AI input.

2. **AI Module (`quiz_generator.py`)**

   * Sends extracted content to Gemini model.
   * Generates a structured JSON with:

     * Question
     * Options
     * Correct Answer
     * Difficulty
     * Explanation

3. **Database Layer**

   * Stores all generated quizzes.
   * Records quiz creation and score submission timestamps.

4. **Frontend Rendering**

   * Displays quiz history and details.
   * Uses modals to show full quiz content.

---

## 📊 Database Schema (SQLite)

| Column            | Type     | Description                    |
| ----------------- | -------- | ------------------------------ |
| `id`              | Integer  | Primary key                    |
| `url`             | String   | Wikipedia URL                  |
| `title`           | String   | Article title                  |
| `summary`         | Text     | Summary content                |
| `quiz_questions`  | JSON     | Generated quiz set             |
| `related_topics`  | JSON     | Related Wikipedia topics       |
| `created_at`      | DateTime | When quiz was generated        |
| `submitted_score` | Integer  | Score submitted by user        |
| `total_questions` | Integer  | Total number of quiz questions |
| `attempted_at`    | DateTime | When quiz was attempted        |

---

## 🖥️ Frontend Overview

### Key Components

| Component           | Description                                          |
| ------------------- | ---------------------------------------------------- |
| `Tab1-Generate.jsx` | Handles Wikipedia URL input and quiz generation      |
| `Tab2-History.jsx`  | Displays list of all stored quizzes                  |
| `QuizDisplay.jsx`   | Renders detailed quiz view and explanations          |
| `Modal.jsx`         | Reusable popup component for displaying quiz details |

---

## 🧪 Example Quiz Entry

```json
{
  "id": 9,
  "title": "Agriculture",
  "summary": "Agriculture is the practice of cultivating the soil...",
  "quiz_questions": [
    {
      "question": "What was a key factor in the rise of sedentary civilization?",
      "options": ["Farming", "Mining", "Trade", "War"],
      "answer": "Farming",
      "difficulty": "easy",
      "explanation": "Farming produced food surpluses that enabled city life."
    }
  ],
  "submitted_score": 4,
  "total_questions": 5,
  "attempted_at": "2025-11-09T20:30:00"
}
```

---

## 🔮 Future Enhancements

* 🔐 User authentication & personalized dashboard
* 🌐 Multi-language quiz generation
* 📊 Quiz analytics & progress tracking
* 🧩 Adaptive difficulty levels
* 📥 Export quizzes as PDF or share links

---

## 🧑‍💻 Developer Information

**Project Title:** Wiki Quiz Generator – AI-Powered Wikipedia Quiz Generator
**Developer:** G Sai Archan
**Institution:** Sri Indu  College of Engeering and Technology
**Department:** Computer Science and Engineering - AIML
**Semester:** VIII (Full Stack Development Project)
**Tools Used:** Visual Studio Code, FastAPI, React, SQLite
**Domain:** Artificial Intelligence + Full Stack

---

## 🏁 Conclusion

Wiki Quiz Generator successfully demonstrates how AI can transform traditional learning into an interactive, assessment-driven experience.
By combining **AI comprehension**, **FastAPI efficiency**, and **React interactivity**, the project delivers a seamless and intelligent quiz-generation system that can scale into educational platforms.

---

## ❤️ Acknowledgements

* [FastAPI](https://fastapi.tiangolo.com)
* [React.js](https://react.dev)
* [LangChain](https://www.langchain.com)
* [Google Gemini AI](https://ai.google.dev)
* [Wikipedia](https://www.wikipedia.org)

---

## 🧾 License

MIT License © 2026 — G Sai Archan
Feel free to fork, modify, and share with attribution.


