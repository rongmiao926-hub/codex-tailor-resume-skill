---
name: tailor-resume
description: Tailor or rewrite a resume (定制简历) for one or more target job descriptions (JD, 职位描述, 岗位需求) using local resume files or folders plus JD text, files, URLs, or screenshots. Use when the user wants resume-JD fit analysis, targeted follow-up questions for missing experience, extraction from PDF/DOCX/MD/TXT materials, batch JD handling, or generation of a tailored one-page `.docx` resume that reuses a source Word style when possible.
---

# Tailor Resume

Use Chinese throughout. Do not invent experience, metrics, certificates, technologies, employers, or dates. Ask concise follow-up questions whenever missing facts would materially change the resume or the fit assessment.

## Quick Start

If the user has not yet provided enough input, begin with this brief intro and request:

```text
简历定制助手

我可以根据你的简历材料和目标 JD，筛选最匹配的经历，补问关键信息，并生成一份定制简历。
支持的简历输入：PDF、Word、Markdown、TXT，或包含多份简历的文件夹。
支持的 JD 输入：粘贴文本、文件路径、URL、截图；也支持批量 JD。
如果提供 Word 简历，我会尽量复用原有排版；只有 PDF 时只能复用内容，无法保留版式。
请提供简历路径和目标 JD。
```

## Expected Inputs

Expect two logical inputs:

1. Resume source: a file path or folder path containing resumes.
2. JD source: pasted text, a file path, one or more URLs, screenshots, or batch JD input.

Treat the following as batch JD input:

- A folder of JD files
- A text file split by `===`
- Multiple URLs separated by spaces or newlines
- A text file where each non-empty line is a URL

## Workflow

### 1. Resolve Resume Source And Cache

Determine the working resume directory first.

- If the user gives a folder, use that folder directly.
- If the user gives a single resume file, use its parent directory as the working directory.

Reuse `_experience_pool_cache.md` when it is still valid.

- Compare the cache timestamp against all supported resume files in the working directory.
- Supported resume extensions: `.pdf`, `.docx`, `.doc`, `.md`, `.txt`
- Use `exec_command` with shell tools such as `find`, `test`, and `stat`.
- If the cache is newer than every resume file, read it and tell the user that cached experience data was reused.
- If the cache is missing or stale, rebuild it from source files.

### 2. Extract Resume Content

Discover resume files with `find` or `rg --files`.

Use this extraction order:

- `.md` and `.txt`: read directly with shell commands.
- `.docx`: prefer `pandoc input.docx -t markdown`; fallback to `textutil -convert txt -stdout input.docx`.
- `.doc`: use `textutil -convert txt -stdout input.doc`.
- `.pdf`: prefer `pdftotext -layout input.pdf -`; if unavailable, try a minimal Python fallback with `pypdf` only when necessary; if extraction is still poor, tell the user the PDF may be scanned and request a text or Word version.

Summarize the extracted materials into a structured experience pool instead of caching raw full-text resumes. Capture at least:

- Personal and contact details already present in the source
- Education
- Skills and tools
- Work experience
- Projects
- Achievements, metrics, and awards
- Source file references for traceability

Save the structured result to `_experience_pool_cache.md` with `apply_patch`.

### 3. Choose A Style Reference

Prefer reusing an existing Word resume style when available.

- If there is exactly one `.docx` resume, use it as `style_reference`.
- If there are multiple `.docx` resumes, ask the user which one should provide the visual style.
- If there is no user-provided `.docx` but `reference.docx` exists in the working directory, use that.
- If only PDF resumes exist, explain that content can be extracted but original layout cannot be preserved, then ask whether to continue with default formatting.

When asking questions, keep them short and concrete. Ask only what is needed to keep moving.

### 4. Parse JD Inputs

Normalize every JD into the same structure:

- Role title
- Company name if present
- Required skills
- Preferred skills
- Core responsibilities
- Qualifications
- Domain or industry
- Nice-to-have items

