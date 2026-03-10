# Codex Tailor Resume Skill

`tailor-resume` is a Codex skill for tailoring resumes against one or more job descriptions.

## Install

With Codex's GitHub skill installer:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo rongmiao926-hub/codex-tailor-resume-skill \
  --path tailor-resume
```

Manual install:

```bash
cp -R tailor-resume ~/.codex/skills/
```

Restart Codex after installation.

## Usage

Invoke the skill in Codex with a prompt such as:

```text
使用 $tailor-resume，根据我提供的简历材料和目标 JD，补问缺失信息并生成一份定制简历。
```
