# Deploy and verify

Steps for operators after merging jp-infrastructure Tolgee PR. Local validation already run: `terraform validate` on `stacks/shared/tolgee/app`.

## Prerequisites

- [1Password checklist](1password-checklist.md) complete
- PR merged to `jp-infrastructure` `main`
- GitHub Actions **Terraform** workflow can access JP Tolgee vault

## Apply (via CI or local)

Order:

1. **entra** matrix: `stacks/azure/entra/tolgee/`
2. **shared** matrix: `stacks/shared/tolgee/database/`
3. Postgres role bootstrap ([infra runbook](https://github.com/joshua-project/jp-infrastructure/blob/main/docs/runbooks/tolgee.md#pre-apply-postgresql-role-bootstrap))
4. **shared**: `stacks/shared/tolgee/app/`
5. **shared**: `stacks/shared/tolgee/dns/`

Copy storage connection string to 1Password after app stack creates `jptolgeeshared`.

## Verification

| # | Command / action | Expected |
|---|------------------|----------|
| 1 | `curl -sf https://tolgee.joshuaproject.net/actuator/health` | HTTP 200 |
| 2 | Browse to URL | Tolgee login page loads |
| 3 | Entra login | Staff `@joshuaproject.net` succeeds |
| 4 | Native invite test user | Volunteer login succeeds |
| 5 | Create test key + DeepL | Suggestion appears |
| 6 | Azure Log stream | No DB or `/data` mount errors |

Then complete [bootstrap.md](bootstrap.md) and Asana portfolio setup.

## Rollback

1. Remove DNS stack (or disable custom domain)
2. Destroy app stack
3. Database can remain for data retention; drop `tolgee` DB only if fully decommissioning

Entra app can stay registered for future retry.
