# Content-type matrix

When to use Tolgee vs existing Joshua Project translation paths.

## Summary

| Content | Platform | Phase 1 |
|---------|----------|---------|
| Next.js app UI (adopt-forms, future jp-content) | **Tolgee** | Infra + Asana; app wiring Phase 2 |
| Link Hub page bodies | **jp-link-hub admin** | Unchanged |
| Unreached-of-day JSON | **Excel workflow** | Unchanged |
| Main site markdown | **Spike / CMS** | Not Tolgee yet |
| PDFs / handouts | **DeepL Document / manual** | Asana project type only |

## Tolgee — excellent fit

- UI labels, buttons, validation messages
- Form wizard steps, email templates as keyed strings
- Short structured copy with CI pull/push to JSON repos
- DeepL pre-translate + human review in one tool

## Tolgee — poor fit (use other paths)

- Full markdown pages as single documents
- PDF layout / print materials
- Link Hub page overlays (already in DB JSON)
- Bulk UOTD Excel round-trip (mature workflow)

## REST API for documents (optional later)

Tolgee can import segmented content via REST API, but translator UX is key-per-chunk. Only pursue for **structured, repeatable** content with a custom script in this repo — not ad-hoc documents.

## Asana tracks all types

Translators see one Asana queue; execution tool varies by [project type](translation-project-types.md).
