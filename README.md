# helio-moments

Claude Code skill for recording Helio aha moments — no manual editing needed.

## What it does

When you spot a moment worth sharing — an AI doing something surprising, a workflow that just clicks, a "wait, this team is different" feeling — run the skill. It handles the rest: generates the description, uploads your screenshot, and commits the entry to the Helio Moments doc.

## Setup

1. Clone this repo (or add it to your Claude Code project):
   ```bash
   git clone https://github.com/shuangw209/helio-moments.git
   ```

2. Set your GitHub token (needs `repo` scope on `sheet0/gtm`):
   ```bash
   export GITHUB_TOKEN=ghp_...
   ```

3. Open Claude Code in the project directory — it will auto-detect `.claude/commands/helio-moments.md`.

## Usage

In Claude Code:

```
/helio-moments <screenshot_path> [optional description]
```

**Examples:**

```
/helio-moments ~/Desktop/screenshot.png
/helio-moments ~/Desktop/screenshot.png AI 自己商量好分工，没人指挥
/helio-moments /tmp/capture.png The AI fixed the bug while I was sleeping
```

The skill will:
1. Analyze your screenshot
2. Generate a moment entry (date, scene, what you found, why it's worth sharing)
3. Upload the image to `sheet0/gtm`
4. Append the entry to [Helio moments.md](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
5. Commit and give you a link

## Output format

Each recorded moment looks like this:

```
---

**2026-04-16 · AI 自发分工**

**发现了什么：** 两个 AI 没人指挥就商量好谁做什么，像真实团队一样互相补位。

**为什么分享：** 第一次感觉这个团队真的不一样了。

[screenshot]
```

## Where moments live

All entries are stored in:
[`sheet0/gtm / Launch / social media / Helio moments.md`](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
