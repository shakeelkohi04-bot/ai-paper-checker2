# ai-paper-checker2
# AI Exam Paper Checker

A beginner-friendly Flask web application that uses a Gemini API model to help teachers review attempted exam papers. It extracts text from PDF, Word (`.docx`), and TXT files, requests an AI-assisted evaluation, displays question-wise feedback, and allows reports to be downloaded as JSON or CSV.

> **Important:** AI grading can be wrong. This is a review assistant, not a replacement for a qualified teacher. A teacher should verify marks before using them as official grades.

## Features

- Upload a student's attempted paper in PDF, DOCX, or TXT format.
- Optionally upload the question paper, answer key, or reference material.
- Enter the subject, total marks, and a teacher's marking rubric.
- Generate question-wise marks, feedback, suggested answers, overall feedback, and a percentage.
- Download the report as JSON or CSV.
- Run locally on your own computer using Flask.
- Keep the API key in a local `.env` file rather than in source code.

## Requirements

- Python 3.10 or newer recommended.
- Internet connection for Gemini API calls.
- A Gemini API key available to your Google AI Studio account.
- Git, if you want to manage the project with GitHub.

## 1. Download or clone the project

If you have pushed this project to your GitHub repository:

```bash
git clone https://github.com/YOUR-USERNAME/ai-paper-checker.git
cd ai-paper-checker
```

Alternatively, download the ZIP file from GitHub and extract it.

## 2. Create a virtual environment

### Windows (PowerShell)

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can use Command Prompt instead:

```bat
.venv\Scripts\activate.bat
```

### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## 4. Configure the API key

1. Open [Google AI Studio API keys](https://aistudio.google.com/apikey).
2. Create or select an API key if your account is eligible.
3. Copy `.env.example` to a new file named `.env`.
4. Put your real API key after `GEMINI_API_KEY=`.
5. If the configured model is not available to your account, change `GEMINI_MODEL` to a model currently supported by your API account.
6. Never share your key or commit `.env` to GitHub.

Example `.env`:

```dotenv
GEMINI_API_KEY=your_real_key_here
GEMINI_MODEL=gemini-2.5-flash
FLASK_SECRET_KEY=use_a_long_random_secret
```

Do not put quote marks around the values unless they are part of the value.

## 5. Run the application

From the project folder, with the virtual environment activated:

```bash
python app.py
```

Open this address in your browser:

http://127.0.0.1:5000

Keep the terminal running while you use the application. Press `Ctrl+C` in the terminal to stop it.

## 6. How to use it

1. Upload the student's attempted paper.
2. Optionally upload a question paper, answer key, or other reference document.
3. Enter the subject and total available marks.
4. If available, enter the teacher's rubric (for example, key points and how partial marks should be awarded).
5. Click **Evaluate Paper**.
6. Review the question-wise results and download the JSON or CSV report.

For better grading, provide both the question paper/answer key and a clear rubric. If these are omitted, the model may have to infer the questions or criteria, so results may be less reliable.

## Supported files and limitations

- Supported extensions: `.pdf`, `.docx`, `.txt`.
- PDFs must contain selectable text. This version does **not** include OCR for scanned pages or handwriting recognition.
- Old `.doc` Word files are not supported; save them as `.docx`.
- The app has a 15 MB maximum request size.
- Very long documents are truncated before being sent to the model. Review large papers carefully.
- Image-only PDFs and handwritten answers need OCR or a vision-based workflow added separately.
- The API requires an internet connection and may be subject to account quotas, rate limits, and charges.

## GitHub setup

Create an empty repository on GitHub, then run these commands inside this project folder:

```bash
git init
git add .
git commit -m "Initial AI exam paper checker"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/ai-paper-checker.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username and use the repository URL shown by GitHub.

Before pushing, confirm that `.env` is not tracked:

```bash
git status
```

The `.gitignore` file excludes `.env`. If you ever accidentally commit an API key, revoke/rotate it immediately; deleting it in a later commit does not make the exposed key safe.

## Troubleshooting

### `GEMINI_API_KEY is missing`
Make sure the `.env` file is in the same folder as `app.py`, and that the variable is named exactly `GEMINI_API_KEY`.

### API model or API key error
Check that the key is valid, the Gemini API is enabled/available for your account, and `GEMINI_MODEL` names a model currently available to you.

### Quota or rate-limit error
Check your API account's quota and billing/usage settings. Wait and retry if the service rate-limits requests.

### `No selectable text was found`
The PDF may be a scan or image. This version does not perform OCR. Use a text-based PDF or add an OCR stage.

### Word document error
Upload a `.docx` file, not the older `.doc` format.

### Port 5000 is already in use
Close the other application using port 5000, or change the port in the final `app.run(...)` line of `app.py`.

## Security and privacy notes

- Do not upload confidential student data unless you are authorized to process it.
- Text extracted from uploaded files is sent to the configured AI provider for evaluation.
- This educational prototype does not include user accounts, role-based access, database storage, or production-grade deployment security.
- Do not expose Flask's development server directly to the public internet.
- For real institutional use, add authentication, access controls, audit logs, secure deployment, retention/deletion policies, and institutional approval.

## Project structure

```text
ai-paper-checker/
├── app.py
├── requirements.txt
├── README.md
├── .env.example
├── .gitignore
├── templates/
│   ├── index.html
│   └── report.html
└── static/
    └── style.css
```

## License

Choose a license before making the repository public. If this is a university assignment, follow your instructor's rules about attribution and permitted AI assistance.
