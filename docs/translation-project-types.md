# Translation project types (Asana)

**Asana** is the program layer. Each task uses exactly one **project type** custom field (or section) to route work to the correct execution tool.

## Custom fields (recommended)

| Field | Type | Values / notes |
|-------|------|----------------|
| Project type | Single select | See types below |
| Target language | Single select | BCP-47 or ISO codes you support (en, es, pt, ko, …) |
| Execution URL | URL | Deep link to Tolgee project, link-hub editor, Excel path, etc. |
| Reviewer | Person | Human gate before done |
| Target repo / app | Text | e.g. `jp-adopt-forms`, `unreached-of-day-website` |
| Definition of done | Text | See per-type below |

## Project types

### App strings (Tolgee)

| | |
|---|---|
| **Execution** | Tolgee project at `https://tolgee.joshuaproject.net` |
| **When to use** | next-intl JSON namespaces, UI labels, form copy, email strings in Next.js apps |
| **Asana tracks** | Languages, ship date, reviewer, link to Tolgee project |
| **Definition of done** | All keys **Translated** or **Reviewed** in Tolgee; `tolgee pull` merged to target repo; CI green |

### Link Hub page

| | |
|---|---|
| **Execution** | jp-link-hub admin → page editor → Translations section |
| **When to use** | Public link_list / resource_kit page overlays |
| **Asana tracks** | Page URL, `?lang=` code, reviewer |
| **Definition of done** | Overlay reviewed and published; public URL verified |

### Unreached-of-day batch

| | |
|---|---|
| **Execution** | `unreached-of-day-website` Excel export/import utilities |
| **When to use** | Bulk JSON string updates across UOTD locales |
| **Asana tracks** | Language file, volunteer, PR link |
| **Definition of done** | Import merged; site smoke-tested for locale |

### Document / handout

| | |
|---|---|
| **Execution** | DeepL Document, shared drive, or future CMS — **not** Tolgee by default |
| **When to use** | PDFs, Word handouts, long markdown articles |
| **Asana tracks** | Source file link, format, reviewer |
| **Definition of done** | Final file in agreed location; stakeholders signed off |

### Main site article (future)

| | |
|---|---|
| **Execution** | TBD — jp-content CMS i18n or dedicated doc workflow |
| **When to use** | `joshuaproject` Laravel markdown pages at scale |
| **Asana tracks** | Page slug, locale, spike outcome |
| **Definition of done** | Per spike / CMS decision |

## Routing rules

1. **Default for Next.js UI copy** → App strings (Tolgee)
2. **Link Hub public page body** → Link Hub page (do not duplicate in Tolgee)
3. **UOTD JSON bulk** → UOTD batch
4. **Long-form or print** → Document / handout
5. **Unclear** → Coordinator picks type in intake; document in task description

## Status workflow (Asana)

Suggested sections or status values:

1. **Backlog** — approved but not started
2. **In progress** — work happening in execution tool
3. **In review** — reviewer assigned
4. **Done** — definition of done met
5. **Blocked** — waiting on source content, access, or glossary decision

Tolgee key-level progress stays in Tolgee; Asana tracks **milestone** status only unless n8n automation is added (see [n8n-integrations.md](n8n-integrations.md)).
