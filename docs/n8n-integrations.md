# n8n integrations (optional Phase 1.5)

Host: <https://workflows.joshuaproject.net> (`stacks/shared/n8n/`)

No automation is required for Phase 1. These flows close the gap between Tolgee milestone progress and Asana task status.

## Flow A — Weekly open-projects digest

**Trigger:** Cron (Monday 09:00 UTC)

**Steps:**

1. HTTP Request → Tolgee API: list projects / activity (with PAT from 1Password)
2. Format summary (projects with untranslated keys, pending review)
3. Post to Slack or email coordinators (existing n8n channels)

**Asana:** Manual — coordinator updates task status from digest.

## Flow B — Tolgee webhook → Asana comment

**Trigger:** Tolgee webhook on `TRANSLATION_STATE_CHANGE` or export event (configure in Tolgee admin when webhooks are enabled)

**Steps:**

1. Receive webhook payload (project id, language, key count)
2. Lookup Asana task by custom field **Execution URL** or stored mapping table in n8n static data
3. Add comment: "Tolgee: {n} keys reached Reviewed for {lang}"

**Requires:** Mapping Tolgee project ID ↔ Asana task GID (spreadsheet or n8n Data Store).

## Flow C — New Asana task → comment with deep links

**Trigger:** Asana webhook on task created in Translation portfolio

**Steps:**

1. Parse project type custom field
2. If **App strings (Tolgee)**, append comment with Tolgee project URL template
3. If **Link Hub**, append admin editor URL pattern

## Security

- Store Tolgee PAT and Asana PAT in **JP N8N** or **JP Tolgee** vault; load via n8n credentials
- Verify Tolgee webhook signature if available
- Do not log translation text in n8n execution data for PII-sensitive keys

## Implementation note

Add workflow JSON exports under `jp-infrastructure/docs/n8n-workflows/` when implemented (mirror `jp-link-hub-events.json` pattern).
