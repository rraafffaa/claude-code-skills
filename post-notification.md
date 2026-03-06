# Post AAP Notification

Create a new notification entry in the AAP notifications feed and submit a PR for review.

## Instructions

You are creating a new entry in the `public/feed.atom` file in the `ansible/aap-notifications-feed-content` GitHub repo.

### Required Input from User: $ARGUMENTS

The user will provide the notification details in this format:
```
title: <title>
summary: <summary, max 300 characters>
content: <HTML content for the notification, max 300 characters>
link: <URL to related article/doc>
category: <general|upgrades|new-release|maintenance>
deployment_type: <all|managed-azure|saas-aws|self-managed>
unpublish: <date in YYYY-MM-DD format>
```

If the user provides free-form text instead, extract the relevant fields and ask for confirmation before proceeding.

### Steps

1. **Clone the repo** (if not already cloned):
   ```
   cd /tmp && git clone https://github.com/ansible/aap-notifications-feed-content.git
   ```

2. **Determine the next ID** by reading `public/feed.atom` and finding the highest existing ID number in `tag:announcements.ansiblecloud.redhat.com,2025:/feed/<N>`. The new entry gets `N+1`.

3. **Validate the notification:**
   - The `<summary>` text MUST be 300 characters or fewer. Count and confirm.
   - The `<content>` inner text MUST be 300 characters or fewer. Count and confirm.
   - If either exceeds 300 characters, show the count and ask the user to shorten it. Do NOT proceed.

4. **Create a new branch** named `notification/<N+1>-<slugified-title>` from `main`.

5. **Insert the new entry** in `public/feed.atom` as the FIRST `<entry>` element (right after the `<id>` tag of the feed header). Use this template:

```xml
  <entry>
    <title>TITLE_HERE</title>
    <category term="CATEGORY_TERM" label="CATEGORY_LABEL" />
    <link rel="alternate" type="text/html" href="LINK_HERE"/>
    <id>tag:announcements.ansiblecloud.redhat.com,2025:/feed/NEW_ID</id>
    <updated>PUBLISH_DATETIME</updated>
    <summary>SUMMARY_HERE</summary>
    <content type="html"><![CDATA[
      CONTENT_HTML_HERE
    ]]></content>
    <aap:notification>
      <aap:title>TITLE_HERE</aap:title>
      <aap:description type="html"><![CDATA[
        CONTENT_HTML_HERE
      ]]></aap:description>
      <aap:deployment_type>DEPLOYMENT_TYPE</aap:deployment_type>
      <aap:publish>PUBLISH_DATETIME</aap:publish>
      <aap:unpublish>UNPUBLISH_DATETIMEZ</aap:unpublish>
    </aap:notification>
  </entry>
```

- `PUBLISH_DATETIME` = current UTC time in ISO 8601 format (e.g., `2026-03-06T17:00:00Z`)
- `UNPUBLISH_DATETIMEZ` = the user-provided unpublish date at `T23:59:59Z`
- Also update the feed-level `<updated>` timestamp to the new publish time.

6. **Commit and push** the branch.

7. **Create a PR** with:
   - Title: `Add notification: <title>`
   - Body: Include the notification summary and a preview of the entry
   - Reviewers: `prigit1` and `scottharwell`

8. **Show the PR URL** to the user.

9. **Do NOT merge.** Tell the user: "PR is ready for review. Once Priya and Scott approve, run `/merge-notification` to merge to prod."

### Important Notes
- The repo is at: `https://github.com/ansible/aap-notifications-feed-content`
- Reviewers: `prigit1` (Priya), `scottharwell` (Scott)
- The feed XML uses the `aap:` namespace (`xmlns:aap="https://announcements.ansiblecloud.redhat.com/ns/aap/v1"`)
- Entry IDs are sequential integers — always check the current max before creating
- Duplicate IDs have occurred before (two entries use `/feed/6`) — avoid this
