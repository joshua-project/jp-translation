# Integration roadmap

## Phase 1 — Infrastructure (current)

- [x] Tolgee Terraform stacks in jp-infrastructure
- [x] Entra OAuth app **JP Tolgee**
- [x] jp-translation coordination docs + Asana templates
- [ ] 1Password vault populated ([checklist](1password-checklist.md))
- [ ] Terraform apply + [bootstrap](bootstrap.md)
- [ ] Asana translation portfolio live

## Phase 1.5 — Optional automation

- [ ] n8n flows ([n8n-integrations.md](n8n-integrations.md))
- [ ] Weekly translation sync digest to coordinators

## Phase 2 — jp-adopt-forms

Per [Tolgee integration design](https://github.com/joshua-project/jp-adopt-forms/blob/main/docs/plans/2026-03-25-tolgee-integration-design.md):

1. Namespace-split `messages/{namespace}/{locale}.json` (standalone PR)
2. Fix `request.ts` to load locale-specific messages
3. `.tolgeerc` + `@tolgee/cli` push/pull
4. Tolgee SDK on staging only (in-context editing)
5. CI: `tolgee pull` on deploy, `tolgee push` on dev merge
6. Enable locale switcher when es/pt reviewed

## Phase 3 — Additional apps

| App | Approach |
|-----|----------|
| jp-adoption-platform | Repeat adopt-forms pattern |
| jp-content | next-intl + Tolgee when CMS ships |
| unreached-of-day | Optional Tolgee API adapter; Excel remains valid |

## Phase N — joshuaproject Laravel site

Spike required: PHP lang files vs JSON export vs jp-content CMS. Do not block Tolgee infra on this decision.

## Explicit non-goals

- Moving Link Hub overlays into Tolgee
- Replacing UOTD Excel workflow without volunteer buy-in
- Runtime Tolgee dependency in production apps
