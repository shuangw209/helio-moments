# helio-moments

[English](#english) | [中文](#中文)

---

## English

Claude Code skill for recording Helio aha moments — no manual editing needed.

### What it does

When you spot a moment worth sharing — an AI doing something surprising, a workflow that just clicks, a "wait, this team is different" feeling — run the skill. It handles the rest: generates the description, uploads your screenshot, and commits the entry to the Helio Moments doc.

### Setup

1. Clone this repo (or add it to your Claude Code project):
   ```bash
   git clone https://github.com/shuangw209/helio-moments.git
   ```

2. Set your GitHub token (needs `repo` scope on `sheet0/gtm`):
   ```bash
   export GITHUB_TOKEN=ghp_...
   ```

3. Open Claude Code in the project directory — it will auto-detect `.claude/commands/helio-moments.md`.

### Usage

In Claude Code:

```
/helio-moments <screenshot_path> [optional description]
```

**Examples:**

```
/helio-moments ~/Desktop/screenshot.png
/helio-moments ~/Desktop/screenshot.png AI sorted out the split without being told
/helio-moments /tmp/capture.png The AI fixed the bug while I was sleeping
```

The skill will:
1. Analyze your screenshot
2. Generate a moment entry (date, scene, what you found, why it's worth sharing)
3. Upload the image to `sheet0/gtm`
4. Append the entry to [Helio moments.md](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
5. Commit and give you a link

### Output format

Each recorded moment looks like this:

```
---

**2026-04-16 · AI 自发分工**

**发现了什么：** 两个 AI 没人指挥就商量好谁做什么，像真实团队一样互相补位。

**为什么分享：** 第一次感觉这个团队真的不一样了。

[screenshot]
```

### Where moments live

All entries are stored in:
[`sheet0/gtm / Launch / social media / Helio moments.md`](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)

---

## 中文

用于记录使用 Helio 时灵光一现时刻的 Claude Code skill，无需手动编辑文档。

### 功能介绍

当你遇到值得分享的瞬间——AI 做了出乎意料的事、某个工作流突然顺了、或者那种"等等，这个团队真的不一样了"的感觉——跑一下这个 skill，剩下的它来处理：自动生成描述、上传截图、提交到 Helio Moments 文档。

### 安装

1. Clone 这个 repo（或加入你的 Claude Code 项目）：
   ```bash
   git clone https://github.com/shuangw209/helio-moments.git
   ```

2. 设置 GitHub Token（需要 `sheet0/gtm` 仓库的 `repo` 权限）：
   ```bash
   export GITHUB_TOKEN=ghp_...
   ```

3. 在项目目录里打开 Claude Code——会自动识别 `.claude/commands/helio-moments.md`。

### 使用方法

在 Claude Code 里输入：

```
/helio-moments <截图路径> [可选描述]
```

**示例：**

```
/helio-moments ~/Desktop/screenshot.png
/helio-moments ~/Desktop/screenshot.png AI 自己商量好分工，没人指挥
/helio-moments /tmp/capture.png 睡觉的时候 AI 把 bug 修完了
```

skill 会自动：
1. 分析截图内容
2. 生成 moment 条目（日期、场景、发现了什么、为什么值得分享）
3. 把图片上传到 `sheet0/gtm`
4. 追加条目到 [Helio moments.md](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
5. commit 并返回链接

### 输出格式

每条记录格式如下：

```
---

**2026-04-16 · AI 自发分工**

**发现了什么：** 两个 AI 没人指挥就商量好谁做什么，像真实团队一样互相补位。

**为什么分享：** 第一次感觉这个团队真的不一样了。

[截图]
```

### 记录存放位置

所有 moments 写入：
[`sheet0/gtm / Launch / social media / Helio moments.md`](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
