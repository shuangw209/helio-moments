# helio-moments

[English](#english) · [中文](#中文)

---

## English

Claude Code skill for recording Helio aha moments — no manual editing needed.

### What it does

When you spot a moment worth sharing — an AI doing something surprising, a workflow that just clicks, a "wait, this team is different" feeling — run the skill. It handles the rest: generates the description, uploads your screenshot, and commits the entry to the Helio Moments doc.

### Setup

1. Clone this repo:
   ```bash
   git clone https://github.com/shuangw209/helio-moments.git
   ```

2. Get a GitHub access token (one-time setup):
   - Go to https://github.com/settings/tokens/new
   - Give it any name (e.g. "helio-moments")
   - Check the **repo** box
   - Click **Generate token** and copy it
   - Add it to your shell profile so it's always available:
   ```bash
   echo 'export GITHUB_TOKEN=ghp_your_token_here' >> ~/.zshrc && source ~/.zshrc
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
/helio-moments ~/Desktop/screenshot.png AI self-organized without instructions
/helio-moments /tmp/capture.png The AI fixed the bug while I was sleeping
```

The skill will:
1. Analyze your screenshot
2. Generate a moment entry (date, scene, what you found, why it's worth sharing)
3. Upload the image to `sheet0/gtm`
4. Append the entry to [Helio moments.md](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
5. Commit and give you a link

### Output format

```
---

**2026-04-16 · AI self-organized**

**发现了什么：** Two AIs divided the work without anyone telling them to.

**为什么分享：** First time the team felt truly different.

[screenshot]
```

### Where moments live

All entries are stored in:
[`sheet0/gtm / Launch / social media / Helio moments.md`](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)

---

## 中文

Claude Code skill，记录 Helio 的 aha moment，无需手动编辑文档。

### 功能说明

当你看到一个值得分享的瞬间——AI 做了让你意外的事、某个协作流程突然顺了、或者那种"等等，这个团队真的不一样了"的感觉——跑一下这个 skill，剩下的交给它：自动生成描述、上传截图、提交到 Helio Moments 文档。

### 安装

1. Clone 这个仓库：
   ```bash
   git clone https://github.com/shuangw209/helio-moments.git
   ```

2. 获取 GitHub 访问凭证（一次性配置）：
   - 打开 https://github.com/settings/tokens/new
   - 随便起个名字（比如 "helio-moments"）
   - 勾选 **repo** 选项
   - 点 **Generate token**，复制生成的 token
   - 把它加到 shell 配置里，以后不用重复设置：
   ```bash
   echo 'export GITHUB_TOKEN=ghp_你的token' >> ~/.zshrc && source ~/.zshrc
   ```

3. 在项目目录打开 Claude Code，它会自动识别 `.claude/commands/helio-moments.md`。

### 用法

在 Claude Code 里输入：

```
/helio-moments <截图路径> [可选描述]
```

**示例：**

```
/helio-moments ~/Desktop/screenshot.png
/helio-moments ~/Desktop/screenshot.png AI 自己商量好分工，没人指挥
/helio-moments /tmp/capture.png 我睡觉的时候 AI 把 bug 修好了
```

skill 会自动：
1. 分析截图内容
2. 生成 moment 条目（日期、场景、发现了什么、为什么分享）
3. 上传图片到 `sheet0/gtm`
4. 追加条目到 [Helio moments.md](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
5. commit 并返回链接

### 输出格式

```
---

**2026-04-16 · AI 自发分工**

**发现了什么：** 两个 AI 没人指挥就商量好谁做什么，像真实团队一样互相补位。

**为什么分享：** 第一次感觉这个团队真的不一样了。

[截图]
```

### Moments 存放位置

所有条目保存在：
[`sheet0/gtm / Launch / social media / Helio moments.md`](https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md)
