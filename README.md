# Cloudflare Cache Purge GitHub Action

[![Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-blue?logo=github)](https://github.com/marketplace/actions/cloudflare-cache-purge)
[![GitHub release](https://img.shields.io/github/v/release/octivi/cloudflare-cache-purge?sort=semver)](https://github.com/octivi/cloudflare-cache-purge/releases)
[![license](https://img.shields.io/github/license/octivi/cloudflare-cache-purge)](https://choosealicense.com/licenses/mit/)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org/)
[![semver](https://img.shields.io/badge/SemVer-2.0.0-blue)](https://semver.org/spec/v2.0.0.html)

This GitHub Action purges Cloudflare cache via Cloudflare API.
It supports:

- full purge (`purge_everything`)
- targeted purge by `files`, `tags`, `hosts`, `prefixes`

## Inputs

| Input | Description | Required | Default |
| --- | --- | --- | --- |
| `CLOUDFLARE_API_TOKEN` | Cloudflare API token with cache purge permissions for the zone. | Yes | - |
| `CLOUDFLARE_ZONE_ID` | Cloudflare Zone ID. | Yes | - |
| `files` | URLs to purge (space- or comma-separated). | No | `""` |
| `tags` | Cache tags to purge (space- or comma-separated). | No | `""` |
| `hosts` | Hostnames to purge (space- or comma-separated). | No | `""` |
| `prefixes` | URL prefixes to purge (space- or comma-separated). | No | `""` |

If `files`, `tags`, `hosts` and `prefixes` are all empty, the action sends:
`{"purge_everything": true}`.

## Token permissions

Required permissions for a [User API Token](https://dash.cloudflare.com/profile/api-tokens) or
[Account API tokens](https://dash.cloudflare.com/?to=/:account/api-tokens) if you prefer credentials that are not
associated with users:

- `Cache Purge:Purge`

Documentation:

- https://developers.cloudflare.com/fundamentals/api/get-started/

## How to get Zone ID

To copy your `Zone ID` in the Cloudflare dashboard:

1. Go to **Account home** and locate your account.
2. Open your account **Overview** page and find the **API** section near the bottom.
3. Under **Zone ID**, click **Click to copy**.

Reference:

- https://developers.cloudflare.com/fundamentals/account/find-account-and-zone-ids/#copy-your-zone-id

## Example workflow

Purge everything:

```yml
name: Purge Cloudflare cache

on:
  workflow_dispatch:

jobs:
  purge-cache:
    runs-on: ubuntu-latest
    steps:
      - uses: octivi/cloudflare-cache-purge@v1
        with:
          CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          CLOUDFLARE_ZONE_ID: ${{ vars.CLOUDFLARE_ZONE_ID }}
```

Targeted purge:

```yml
- uses: octivi/cloudflare-cache-purge@v1
  with:
    CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
    CLOUDFLARE_ZONE_ID: ${{ vars.CLOUDFLARE_ZONE_ID }}
    files: "https://example.com/ https://example.com/app.js"
    tags: "release-2026-02"
    hosts: "example.com"
    prefixes: "example.com/static"
```

## CLI usage

Run locally from this repository:

```bash
CLOUDFLARE_API_TOKEN="..." \
CLOUDFLARE_ZONE_ID="..." \
./cloudflare-cache-purge \
  --files https://example.com/ https://example.com/app.js \
  --tags release-2026-02 \
  --hosts example.com \
  --prefixes example.com/static
```

You can also set selectors via env vars: `FILES`, `TAGS`, `HOSTS`, `PREFIXES`.
Values can be space-separated, comma-separated, or mixed.

## Tests

Run tests:

```bash
./tests/run
```

## Notes and limits

Before using this action, read Cloudflare docs, especially limits and purge behavior:

- Purge cache overview: https://developers.cloudflare.com/cache/how-to/purge-cache/
- Purge cache API: https://developers.cloudflare.com/api/resources/cache/methods/purge/

## Requirements

- `bash`
- `curl`
- `jq`

## Getting help

If you run into issues, open a GitHub issue in this repository and include a minimal reproduction
(workflow snippet + inputs).

## Maintainers and contributors

Maintained by the [Octivi DevOps team](https://octivi.com/devops). Contributions are welcome via
pull requests.

## Legal notice

This project is not affiliated with, endorsed by, or sponsored by Cloudflare.
Cloudflare and related marks are trademarks or registered trademarks of Cloudflare, Inc.
