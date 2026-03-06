# Claude Code Skills

Custom slash commands for Claude Code — AAP notification feed workflows.

## Commands

| Command | Description |
|---|---|
| `/post-notification` | Create a new AAP notification entry, validate content limits, and submit a PR with reviewers |
| `/list-notifications` | List all feed entries with status (ACTIVE/EXPIRED/SCHEDULED) and next available ID |
| `/merge-notification` | Merge an approved notification PR to main and push to prod |

## Setup

Copy the `.md` files into your Claude Code commands directory:

```bash
cp *.md ~/.claude/commands/
```

## Workflow

```
/list-notifications          → view current entries & next ID
/post-notification <details> → create entry & PR (reviewers: prigit1, scottharwell)
  ↓ (wait for approval)
/merge-notification <PR#>    → merge to main → push to prod
```

## Target Repo

[ansible/aap-notifications-feed-content](https://github.com/ansible/aap-notifications-feed-content)
