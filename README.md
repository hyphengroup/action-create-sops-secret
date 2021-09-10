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
    json_secrets_str: ${{ toJSON(secrets) }}
    prefix: STAGING_ENV_
    file_path: my-service/env-secrets.yaml
- uses: hyphengroup/action-create-sops-secret@v0.1.0
  with:
    json_secrets_str: ${{ toJSON(secrets) }}
    prefix: STAGING_CERT_
    file_path: my-service/certs.yaml
```

Creates:
- `my-service` directory if it does not exist
- `my-service/env-secrets.yaml` with 3 keys: [ `API_KEY`, `DB_HOST`, `DB_NAME` ]
- `my-service/certs.yaml` with 2 keys: [ `PRIVATE_KEY`, `PUBLIC_KEY` ]
