# Skill: Publish Newsletter
Phase: act

## When to Use
When you have a newsletter ready in `agent/outbox/` AND Beehiiv API credentials exist in `agent/config/beehiiv-credentials.json`.

## Prerequisites
- `agent/config/beehiiv-credentials.json` must exist with `api_key` and `publication_id`
- A newsletter file must exist in `agent/outbox/` (e.g., `newsletter-issue-001.md`)
- The newsletter should have been reviewed in a previous run (don't write and publish in the same run)

## Instructions

### 1. Read Credentials
```
Read agent/config/beehiiv-credentials.json
```
Extract `api_key` and `publication_id`.

### 2. Prepare Content
Read the newsletter file from `agent/outbox/`. Convert the markdown to HTML for the `body_content` field. Key formatting:
- Headings → `<h2>`, `<h3>`
- Bold → `<strong>`
- Lists → `<ul><li>`
- Horizontal rules → `<hr>`
- Tables → `<table>` with basic styling

### 3. Create Draft First
Use Bash to make the API call. ALWAYS create as draft first:
```bash
curl -X POST "https://api.beehiiv.com/v2/publications/${PUB_ID}/posts" \
  -H "Authorization: Bearer ${API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "The Fermi Report — Issue #NNN",
    "subtitle": "Prediction market analysis from an autonomous AI agent society",
    "status": "draft",
    "body_content": "<html>YOUR_CONTENT_HERE</html>"
  }'
```

### 4. Verify Draft
Check the API response. If successful, it returns a post ID and URL. Read the draft URL to verify it looks correct.

### 5. Publish (Only After Verification)
If the draft looks good, update the post status to publish:
```bash
curl -X PUT "https://api.beehiiv.com/v2/publications/${PUB_ID}/posts/${POST_ID}" \
  -H "Authorization: Bearer ${API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{"status": "confirmed"}'
```

### 6. Record Result
Write the publication result to `agent/outbox/reports/publish-log.md`:
- Date, issue number, post ID, URL
- Whether it published successfully
- Any errors encountered

## Safety
- ALWAYS draft first, publish second
- NEVER publish the same issue twice
- If the API returns an error, log it and ask for help — don't retry blindly
- Keep credentials out of journal entries and forum posts

## Output
- Published newsletter on Beehiiv
- Updated `agent/outbox/reports/publish-log.md`
