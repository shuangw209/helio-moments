# helio-moments

Record an aha moment to the Helio Moments document.

**Usage**: `/helio-moments <screenshot_path> [optional description]`

---

## Instructions

Input: $ARGUMENTS

Parse it as: the first whitespace-delimited token is the screenshot file path; everything after is an optional description.

### Step 1 — Validate input

Read the image file at the given path. If the file does not exist, tell the user and stop.

If `GITHUB_TOKEN` is not set in the environment, tell the user to set it (needs `repo` scope on `sheet0/gtm`) and stop.

### Step 2 — Generate the moment entry

Analyze the screenshot. Use the screenshot and any description provided to generate:

- **date** — today's date in `YYYY-MM-DD` format
- **scene_slug** — 2-4 word English slug, lowercase hyphenated (e.g. `ai-self-splits-task`)
- **scene_label** — human-readable label; match language of description (default: Chinese)
- **what_found** — 1-2 sentences describing the aha moment. Be specific and concrete. Match language of description (default: Chinese).
- **why_share** — 1 sentence on why this is remarkable or worth sharing. Match language of description (default: Chinese).

### Step 3 — Upload the screenshot to GitHub

Upload the image as a new file in the `sheet0/gtm` repo under the images folder:

- **Repo**: `sheet0/gtm`
- **File path**: `Launch/social media/moments-images/<date>-<scene_slug>.png`
- **API**: `PUT https://api.github.com/repos/sheet0/gtm/contents/Launch/social%20media/moments-images/<date>-<scene_slug>.png`
- **Headers**: `Authorization: token <GITHUB_TOKEN>`, `Content-Type: application/json`
- **Body**: `{"message": "add moment image: <date> <scene_slug>", "content": "<base64-encoded bytes of image file>"}`

Read the image as raw bytes and base64-encode before sending.

After a successful upload, the raw image URL is:
`https://raw.githubusercontent.com/sheet0/gtm/main/Launch/social%20media/moments-images/<date>-<scene_slug>.png`

### Step 4 — Fetch current moments.md

```
GET https://api.github.com/repos/sheet0/gtm/contents/Launch/social%20media/Helio%20moments.md
Authorization: token <GITHUB_TOKEN>
```

Save the `sha` field. Decode the `content` field (base64) to get the current file text.

### Step 5 — Build new entry

Construct the entry to append (add a blank line before `---` if the file does not already end with one):

```
---

**<date> · <scene_label>**

**发现了什么：** <what_found>

**为什么分享：** <why_share>

<img src="<raw image url>" width="800" />
```

Append this to the end of the current file text.

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

### Step 7 — Confirm

Report back to the user:
- The entry was added successfully
- Show a preview of the appended entry (just the text, not the image)
- Link: `https://github.com/sheet0/gtm/blob/main/Launch/social%20media/Helio%20moments.md`