Parse each input type as follows:

- Pasted text: parse directly.
- URL: use `web.open` on the direct URL and extract job details from the page.
- `.md`, `.txt`, `.docx`, `.doc`, `.pdf`: use the same local extraction rules as resume files.
- Local screenshot or image file: use `view_image`.

If the JD page is blocked by login, anti-bot checks, or client-side rendering that prevents extraction, tell the user immediately and ask for pasted text or a local file instead of guessing.

For batch inputs:

- Parse each item into a separate JD record.
- If the input file uses `===`, split on that delimiter.
- If a text file contains one URL per line, treat each line as a separate JD.
- After parsing, show the detected job list and ask whether to generate all resumes or only selected items.

### 5. Analyze Fit And Ask Targeted Questions

Compare the experience pool against JD requirements.

- In batch mode, aggregate repeated gaps first so the user is not asked the same question multiple times.
- Label evidence as `strong match`, `weak match`, or `missing`.
- Prioritize questions that can materially improve fit or credibility.

Ask at most one to three concise questions at a time.

- Anchor questions to the JD requirement.
- Give concrete recall cues tied to the user's known background.
- Ask about evidence, scope, ownership, tools, and measurable outcomes.

Add confirmed user details back into the experience pool before drafting. If the user does not confirm an item, keep it as an explicit gap instead of guessing.

### 6. Draft The Tailored Resume

Write the resume in Chinese and keep it to one page after document rendering.

Use a structure close to:

```text
# 姓名
[联系方式]

## 个人简述
[2-3 句，直接对应目标岗位]

## 教育经历

## 专业技能

## 相关经历

## 荣誉与成果
```

Adapt section titles if the target role benefits from clearer grouping.

Apply these writing rules:

- Reorder content by relevance to the target role.
- Rewrite rather than copy-paste raw bullets.
- Use STAR-style bullets: context or challenge -> action -> measurable result.
- Keep only evidence that helps this application.
- Reuse contact, education, and factual history from source materials without embellishment.
- Surface the strongest, most role-relevant evidence first.

In batch mode, generate a separate resume draft for each JD.

### 7. Generate Output Files

Create a temporary Markdown file named `简历_<岗位名称>_temp.md` in the working directory with `apply_patch`.

Convert it to Word with `pandoc`.

- Base command: `pandoc temp.md -o 简历_<岗位名称>.docx --from markdown --to docx`
- If `style_reference` exists, add `--reference-doc=<path>`

Delete the temporary Markdown file after successful conversion.

If `python-docx` is already available, optionally apply the Chinese kinsoku and punctuation fix from the original workflow. If it is unavailable, skip that polish step and mention it briefly instead of blocking the task.

If `generate_pdfs.py` exists in the working directory:

- Inspect the script before editing it.
- Add the new resume only if the script is clearly designed for that pattern.
- Run it after updating.
- If the script is custom or risky to patch automatically, leave it alone and tell the user PDF generation needs manual follow-up.

If `pandoc` is missing, stop and tell the user instead of pretending the document was generated.

### 8. Report Results

Summarize in Chinese:

- Target role or roles
- Which experiences were selected and why
- Remaining gaps that could still weaken the application
- Output file paths
- Which document, if any, was used as the style reference

For batch mode, prefer a compact table with one row per job.

## Tooling Rules

Use the Codex toolset rather than Claude-specific tooling.

- Use `exec_command` for local file discovery, extraction commands, and document conversion.
- Use `web` tools only for online JD pages or other internet content.
- Use `view_image` for local JD screenshots.
- Use `apply_patch` for creating or editing local Markdown, cache, or helper files.

## Quality Rules

- Keep the user interaction in Chinese.
- Keep questions focused and low-friction.
- Do not claim skills or outcomes that are not supported by source material or user confirmation.
- Prefer concrete evidence and quantified outcomes over keyword stuffing.
- Explicitly warn when extraction quality is degraded by scanned PDFs, screenshots, or missing Word sources.
