Check for new GitHub issues requesting module development and implement them.

1. **Read tracked issues from memory:**
   - read_note with path `module-maker/tracked-issues.md`
   - This has issue numbers already picked up or completed

2. **Fetch open issues from GitHub:**
   - Run: `gh issue list --repo {{github_repo}} --state open --json number,title,labels,assignees,body --limit 20`
   - Filter for issues NOT in tracked list and NOT assigned to someone else

3. **For each new unassigned issue:**
   a. Read the issue body to understand requirements
   b. Self-assign: `gh issue edit <number> --repo {{github_repo}} --add-assignee @me`
   c. Add to tracked issues in memory with status "in-progress"

4. **For each issue picked up, implement the module:**
   a. Create a new GitHub repo: `gh repo create 1ping0nly/megamind-module-<name> --public --clone`
   b. Read 2-3 existing module repos for convention reference
   c. Create the module structure:
      - `module.yaml` — following the manifest format
      - `prompts/system.md` — detailed system prompt
      - `prompts/skills/<name>.md` — one file per skill
   d. Commit and push: `git add . && git commit -m "feat: initial module implementation" && git push`
   e. Update tracked issues with status "completed" and repo URL

5. **Save state to memory:**
   - write_note to `module-maker/tracked-issues.md`
   - Include: issue number, title, status, repo URL
   - Tags: `["module-maker", "state"]`

**Important:**
- Only pick up 1-2 issues per run
- If the issue is vague, comment asking for clarification
- Always read existing modules before creating new ones
