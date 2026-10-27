# 📝 AI Exam Paper Checker

A Streamlit app that uses the OpenRouter API to check a student's exam paper. Upload the paper as a PDF or DOCX file and get a total score, percentage, grade, question-wise marks, strengths, and weaknesses.

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
4. Create a free account and API key at [OpenRouter](https://openrouter.ai/keys).
5. Provide the key in **one** of these ways:
   - Type it into the sidebar when the app runs, or
   - Create `.streamlit/secrets.toml` containing:
     ```toml
     OPENROUTER_API_KEY = "your-key-here"
     ```
   - Or set an environment variable named `OPENROUTER_API_KEY`.

## Run

```bash
streamlit run app.py
```

Then open the local URL shown in the terminal.

## Notes

- **Never commit your API key.** `.gitignore` already excludes `.streamlit/secrets.toml` and `.env`.
- The default model is `openrouter/free`, which picks a random free model for each request. For consistent grading, choose one specific model from the [OpenRouter models page](https://openrouter.ai/models?pricing=free) and paste its slug (for example, one ending in `:free`) into the sidebar.
- Free models have rate limits (a small number of requests per minute and per day), so many quick uploads may fail. Wait a minute and try again.
- PDFs are sent to OpenRouter as files. Scanned or handwritten PDFs need a model that can read images, and some PDF parsing engines on OpenRouter are paid.
- AI grading can be inconsistent or wrong. Treat the result as an assistant's opinion and review it before using it as a final grade.

## Project structure

```
exam-paper-checker/
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```
