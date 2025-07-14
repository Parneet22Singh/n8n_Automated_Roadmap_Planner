# 📚 Academic & Career Roadmap Generator (n8n Workflow)

This project is an **n8n-based automation** that creates and delivers a personalized academic and career roadmap to B.Tech students via **Gmail** and **Google Calendar**. It leverages the **Gemini API** for dynamic HTML generation and automates scheduling and email notifications.

---

## ✨ Features

- 🎓 Generates semester-specific roadmaps based on student year and discipline
- 📧 Sends a formatted HTML roadmap via Gmail
- 📅 Adds roadmap tasks as scheduled events in Google Calendar
- 🧠 Extracts and parses AI-generated HTML to identify tasks and structure
- 📦 Ready-to-import `academic-roadmap.json` workflow included

---

## 🚀 How It Works

1. User submits inputs (Name, Discipline, Year, Understanding).
2. Gemini API generates a detailed HTML roadmap.
3. A Code node:
   - Extracts the recipient's email
   - Prepares the HTML body for Gmail
4. Another Code node:
   - Parses the roadmap to extract tasks
   - Maps them to current semester
   - Distributes them evenly as Google Calendar events
5. Gmail node sends the formatted email.
6. Google Calendar node schedules the roadmap tasks across the semester.

---

## 📁 Workflow Setup

### 🔄 Import Workflow File

1. Download or clone this repository
2. Open your n8n instance (`http://localhost:5678` by default)
3. Go to **Workflows > Import Workflow**
4. Upload the provided `academic-roadmap.json` file
5. Save and activate the workflow

---

## 🔑 Required Credentials

Before running the workflow, set up the following credentials in n8n:

### 📧 Gmail OAuth2

- **Credential Type:** Gmail OAuth2
- **Scopes Required:** `https://www.googleapis.com/auth/gmail.send`
- **Steps:**
  1. Enable Gmail API in Google Cloud Console
  2. Create OAuth 2.0 credentials (Client ID and Secret)
  3. Add them to n8n and authorize access

### 📅 Google Calendar OAuth2

- **Credential Type:** Google Calendar OAuth2
- **Scopes Required:** `https://www.googleapis.com/auth/calendar`
- **Steps:**
  1. Enable Google Calendar API
  2. Use the same Client ID/Secret or create a new one
  3. Grant calendar access when authorizing

### 🤖 Gemini API (Google AI Studio)

- **Method:** Use `HTTP Request` node
- **Authentication:** API Key
- **Setup:**
  - Create and deploy a Gemini model on [Google AI Studio](https://makersuite.google.com)
  - Copy the API Key and add it as an environment variable or in Secrets

---

## ⚙️ Configuration

- Set the email dynamically based on Gemini output in the Code node.
- Calendar events span the current semester (approx. 6 months).
- Tasks are detected based on heading context (`Semester 5`, `Semester 6`, etc.).
- Project-type tasks are longer (3 hrs); others default to 2 hrs.

---

## 🧪 Sample Input

```json
{
  "What is your name?": "Parneet Singh",
  "What is your discipline of study?": "Computer Science",
  "What year are you in?": "3",
  "What is your current level of understanding?": "Intermediate"
}
