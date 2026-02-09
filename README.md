# Cloudflare Cache Purge GitHub Action

[![Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-blue?logo=github)](https://github.com/marketplace/actions/purge-cloudflare-zone-cache)
[![GitHub release](https://img.shields.io/github/v/release/octivi/cloudflare-cache-purge?sort=semver)](https://github.com/octivi/cloudflare-cache-purge/releases)
[![license](https://img.shields.io/github/license/octivi/cloudflare-cache-purge)](https://choosealicense.com/licenses/mit/)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org/)
[![semver](https://img.shields.io/badge/SemVer-2.0.0-blue)](https://semver.org/spec/v2.0.0.html)

This GitHub Action purges Cloudflare cache via Cloudflare API.
It supports:

- full purge (`purge_everything`)
- targeted purge by `files`, `tags`, `hosts`, `prefixes`

## Why choose this action

- Pure Bash implementation with minimal dependencies (`bash`, plus `curl` and `jq` for the API call)
- Fast startup: no `npm`/`pip` install step during workflow execution
- Lower supply-chain and maintenance overhead: no runtime pinning, lockfiles, or dependency CVEs
- Easier security audit: all logic lives in a small, readable script
- Covered by automated tests (`./tests/run`) and CI
- Works on `ubuntu-slim`, which can help reduce runner costs:
  <https://docs.github.com/en/actions/reference/runners/github-hosted-runners>
- Can be used both as a GitHub Action and as a standalone script
- Released under the MIT License: a short and simple permissive license
- Documented security policy: [SECURITY.md](./SECURITY.md)

## Inputs

| Input | Description | Required | Default |
| --- | --- | --- | --- |
| `CLOUDFLARE_API_TOKEN` | Cloudflare API token with cache purge permissions for the zone | Yes | - |
| `CLOUDFLARE_ZONE_ID` | Cloudflare Zone ID | Yes | - |
| `files` | URLs to purge (space-, comma- or newline-separated) | No | `""` |
| `tags` | Cache tags to purge (space-, comma- or newline-separated) | No | `""` |
| `hosts` | Hostnames to purge (space-, comma- or newline-separated) | No | `""` |
| `prefixes` | URL prefixes to purge (space-, comma- or newline-separated) | No | `""` |
| `dry_run` | If `true`, print planned request and skip API call | No | `"false"` |
| `verbose` | If `true`, print detailed logs | No | `"false"` |

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

1. Go to **Account home** and locate your account
2. Open your account **Overview** page and find the **API** section near the bottom
3. Under **Zone ID**, click **Click to copy**

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

Optional execution modes:

```bash
./cloudflare-cache-purge --dry-run --verbose
```

You can also set values via env vars: `FILES`, `TAGS`, `HOSTS`, `PREFIXES`, `DRY_RUN`, `VERBOSE`.
List values can be space-separated, comma-separated, newline-separated, or mixed.
`DRY_RUN` and `VERBOSE` are presence flags: any non-empty value enables the mode, leaving the variable unset disables it.

When run inside GitHub Actions, logs are grouped, warnings/errors are emitted as workflow annotations, and a short result is written to `GITHUB_STEP_SUMMARY`.

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

## Other Octivi GitHub Actions

If you are interested in other GitHub Actions we build, see:

- [`octivi/update-copyright-year`](https://github.com/octivi/update-copyright-year) - Updates the copyright year in file headers across your repository
- [`octivi/update-securitytxt-expires`](https://github.com/octivi/update-securitytxt-expires) - Updates the `Expires` field in `security.txt` files to a future date so published security contact metadata stays current

## Maintainers and contributors

Maintained by the [Octivi DevOps team](https://octivi.com/devops). Contributions are welcome via
pull requests.

## Legal notice

This project is not affiliated with, endorsed by, or sponsored by Cloudflare.
Cloudflare and related marks are trademarks or registered trademarks of Cloudflare, Inc.
