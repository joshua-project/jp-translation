# Asana templates

Create a **Translation** portfolio (or team) in Asana. Use **task templates** or duplicate tasks from this doc.

## Portfolio structure

```
Translation (portfolio)
├── App strings — Tolgee
├── Link Hub pages
├── Unreached of the Day
└── Documents & handouts
```

## Template: App strings (Tolgee)

**Task name:** `[App strings] {app} → {language}`  
Example: `[App strings] jp-adopt-forms → Spanish`

**Project type:** App strings (Tolgee)

**Description template:**

```markdown
## Goal
Translate app UI strings for {app} into {language}.

## Execution
- Tolgee project: {tolgee_project_url}
- Target repo: {github_repo}
- Design spec: https://github.com/joshua-project/jp-adopt-forms/blob/main/docs/plans/2026-03-25-tolgee-integration-design.md

## Assignees
- Translator: @
- Reviewer: @

## Definition of done
- [ ] All new/changed keys machine-translated or manually translated in Tolgee
- [ ] Reviewer marked strings Translated/Reviewed
- [ ] `tolgee pull` merged to dev (Phase 2+)
- [ ] Staging verified

## Notes
(Glossary links, tone, terminology)
```

**Subtasks (optional):**

1. Push latest English keys to Tolgee
2. Review machine translations
3. In-context review on staging (Phase 2+)
4. Merge translation sync PR

## Template: Link Hub page

**Task name:** `[Link Hub] {page title} → {language}`

**Description template:**

```markdown
## Page
- Admin editor: https://go.joshuaproject.net/admin/pages/{page_id}
- Public URL: {canonical_url}?lang={bcp47}

## Definition of done
- [ ] Overlay generated and edited in admin
- [ ] Reviewer approved copy
- [ ] Published; public URL checked
```

## Template: UOTD batch

**Task name:** `[UOTD] {language} string update — {sprint or date}`

**Description template:**

```markdown
## Workflow
1. Export: unreached-of-day-website/utilities/export-translations.js
2. Translate in Excel
3. Import: utilities/import-translations.js
4. PR to main

## Definition of done
- [ ] PR merged
- [ ] Locale spot-checked on site
```

## Template: Document / handout

**Task name:** `[Document] {title} → {language}`

**Description template:**

```markdown
## Source
- File: {link to SharePoint/Drive/source}

## Execution
- [ ] DeepL Document or manual translation
- [ ] Reviewer sign-off
- [ ] Final PDF/DOCX uploaded to {location}
```

## Intake form (optional)

Asana **form** fields:

1. What are you translating? (dropdown: project types)
2. Target language
3. Source link or repo
4. Deadline
5. Reviewer email

Coordinator creates a typed task from submissions and fills **Execution URL**.
