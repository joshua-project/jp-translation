# jp-translation

Coordination repo for Joshua Project multilingual work. **Asana** tracks translation projects; **Tolgee** (`https://tolgee.joshuaproject.net`) executes **App strings** work. Infrastructure lives in [jp-infrastructure](https://github.com/joshua-project/jp-infrastructure).

## Architecture (Strategy D)

| Layer | Tool | Purpose |
|-------|------|---------|
| Program management | **Asana** | Intake, assignees, deadlines, one queue for all translation types |
| App UI strings | **Tolgee** | Key management, DeepL, review states, CI pull/push (Phase 2+) |
| Link Hub pages | jp-link-hub admin | Overlay translations (`?lang=`) |
| Unreached of the Day | Excel ↔ JSON scripts | Bulk string workflow |
| Documents / handouts | DeepL Document / manual | Separate Asana project type |

Production apps **do not** call Tolgee at runtime. Tolgee is the management layer; committed translation files ship via CI.

## Repo map

| Repo | Role |
|------|------|
| **jp-infrastructure** | Tolgee Azure stacks, Entra OAuth, [runbook](../jp-infrastructure/docs/runbooks/tolgee.md) |
| **jp-translation** (this repo) | Runbooks, Asana templates, project-type taxonomy |
| **jp-adopt-forms** | First app integration target ([Tolgee design](https://github.com/joshua-project/jp-adopt-forms/blob/main/docs/plans/2026-03-25-tolgee-integration-design.md)) |

## Docs

- [1Password checklist](docs/1password-checklist.md) — create before first Terraform apply
- [Bootstrap Tolgee](docs/bootstrap.md) — post-deploy admin setup
- [Translation project types](docs/translation-project-types.md) — Asana routing rules
- [Asana templates](docs/pm-templates-asana.md) — task templates per type
- [Content-type matrix](docs/content-type-matrix.md) — Tolgee vs other paths
- [Integration roadmap](docs/integration-roadmap.md) — phased app wiring
- [n8n integrations](docs/n8n-integrations.md) — optional Asana ↔ Tolgee automation
- [Deploy and verify](docs/deploy-verify.md) — apply order and smoke tests

## Quick start (operators)

1. Complete [1Password checklist](docs/1password-checklist.md)
2. Merge and apply jp-infrastructure Tolgee stacks (see infra runbook)
3. Bootstrap Postgres role + Tolgee admin ([bootstrap.md](docs/bootstrap.md))
4. Create Asana translation portfolio ([pm-templates-asana.md](docs/pm-templates-asana.md))
