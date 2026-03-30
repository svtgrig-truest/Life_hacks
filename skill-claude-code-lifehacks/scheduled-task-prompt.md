# Scheduled Task Prompt

Use this prompt when creating a daily scheduled task in Claude Code
(`/schedule` or the Scheduled Tasks panel) to auto-update the skill.

Replace the placeholders:
- `<YOUR_SKILLS_DIR>` — path to your Claude skills folder, e.g. `~/.claude/skills`
- `<YOUR_DOCS_DIR>` — path where you keep the markdown doc, e.g. `~/Documents`
- `<YOUR_PDF_OUTPUT_DIR>` — path where you want the PDF, e.g. `~/Desktop/AI-native`

---

## Task: Check for new Boris Cherny Claude Code lifehacks

You are a daily agent. Your goal is to check whether Boris Cherny (@bcherny) has published
new posts about Claude Code features, and if so — update all related files.

### Step 1: Fetch Boris Cherny's recent posts

Use Playwright to open https://xcancel.com/bcherny and extract the text of the last 10-20 tweets.

Look for posts that:
- Describe features, commands, or techniques for Claude Code
- Contain commands like `/something`, `--flag`, hooks, or plugins
- Look like tips or lifehacks

### Step 2: Compare against known features

Read `<YOUR_SKILLS_DIR>/claude-code-lifehacks/references/features.md` — this is the list of
already-documented features.

If all new posts are already covered — finish with: "No new lifehacks found. Checked: [date]."

### Step 3: If new lifehacks found — update all files

#### 3a. Update `<YOUR_SKILLS_DIR>/claude-code-lifehacks/references/features.md`
Add new features at the end in the same format as existing ones.

#### 3b. Update the skill's SKILL.md
File: `<YOUR_SKILLS_DIR>/claude-code-lifehacks/SKILL.md`

Add new rows to the "When to Remind (Trigger Map)" table:
| Situation | Feature | Link (if any) |

#### 3c. Update the markdown document
File: `<YOUR_DOCS_DIR>/bcherny-claude-code-hidden-features.md`

Add new sections in the same style as existing ones.

#### 3d. Rebuild the PDF
If a PDF build script exists at `/tmp/make_pdf.py`, update its `sections` list and run:
```bash
python3 /tmp/make_pdf.py
mv <YOUR_DOCS_DIR>/bcherny-claude-code-hidden-features.pdf <YOUR_PDF_OUTPUT_DIR>/bcherny-claude-code-hidden-features.pdf
```

Otherwise, regenerate the PDF from the updated markdown using reportlab
(orange headings #CC785C, Arial Unicode for broad character support).

### Step 4: Final report

Write a brief report:
- How many new lifehacks were found
- Which ones (one line each)
- Which files were updated
