<p>
  <a href="./README.md">
    <img alt="中文" src="https://img.shields.io/badge/语言-中文-1677ff">
  </a>
  <a href="./README.en.md">
    <img alt="English" src="https://img.shields.io/badge/Language-English-555555">
  </a>
</p>

# Tailor Resume for Codex

## ⚠️ 先说明

这不是 Codex App 本体，而是一个要安装到 Codex 里面使用的 skill。

也就是说，你需要先装好 Codex App，再按照下面的步骤安装这个 skill。

## 🖥️ 使用前先安装 Codex App

如果你还没有安装 Codex，可以先这样做：

1. 打开 OpenAI 官方 Codex 页面：[openai.com/codex](https://openai.com/codex/)
2. 点击页面上的 `Download` 下载 Codex App。
3. 按提示完成安装。
4. 打开 Codex App，并使用你的 ChatGPT 账号登录。
5. 登录成功后，再继续安装下面这个 `tailor-resume` skill。

如果你不确定自己的账号能不能用 Codex，最稳妥的方式是直接看 OpenAI 官方 Codex 页面上的最新说明。

这是一个给 Codex 用的简历定制 skill。

你可以把自己不同阶段、不同方向、不同版本的简历一起交给它，再把一个或一批目标岗位 JD 丢进去。它会先把所有简历内容整理成一个完整的“经历池”，再对照 JD 找 gap、主动追问你可能遗漏但其实做过的经历，最后按具体岗位重写简历，并输出可继续编辑的 Word 文档。

它不是简单地“改几个关键词”，而是把“多版本简历整理 + 批量 JD 分析 + gap 挖掘 + 针对性改写 + Word 输出”串成一个完整流程。

## 核心能力

### 1. 多版本简历 -> 经历池

你可以把所有版本的简历一起喂进去。无论是早期版本、不同岗位方向版本，还是某一版里写过后来删掉的内容，它都会统一提取出经历、项目、技能和成果，合并成一个完整的经历池。

### 2. 批量喂入 JD

你可以一次性丢给它多个 JD。支持文本、文件、链接、截图，甚至把 10 个岗位的 JD 截图丢进同一个文件夹里，它也会逐个读取、逐个分析。

### 3. 挖掘 gap 经历

它会把经历池和 JD 逐项对比，找出中间的 gap，然后主动问你问题。很多时候不是你没做过，而是你没想到这段经历可以写进这个岗位的简历里。它会帮你把这些可用但没写出来的经历挖出来。

### 4. 针对 JD 润色改写

它会按 STAR 原则重写你的经历，但不是模板式套话。它会根据这个具体 JD 调整侧重点、换用更贴近岗位需求的表达和关键词，让招聘方更快看出“你做过他们要的事情”。

### 5. 保留排版，输出 Word

最后它会输出 Word 文档。如果你有多个版本的 `.docx` 简历，还可以指定最喜欢的一份作为样式参考，让新简历继续沿用原来的字体、间距、页边距和整体版式。

## 🔧 再安装这个 skill

### 方式一：直接复制命令安装（推荐） 🚀

如果你平时会打开终端，这是最省事的方式。

1. 在 Mac 上打开“终端”。
如果你不知道在哪里打开，可以按 `Command + Space`，输入“终端”，然后回车。
2. 把下面这整段命令完整复制进去。
3. 按一次回车，等它安装完成。
4. 重启 Codex。

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo rongmiao926-hub/codex-tailor-resume-skill \
  --path tailor-resume
```

安装完成后，`tailor-resume` 会被放到你的 `~/.codex/skills/` 目录里。

### 方式二：手动安装 📁

如果你不想碰命令行，也可以手动复制文件：

1. 点击这个仓库右上角的 `Code`。
2. 选择 `Download ZIP` 下载压缩包。
3. 解压后，你会看到一个叫 `tailor-resume` 的文件夹。
4. 把这个文件夹复制到你电脑上的 `~/.codex/skills/` 目录里。
5. 重启 Codex。

如果你不知道 `~/.codex/skills/` 在哪里：

1. 在 Finder 顶部菜单点 `前往`。
2. 选择 `前往文件夹...`。
3. 输入 `~/.codex/skills/`。
4. 把 `tailor-resume` 文件夹拖进去。

## 💬 小白友好用法

装好以后，不需要背参数。你就像平时跟 Codex 说话一样，直接告诉它“帮我用 `tailor-resume` 改简历”，再把“简历放在哪”和“JD 放在哪”说清楚就行。

你可以直接这样说：

```text
帮我用 $tailor-resume 改简历。我的简历都放在 ~/Documents/简历库/，请先把所有版本整理成经历池，再根据下面这个产品经理 JD 帮我生成一份一页中文简历。JD 如下：...
```

```text
帮我用 $tailor-resume 改简历。我有多个岗位要投，简历在 ~/Documents/resumes/，JD 截图都在 ~/Documents/jd-screenshots/。请先统一分析 gap，再分别生成每个岗位的定制简历。
```

```text
帮我用 $tailor-resume 改简历。我的简历在 ~/Documents/resumes/，并且请沿用 ~/Documents/resumes/终版简历.docx 的排版风格。JD 链接在这里：https://example.com/job/12345
```

## 📝 说明

- 如果你只提供 PDF 简历，skill 可以提取内容，但通常无法完整复用原排版。
- 如果 JD 是截图或网页，它也会尽量解析，但质量会受原始内容清晰度和网页可读性影响。
- 如果至少提供一份 `.docx` 简历，Word 输出效果通常更好。
