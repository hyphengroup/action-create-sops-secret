# `create-sops-secret` GitHub Action

Creates encrypted isindir/sops-secrets-operator yml manifests from GitHub secrets

# Usage

pre-req:
- `mozilla/sops` is pre-installed in env
- `jq` is installed in env

For the following GitHub secrets:

```
STAGING_ENV_API_KEY=foo
STAGING_ENV_DB_HOST=bar
STAGING_ENV_DB_NAME=baz
STAGING_CERT_PRIVATE_KEY=...
STAGING_CERT_PUBLIC_KEY=...
```

This Workflow

```yaml
- uses: mdgreenwald/mozilla-sops-action@v1.1.0
- uses: hyphengroup/action-create-sops-secret@v0.1.0
  with: 
    prefix: STAGING_ENV_
    name: env-secrets
- uses: hyphengroup/action-create-sops-secret@v0.1.0
  with: 
    prefix: STAGING_CERT_
    name: certs
```

Creates:
- `env-secret.yaml` with 3 keys: [ `API_KEY`, `DB_HOST`, `DB_NAME` ]
- `certs.yaml` with 2 keys: [ `PRIVATE_KEY`, `PUBLIC_KEY` ]
