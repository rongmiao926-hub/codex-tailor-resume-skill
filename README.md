# Tailor Resume for Codex

## 中文介绍

这是一个给 Codex 用的简历定制 skill。

你可以把自己不同阶段、不同方向、不同版本的简历一起交给它，再把一个或一批目标岗位 JD 丢进去。它会先把所有简历内容整理成一个完整的“经历池”，再对照 JD 找 gap、主动追问你可能遗漏但其实做过的经历，最后按具体岗位重写简历，并输出可继续编辑的 Word 文档。

它不是简单地“改几个关键词”，而是把“多版本简历整理 + 批量 JD 分析 + gap 挖掘 + 针对性改写 + Word 输出”串成一个完整流程。

## English Overview

This is a Codex skill for tailoring resumes to specific job descriptions.

You can feed it multiple versions of your resume from different time periods or career directions, plus one or many target JDs. It builds a single experience pool from all resume versions, compares that pool against the JD requirements, asks follow-up questions to uncover missing but relevant evidence, rewrites your experience for the exact role, and outputs an editable Word document.

This is not just keyword swapping. It is a full workflow for consolidating resume history, batch-reading JDs, surfacing gaps, rewriting with intent, and producing a polished `.docx` resume.

## 核心能力 / Key Capabilities

### 1. 多版本简历 -> 经历池

你可以把所有版本的简历一起喂进去。
无论是早期版本、不同岗位方向版本，还是某一版里写过后来删掉的内容，它都会统一提取出经历、项目、技能和成果，合并成一个完整的经历池。

Feed in every version of your resume. The skill extracts experience, projects, skills, and achievements across all versions and merges them into one reusable experience pool, including items that were removed from later drafts.

### 2. 批量喂入 JD

你可以一次性丢给它多个 JD。
支持文本、文件、链接、截图，甚至把 10 个岗位的 JD 截图丢进同一个文件夹里，它也会逐个读取、逐个分析。

Feed in JDs in bulk. It can process pasted text, local files, links, and screenshots, including folders that contain many JD screenshots or documents.

### 3. 挖掘 gap 经历

它会把经历池和 JD 逐项对比，找出中间的 gap，然后主动问你问题。
很多时候不是你没做过，而是你没想到这段经历可以写进这个岗位的简历里。它会帮你把这些可用但没写出来的经历挖出来。

It compares your experience pool against the JD, identifies the gaps, and asks targeted follow-up questions. This often surfaces relevant experience you actually have but did not think to include or position for that role.

### 4. 针对 JD 润色改写

它会按 STAR 原则重写你的经历，但不是模板式套话。
它会根据这个具体 JD 调整侧重点、换用更贴近岗位需求的表达和关键词，让招聘方更快看出“你做过他们要的事情”。

It rewrites experience using STAR logic, but not as generic filler. It changes emphasis, wording, and keywords around the specific JD so the reader quickly sees that you have done the work they need.

### 5. 保留排版，输出 Word

最后它会输出 Word 文档。
如果你有多个版本的 `.docx` 简历，还可以指定最喜欢的一份作为样式参考，让新简历继续沿用原来的字体、间距、页边距和整体版式。

It outputs an editable Word document. If you provide one or more `.docx` resumes, you can choose a preferred style reference so the generated resume reuses that layout, spacing, and typography.

## Install

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

Install 完成后，重启 Codex。
Restart Codex after installation.

## 小白友好用法 / Beginner-Friendly Usage

装好以后，不需要背参数。
你就像平时跟 Codex 说话一样，把“简历在哪”和“目标 JD 是什么”告诉它就行。

You do not need to memorize a strict command format. Just talk to Codex naturally and tell it where your resumes are and what job you are targeting.

你可以直接这样说：

```text
使用 $tailor-resume，把 ~/Documents/简历库/ 里的所有简历都整理成经历池，再根据下面这个产品经理 JD 帮我生成一份一页中文简历。JD 如下：...
```

```text
使用 $tailor-resume，我有多个岗位要投。简历在 ~/Documents/resumes/，JD 截图都在 ~/Documents/jd-screenshots/。请先统一分析 gap，再分别生成每个岗位的定制简历。
```

```text
使用 $tailor-resume，帮我针对这个岗位改简历，并且沿用 ~/Documents/resumes/终版简历.docx 的排版风格。JD 链接在这里：https://example.com/job/12345
```

You can also say things like:

```text
Use $tailor-resume. My resumes are in ~/Documents/resumes/. Build one experience pool from all of them, compare it against this JD, ask me about any missing but important experience, and generate a one-page resume in Word.
```

## Notes

- 如果你只提供 PDF 简历，skill 可以提取内容，但通常无法完整复用原排版。
- 如果 JD 是截图或网页，它也会尽量解析，但质量会受原始内容清晰度和网页可读性影响。
- Word output is best when at least one source resume is provided as `.docx`.
