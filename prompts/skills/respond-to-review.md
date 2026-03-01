Check for review feedback on open module PRs and address comments.

1. **Read tracked issues from memory:**
   - read_note with path `module-maker/tracked-issues.md`
   - Filter for issues with status "pr-open"

2. **For each open PR, check for new review comments:**
   - Run: `gh pr view <pr-number> --repo <repo> --json reviews,comments,reviewRequests`
   - Run: `gh api repos/<repo>/pulls/<pr-number>/comments --jq '.[] | {id, body, path, line, created_at}'`
   - Compare timestamps against last check (from memory)

3. **For each new review comment:**
   a. Clone or pull the repo
   b. Read the comment and the file being commented on
   c. Make the requested change
   d. Commit: `git commit -am "fix: address review feedback"`
   e. Push: `git push`

4. **If a PR is approved and all checks pass:**
   - Update tracked issues with status "approved"
   - Comment: "All review feedback addressed. Ready for merge."

5. **Save state to memory:**
   - write_note to `module-maker/tracked-issues.md`
   - Update last-review-check timestamp
   - Tags: `["module-maker", "state"]`

**Important:**
- If you disagree with a comment, explain your reasoning in a reply
- Always pull latest before making changes
- Keep commits atomic — one commit per review comment
