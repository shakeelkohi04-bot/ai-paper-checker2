# 📝 AI Exam Paper Checker

A Streamlit app that uses the Google Gemini API to check a student's exam paper. Upload the paper as a PDF or DOCX file and get a total score, percentage, grade, question-wise marks, strengths, and weaknesses.

## Features

- Upload a student paper in **PDF** or **DOCX** format (scanned PDFs work too)
- Optional **marking scheme / answer key** upload for stricter grading
- Score, percentage, grade, and per-question feedback
- Custom total marks and extra grading instructions
- Download the result as JSON

## Setup

1. Clone the repository and open the folder:
   ```bash
   git clone https://github.com/<your-username>/exam-paper-checker.git
   cd exam-paper-checker
   ```
2. (Recommended) create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate      # Windows: venv\Scripts\activate
   ```
3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
5. Provide the key in **one** of these ways:
   - Type it into the sidebar when the app runs, or
   - Create `.streamlit/secrets.toml` containing:
     ```toml
     GEMINI_API_KEY = "your-key-here"
     ```
   - Or set an environment variable named `GEMINI_API_KEY`.

## Run

```bash
streamlit run app.py
```

Then open the local URL shown in the terminal.

## Notes

- **Never commit your API key.** `.gitignore` already excludes `.streamlit/secrets.toml` and `.env`.
- The default model is `gemini-2.5-flash`. If your key does not support it, change the model name in the sidebar.
- The free tier has rate limits, so very large papers or many quick uploads may fail. Wait a minute and try again.
- AI grading can be inconsistent or wrong. Treat the result as an assistant's opinion and review it before using it as a final grade.

## Project structure

```
exam-paper-checker/
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```
