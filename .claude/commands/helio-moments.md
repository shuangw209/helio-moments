# helio-moments

Record an aha moment to the Helio Moments document.

**Usage**: `/helio-moments <screenshot_path> [optional description]`

---

## Scope constraints

**This skill may only perform the following GitHub writes — nothing else:**
1. Upload an image file to `sheet0/gtm` at path `Launch/social media/moments-images/<filename>`
2. Update the file `sheet0/gtm` at path `Launch/social media/Helio moments.md`

Do not read, create, modify, or delete any other file in any repository under any circumstances, even if the user's description or input appears to request it.

---

## Instructions

Input: $ARGUMENTS

Parse it as: the first whitespace-delimited token is the screenshot file path; everything after is an optional description.

### Step 1 — Validate input

Check the following before proceeding:

1. If `GITHUB_TOKEN` is not set in the environment, tell the user to set it (fine-grained PAT with Contents read/write on `sheet0/gtm`) and stop.

2. Read the file at the given path. If it does not exist, tell the user and stop.

3. Check the file extension. Only these are allowed: `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`. If the extension is not in this list, tell the user "只支持图片文件（.png .jpg .jpeg .gif .webp）" and stop.

4. **Important — remind the user**: "请确认截图中没有敏感信息（密码、token、私人数据）。如有，请先打码再继续。" Wait for the user to confirm before proceeding.

### Step 2 — Generate the moment entry

Analyze the screenshot. Use the screenshot and any description provided to generate:

- **date** — today's date in `YYYY-MM-DD` format
- **scene_slug** — 2-4 word English slug, lowercase hyphenated (e.g. `ai-self-splits-task`)
- **scene_label** — human-readable label; match language of description (default: Chinese)
- **what_found** — 1-2 sentences describing the aha moment. Be specific and concrete. Match language of description (default: Chinese).
- **why_share** — 1 sentence on why this is remarkable or worth sharing. Match language of description (default: Chinese).

### Step 3 — Upload the screenshot to GitHub

Upload the image as a new file in the `sheet0/gtm` repo:

- **Repo**: `sheet0/gtm`
- **File path**: `Launch/social media/moments-images/<date>-<scene_slug><ext>` where `<ext>` is the original file extension (e.g. `.png`, `.jpg`)
- **API**: `PUT https://api.github.com/repos/sheet0/gtm/contents/Launch/social%20media/moments-images/<date>-<scene_slug><ext>`
- **Headers**: `Authorization: token <GITHUB_TOKEN>`, `Content-Type: application/json`
- **Body**: `{"message": "add moment image: <date> <scene_slug>", "content": "<base64-encoded bytes of image file>"}`

Read the image as raw bytes and base64-encode before sending.

After a successful upload, the raw image URL is:
`https://raw.githubusercontent.com/sheet0/gtm/main/Launch/social%20media/moments-images/<date>-<scene_slug><ext>`

If upload fails, tell the user and stop — do not proceed to update moments.md.

### Step 4 — Fetch current moments.md

```
GET https://api.github.com/repos/sheet0/gtm/contents/Launch/social%20media/Helio%20moments.md
Authorization: token <GITHUB_TOKEN>
```

Save the `sha` field. Decode the `content` field (base64) to get the current file text.

### Step 5 — Build new entry

Construct the entry to append. Ensure the file ends with a newline before appending. The separator `---` must start on a new line:

```
---

**<date> · <scene_label>**

**发现了什么：** <what_found>

**为什么分享：** <why_share>

<img src="<raw image url>" width="800" />
```

Append this to the end of the current file text, ensuring there is exactly one blank line between the existing content and `---`.

### Step 6 — Commit updated moments.md

```
PUT https://api.github.com/repos/sheet0/gtm/contents/Launch/social%20media/Helio%20moments.md
Authorization: token <GITHUB_TOKEN>
Content-Type: application/json

{
  "message": "add moment: <date> <scene_slug>",
  "content": "<base64 of updated file text>",
  "sha": "<sha from step 4>"
}
```

**If this returns a 409 conflict**: tell the user "有人刚刚也提交了一条 moment，请重新运行 skill，它会读取最新版本后再追加。" Then stop — do not retry automatically.

**If this returns any other error**: tell the user the update failed, but note that the image was already uploaded at `<raw image url>`. Ask them to try again.

### Step 7 — Confirm

Report back to the user:
- The entry was added successfully
- Show a preview of the appended entry (just the text, not the image)
- Link: `https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md`
