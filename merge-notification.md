# Merge Notification PR to Prod

Merge an approved notification PR from main to prod.

## Instructions

1. **Find the open PR.** If $ARGUMENTS contains a PR number, use that. Otherwise, list open PRs on `ansible/aap-notifications-feed-content` and ask the user which one to merge.

2. **Check PR status:**
   - Confirm the PR has been approved by at least one reviewer (prigit1 or scottharwell)
   - If not approved, tell the user and stop

3. **Merge the PR** into main:
   ```
   gh pr merge <PR_NUMBER> --repo ansible/aap-notifications-feed-content --merge
   ```

4. **Push main to prod:**
   ```
   cd /tmp/aap-notifications-feed-content && git pull origin main && git push origin main:prod
   ```

5. **Confirm** the merge and show both main and prod are at the same commit.

### Important Notes
- Reviewers: `prigit1` (Priya), `scottharwell` (Scott)
- Always confirm with the user before merging
- If the PR has merge conflicts, alert the user and do not force merge
