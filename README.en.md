# Tailor Resume for Codex

## ⚠️ Before you start

This repository is not the Codex app itself. It is a skill that needs to be installed inside Codex.

So before using this repository, install the Codex app first.

## 🖥️ Install the Codex app first

If you do not have Codex yet:

1. Open the official Codex page: [openai.com/codex](https://openai.com/codex/)
2. Click `Download`.
3. Install the Codex app.
4. Open Codex and sign in with your ChatGPT account.
5. After that, come back and install this `tailor-resume` skill.

If you are unsure whether your account includes Codex access, check the latest availability details on the official Codex page.

This is a Codex skill for tailoring resumes to specific job descriptions.

You can feed it multiple versions of your resume from different time periods or career directions, plus one or many target JDs. It builds a single experience pool from all resume versions, compares that pool against the JD requirements, asks follow-up questions to uncover missing but relevant evidence, rewrites your experience for the exact role, and outputs an editable Word document.

This is not just keyword swapping. It is a full workflow for consolidating resume history, batch-reading JDs, surfacing gaps, rewriting with intent, and producing a polished `.docx` resume.

## Key Capabilities

### 1. Multiple Resume Versions -> One Experience Pool

Feed in every version of your resume. The skill extracts experience, projects, skills, and achievements across all versions and merges them into one reusable experience pool, including items that were removed from later drafts.

### 2. Batch JD Ingestion

Feed in JDs in bulk. It can process pasted text, local files, links, and screenshots, including folders that contain many JD screenshots or documents.

### 3. Gap Discovery Through Follow-Up Questions

It compares your experience pool against the JD, identifies the gaps, and asks targeted follow-up questions. This often surfaces relevant experience you actually have but did not think to include or position for that role.

### 4. JD-Specific Rewrite

It rewrites experience using STAR logic, but not as generic filler. It changes emphasis, wording, and keywords around the specific JD so the reader quickly sees that you have done the work they need.

### 5. Keep Layout And Export To Word

It outputs an editable Word document. If you provide one or more `.docx` resumes, you can choose a preferred style reference so the generated resume reuses that layout, spacing, and typography.

## 🔧 Then install this skill

Use Codex's GitHub skill installer:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo rongmiao926-hub/codex-tailor-resume-skill \
  --path tailor-resume
```

Or install manually:

```bash
cp -R tailor-resume ~/.codex/skills/
```

Restart Codex after installation.

## 💬 Beginner-Friendly Usage

You do not need to memorize a strict command format. Just talk to Codex naturally, ask it to use `tailor-resume`, and tell it where your resumes are and where the JD is.

For example:

```text
Help me use $tailor-resume to tailor my resume. My resumes are in ~/Documents/resumes/. Build one experience pool from all of them, compare it against this JD, ask me about any missing but important experience, and generate a one-page resume in Word.
```

```text
Help me use $tailor-resume to tailor my resume. I am applying to several jobs. My resumes are in ~/Documents/resumes/ and my JD screenshots are in ~/Documents/jd-screenshots/. Analyze the gaps once, then generate a tailored resume for each job.
```

```text
Help me use $tailor-resume to tailor my resume. My resumes are in ~/Documents/resumes/, and please reuse the formatting from ~/Documents/resumes/final-resume.docx. Here is the JD link: https://example.com/job/12345
```

## 📝 Notes

- If you only provide PDF resumes, the skill can usually reuse the content but not the original layout.
- If the JD is a screenshot or webpage, extraction quality depends on image clarity and page readability.
- Word output is usually best when at least one source resume is provided as `.docx`.
