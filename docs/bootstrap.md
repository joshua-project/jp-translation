# Tolgee bootstrap (post-Terraform)

Run after `stacks/shared/tolgee/{database,app,dns}` and `stacks/azure/entra/tolgee/` are applied. See [jp-infrastructure runbook](https://github.com/joshua-project/jp-infrastructure/blob/main/docs/runbooks/tolgee.md).

## 1. Verify health

```bash
curl -sf https://tolgee.joshuaproject.net/actuator/health
```

Expect HTTP 200 with `"status":"UP"`.

## 2. Initial admin login

On first boot Tolgee writes a generated password to `/data/initial.pwd` inside the container.

To read it:

1. Azure Portal → `jp-tolgee-shared` → **SSH** or **Advanced Tools (Kudu)** → Bash
2. `cat /data/initial.pwd`
3. Sign in at <https://tolgee.joshuaproject.net> with username `admin` and that password
4. Change the password immediately; store the new value in **JP Tolgee** 1Password (admin item)

## 3. Harden authentication

In Tolgee **Server administration** → **Security**:

- Disable **Registrations allowed** (should already be off via env)
- Keep **Native authentication** enabled for volunteer invite accounts
- Confirm **OAuth2** shows Microsoft / Entra (env-driven)

## 4. Machine translation

**Server administration** → **Machine translation**:

- Enable **DeepL** (key injected via Terraform)
- Enable **Auto translation** for new keys where appropriate

## 5. Translation quality gate

For each project (and in CLI later):

- Only export/pull states **Translated** and **Reviewed** to production repos
- Machine-translated strings stay in Tolgee until a human promotes them

Document this in project settings and train reviewers.

## 6. Entra staff SSO

1. Open an incognito window → **Login with OAuth2** (or Microsoft button)
2. Sign in with `@joshuaproject.net` staff account
3. If consent fails, Entra admin must approve app **JP Tolgee**

Redirect URI (must match Entra registration):

`https://tolgee.joshuaproject.net/login/auth_callback/oauth2`

## 7. Create placeholder Tolgee projects

Create empty projects (no push from apps yet):

| Project name | Languages | Notes |
|--------------|-----------|-------|
| `jp-adopt-forms` | en, es, pt | Phase 2 integration |
| `jp-adoption-platform` | en, es, pt | Phase 4 in adopt-forms design |
| `joshuaproject-website-future` | TBD | Spike before use |

Assign staff **Manager**, volunteers **Translator** / **Reviewer** roles per project.

## 8. API keys (Phase 2 prep)

For each project, generate a **Project API key** with translate + view scopes. Store in 1Password (`Tolgee API - <project>`). Do not commit to git.

## 9. Asana portfolio

Create the **Translation** portfolio in Asana using [pm-templates-asana.md](pm-templates-asana.md). Link each open Tolgee project as an **App strings (Tolgee)** task with the Tolgee project URL in the description.

## 10. Smoke test

1. Add a test key `smoke.test` = `Hello` in `jp-adopt-forms` project (English)
2. Trigger DeepL for Spanish
3. Review and mark **Translated**
4. Confirm export would include the key (UI export or API)

Delete smoke keys when done.
