# Lab Tool Template

GitHub template repo for new TwoSetAI Lab tools. Click **"Use this template"** on the GitHub repo page to spin up a new tool with the security scanning scaffolding already in place.

## What you get out of the box

- **`.github/workflows/semgrep.yml`** — Semgrep SAST scan on every PR + push + weekly Monday. Warn-only on first rollout; flip `continue-on-error: true` → `false` later to make PRs blocking.
- **`.gitleaksignore`** — allowlist file for Gitleaks false positives. Starts empty with instructions.
- **`.gitignore`** — standard TwoSetAI patterns: node_modules, .env*, OAuth JSONs, service accounts, Vercel artifacts, PROJECT.md / COSTS.md / FEATURE_*.md gitignored by house rule.

## After creating from this template

1. Enable Dependabot alerts + security updates: Settings → Code security → "Enable all"
2. If the repo is public: enable Secret scanning + push protection on the same page
3. On the user-level [security defaults page](https://github.com/settings/security_analysis), confirm "Automatically enable for new repositories" is checked on everything (should auto-apply)
4. Open the first PR → verify Semgrep workflow runs and reports findings in the Actions log

## Local checks before pushing

Run on your laptop before pushing:

```bash
# Install once
brew install gitleaks

# Scan git history for leaked secrets
gitleaks detect --no-banner --redact
```

Clean = `no leaks found`. Anything flagged = rotate the key AND rewrite history (`git filter-repo`) before pushing.

## Why this template exists

Set up 2026-10-19 after a security pass across all Lab repos found 3 real leaks + 2 false positives. New Lab tools inherit the scanning scaffolding so you don't repeat the setup per repo.
