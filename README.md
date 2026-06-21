# SkillNexora 🚀
> AI-powered learning visibility platform that helps students transform their learning journey into professional opportunities.

SkillNexora bridges the gap between learning and visibility. It allows users to track their learning activities, automatically build a skill profile, generate professional social media content, create personalized recruiter outreach messages, and view streaks/badges.

---

## 🎯 Hack2Skills Submission Details

*   **Vertical**: Career Tech / Developer Tools / AI-Powered Productivity
*   **Target Users**: Students, self-learners, freshers, open-source contributors, and job seekers.

### 🧠 Approach & Logic

1.  **AI Skill Extraction**:
    *   **Logic**: When a student adds a learning resource (e.g., Coursera, YouTube, blog), the system extracts raw technical keywords and general topics from the title and descriptions using optimized system prompts sent to the **Groq API** (`llama-3.3-70b-versatile`).
    *   **Impact**: Translates daily reading/studying into a structured skills profile without requiring manual resume updates.
2.  **Gamification & Streaks**:
    *   **Logic**: A calendar tracking system evaluates logging activities. If the user logs a resource on consecutive calendar days, their streak increments. Gaps of more than 1 day reset the streak, prompting consistency.
    *   **Impact**: Increases user engagement through positive reinforcement and earned milestones.
3.  **Outreach & Social Media Content Pipeline**:
    *   **Logic**: The system builds a dynamic text summary of the student's logged skills, learning hours, and topic history. This summary forms the context fed into the AI content generator to produce highly personalized LinkedIn posts, X threads, and recruiter cold-outreach templates.

---

## 🛠️ Tech Stack

| Component | Technology |
| :--- | :--- |
| **Backend** | Python + Flask |
| **Database** | PostgreSQL / SQLite (Local Fallback) |
| **Authentication** | Flask-Login |
| **AI Inference** | Groq API (Llama 3 Models) |
| **Frontend** | HTML5, CSS3, JavaScript, Tailwind CSS, Jinja2 Templates |

---

## ✨ Features Overview

*   **📚 Learning Tracker**: Log courses, videos, blogs, books, and articles. Track progress percentage and record key takeaways.
*   **🔥 Streak & Badges System**: Visual indicators of learning streaks (7-Day, 30-Day) and unlockable badges based on platform activity.
*   **✍️ AI Post Generator**: Instantly generate structured LinkedIn posts or Twitter threads based on the actual learning logs.
*   **📩 AI Cold Outreach**: Personalize outreach DMs to recruiters or hiring managers for target roles and companies.
*   **🚀 Demo Mode**: Eephemeral testing accounts populated with seeded mock data, allowing quick product exploration without registration.

---

## ⚙️ Running Locally

Follow these steps to run the application in a local environment:

**1. Clone the repository**
```bash
git clone https://github.com/deepikagandla7456/skillnexora.git
cd skillnexora
```

**2. Setup Virtual Environment & Install Dependencies**
```bash
python -m venv venv
source venv/Scripts/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

**3. Configure Environment Variables**
Create a `.env` file in the root directory (based on `.env.example`):
```ini
SECRET_KEY=your_session_secret_key
GROQ_API_KEY=your_groq_api_key
```

**4. Start the Application**
```bash
python run.py
```
Open [http://localhost:5000](http://localhost:5000) in your web browser.

---

## 📁 Project Structure

```
skillnexora/
├── app/
│   ├── __init__.py        → Flask App factory and DB context setup
│   ├── models.py          → SQLAlchemy Database models
│   ├── helpers.py         → Groq LLM prompts and streak logic
│   ├── demo_data.py       → Seeds data for Demo Mode
│   ├── routes/            → Segmented routes
│   │   ├── auth.py        → Auth & Demo login
│   │   ├── main.py        → Home & Dashboard
│   │   ├── learning.py    → Tracker routes
│   │   ├── post.py        → AI Post Generation
│   │   ├── outreach.py    → Recruiter Outreach
│   │   └── streak.py      → Gamified badges wall
│   ├── templates/         → Jinja2 HTML Layouts
│   └── static/            → Style sheets
├── requirements.txt       → Library dependencies
├── vercel.json            → Serverless deployment configuration
└── run.py                 → Development server entry point
```

---

## 🔍 Assumptions & Fallbacks

*   **API Accessibility**: The app assumes the user has configured a valid `GROQ_API_KEY` for LLM tasks. If the key is missing or invalid, the helper functions catch the exception gracefully and return a helpful notice rather than crashing the page.
*   **Storage Fallback**: The app defaults to a local SQLite database (`instance/skillnexora.db`) if no PostgreSQL `DATABASE_URL` is set in the environment, facilitating zero-config local testing.
