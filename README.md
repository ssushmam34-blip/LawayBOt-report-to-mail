# ⚖️ AI Lawyer Chatbot – Flask Application

## 📌 Project Overview

The **AI Lawyer Chatbot** is a Flask-based web application that provides professional legal assistance strictly related to **Indian law**.

The system integrates:

- Groq LLM API (LLaMA 3.3 70B Versatile)
- Text-to-Speech (TTS) using pyttsx3
- MailerSend API for sending chat logs
- Python logging system for conversation storage

The chatbot answers only law-related queries and responds in a formal, structured legal format with proper statutory references.

---

## 🚀 Features

### ✅ 1. Indian Legal Assistant
- Answers strictly legal questions.
- Refuses non-legal queries politely.
- Maintains professional legal tone.
- Mentions:
  - Relevant Act name
  - Section/Article number
  - Legal principle
  - Indian jurisdiction

---

### ✅ 2. Structured Legal Response Format

Every response follows:

1. Brief Legal Summary  
2. Relevant Law Citation(s)  
3. Explanation  
4. Practical Legal Steps  
5. Short & Professional Conclusion  

---

### ✅ 3. Text-to-Speech (TTS)

- Converts AI response into speech.
- Uses `pyttsx3` (offline TTS engine).
- Runs in a separate background thread.
- Prevents blocking the Flask server.

---

### ✅ 4. Chat Logging

All conversations are stored in:

logs/AI_lawyer_chat.log

Logs contain:
- User messages
- AI responses
- Errors (if any)

---

### ✅ 5. Automatic Email Log Sending

When the user types:

bye

The system:
- Reads the entire log file
- Sends it via MailerSend API
- Emails complete chat history

---

## 🏗️ Project Structure

AI-Lawyer/
│
├── app.py
├── templates/
│   └── index.html
├── logs/
│   └── AI_lawyer_chat.log
├── requirements.txt
└── README.md

---

## ⚙️ Technologies Used

- Python 3.x  
- Flask  
- Groq API  
- pyttsx3  
- MailerSend API  
- Logging module  
- Threading  

---

## 🔑 Installation Guide

### 1️⃣ Install Required Packages

```bash
pip install flask groq pyttsx3 mailersend
```

---

### 2️⃣ Add API Keys in app.py

```python
client = Groq(api_key="YOUR_GROQ_API_KEY")
ms = MailerSendClient(api_key="YOUR_MAILERSEND_API_KEY")
```

⚠️ Do NOT expose API keys in public repositories.  
Use environment variables in production.

---

## ▶️ Running the Application

```bash
python app.py
```

Open in browser:

http://127.0.0.1:5000/

---

## 🔄 Application Workflow

1. User sends a message.
2. Flask receives `/chat` POST request.
3. Message is sent to Groq LLM.
4. AI generates structured legal reply.
5. Reply is:
   - Logged to file
   - Spoken using TTS (background thread)
   - Sent back as JSON response
6. If user types "bye":
   - Log file is emailed automatically.

---

## 🧵 Threading Implementation (TTS)

```python
tts_thread = threading.Thread(target=speak_text, args=(reply,))
tts_thread.daemon = True
tts_thread.start()
```

Why threading?
- Prevents server freezing
- Allows smooth chat response
- Runs speech engine in background

---

## 🛠 Logging Configuration

```python
logging.basicConfig(
    filename="logs/AI_lawyer_chat.log",
    level=logging.INFO,
)
```

- Stores chat history
- Records errors
- Reduces unnecessary HTTP logs

---

## 📧 Email Integration

When user says "bye":

```python
if user_message.lower().strip() == "bye":
```

- Log file is read
- EmailBuilder constructs email
- MailerSend sends conversation history

---

## 🔐 Restrictions & Safety

The chatbot:
- Only answers law-related queries
- Refuses medical, entertainment, technical questions
- Does not provide personal opinions
- Always cites Indian legal sources
- Maintains professional tone

---

## 📈 Future Improvements

- Add user authentication
- Store data in MySQL/PostgreSQL
- Admin dashboard
- Case tracking system
- Voice input (Speech-to-Text)
- Cloud deployment (AWS / Render / Railway)

---

## ⚠️ Disclaimer

This project is for academic and educational purposes only.  
It does not replace a licensed advocate or legal professional.  
Always consult a registered lawyer for real legal matters.

---

## 👩‍💻 Author

AI Lawyer Legal Assistant  
Built using Flask + Groq LLM API
