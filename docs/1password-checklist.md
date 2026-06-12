# 1Password checklist — JP Tolgee

Complete **before** the first Terraform apply on `stacks/shared/tolgee/*`. Account: **joshuaproject** (`OP_ACCOUNT=joshuaproject` in CI).

## 1. Create vault

Create vault: **`JP Tolgee`**

Grant access to infrastructure operators and the CI service account (step 2).

## 2. CI service account

In **`CI Automation`** vault, create:

| Item | Field | Notes |
|------|-------|-------|
| `jp-tolgee-sa` | `credential` | 1Password service account token with read access to **JP Tolgee** vault only |

Reference in GitHub Actions: `op://CI Automation/jp-tolgee-sa/credential`

Mirror the existing `jp-n8n-sa` pattern.

## 3. Production secrets

In **`JP Tolgee`** vault, create item **`Tolgee - Production`**:

| Field | Purpose | How to generate |
|-------|---------|-----------------|
| `database-password` | Postgres role `tolgee_app_prod` | `openssl rand -base64 32` — use same value in [SQL bootstrap](https://github.com/joshua-project/jp-infrastructure/blob/main/docs/runbooks/tolgee.md#pre-apply-postgresql-role-bootstrap) |
| `jwt-secret` | Tolgee JWT signing | `openssl rand -base64 48` |
| `storage-connection-string` | Ops reference for `jptolgeeshared` account | Populate **after** first app stack apply from Azure Portal → Storage account → Access keys → Connection string |
| `deepl-auth-key` | Tolgee machine translation (DeepL) | Copy from `op://JP Link Hub/Link Hub - Production/DEEPL_API_KEY` (same key for now; rotate independently later if needed) |

## 4. DeepL

Same API key as Link Hub, stored on the Tolgee item so CI reads only **JP Tolgee**:

`op://JP Tolgee/Tolgee - Production/deepl-auth-key`

Loaded with other Tolgee secrets via `jp-tolgee-sa`. When Link Hub rotates its key, update both entries (or split to a dedicated Tolgee key later).

## 5. Terraform variable mapping

These references are wired in `.github/workflows/terraform.yml` (shared matrix):

| TF variable | 1Password reference |
|-------------|---------------------|
| `TF_VAR_tolgee_db_password` | `op://JP Tolgee/Tolgee - Production/database-password` |
| `TF_VAR_tolgee_jwt_secret` | `op://JP Tolgee/Tolgee - Production/jwt-secret` |
| `TF_VAR_tolgee_storage_connection_string` | `op://JP Tolgee/Tolgee - Production/storage-connection-string` |
| `TF_VAR_tolgee_deepl_auth_key` | `op://JP Tolgee/Tolgee - Production/deepl-auth-key` |

OAuth client ID/secret come from Terraform remote state (`stacks/azure/entra/tolgee/`), not 1Password.

## 6. Post-bootstrap (Tolgee UI)

After admin setup, store per-project API keys in **JP Tolgee** as separate items (e.g. `Tolgee API - jp-adopt-forms`) when Phase 2 CI integration begins. Do not commit PATs to git.

## 7. Entra

Ensure Entra admin consent for app registration **JP Tolgee** after `stacks/azure/entra/tolgee/` applies. Redirect URI must include:

`https://tolgee.joshuaproject.net/login/auth_callback/oauth2`
