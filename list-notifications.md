# List AAP Notifications

Show all current entries in the AAP notifications feed.

## Instructions

1. **Clone or update the repo:**
   ```
   cd /tmp && (cd aap-notifications-feed-content && git pull origin main 2>/dev/null || cd /tmp && git clone https://github.com/ansible/aap-notifications-feed-content.git)
   ```

2. **Read `public/feed.atom`** from the `main` branch.

3. **Parse and display all entries** in a table with these columns:
   - **ID** — the number from `tag:announcements.ansiblecloud.redhat.com,2025:/feed/<N>`
   - **Title** — the entry title
   - **Category** — the category term
   - **Deployment Type** — from `<aap:deployment_type>`
   - **Published** — the `<updated>` date
   - **Unpublish** — from `<aap:unpublish>`
   - **Status** — "ACTIVE" if current date is between publish and unpublish, "EXPIRED" if past unpublish date, "SCHEDULED" if before publish date

4. **Sort by ID descending** (newest first).

5. **Show the next available ID** at the bottom: "Next available ID: N+1"

6. **Flag any issues:**
   - Duplicate IDs
   - Expired entries still in the feed
   - Missing required fields
