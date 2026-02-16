# Changelog

## [Unreleased]

### Changed

- Make setup and troubleshooting guidance easier to follow across README and
  security documentation
  ([`261c18d`](https://github.com/octivi/cloudflare-cache-purge/commit/261c18d),
  [`1b369e6`](https://github.com/octivi/cloudflare-cache-purge/commit/1b369e6),
  [`715e6d3`](https://github.com/octivi/cloudflare-cache-purge/commit/715e6d3))

### Added

- Add practical examples for reporting security issues
  ([`715e6d3`](https://github.com/octivi/cloudflare-cache-purge/commit/715e6d3))

### Removed

- Remove outdated planning notes that are no longer relevant to users
  ([`e0499c5`](https://github.com/octivi/cloudflare-cache-purge/commit/e0499c5))

### Fixed

- Fix broken Marketplace link after the action rename
  ([`3e35ad2`](https://github.com/octivi/cloudflare-cache-purge/commit/3e35ad2))

## [1.1.0] - 2026-02-09

### Changed

- **Breaking:** Rename the action to resolve a GitHub Marketplace naming
  conflict; update workflows that reference the old action name
  ([`cba4ec2`](https://github.com/octivi/cloudflare-cache-purge/commit/cba4ec2))
- Improve onboarding docs with clearer usage guidance and direct links to source
  code and Marketplace
  ([`a6b004c`](https://github.com/octivi/cloudflare-cache-purge/commit/a6b004c),
  [`c45fc02`](https://github.com/octivi/cloudflare-cache-purge/commit/c45fc02),
  [`39f7bbf`](https://github.com/octivi/cloudflare-cache-purge/commit/39f7bbf))

### Added

- Add support for multiline YAML inputs for easier configuration in complex
  workflows
  ([`3556c31`](https://github.com/octivi/cloudflare-cache-purge/commit/3556c31))
- Add `dry-run` mode to preview actions safely and `verbose` mode for easier
  debugging, with GitHub-native execution reporting
  ([`c657f74`](https://github.com/octivi/cloudflare-cache-purge/commit/c657f74))

### Removed

- No user-facing removals.

### Fixed

- No user-facing fixes.

## [1.0.0] - 2026-02-08

### Changed

- Align token variable naming with Cloudflare terminology for clearer setup
  ([`5356aac`](https://github.com/octivi/cloudflare-cache-purge/commit/5356aac))

### Added

- Initial release of the GitHub Action for purging Cloudflare cache directly
  from workflows
  ([`1a4eee8`](https://github.com/octivi/cloudflare-cache-purge/commit/1a4eee8))

### Removed

- No user-facing removals.

### Fixed

- Fix shell snippet formatting in docs examples
  ([`9c8ea55`](https://github.com/octivi/cloudflare-cache-purge/commit/9c8ea55))

<!-- Reference links (recommended) -->

[Unreleased]: https://github.com/octivi/cloudflare-cache-purge/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/octivi/cloudflare-cache-purge/releases/tag/v1.1.0
[1.0.0]: https://github.com/octivi/cloudflare-cache-purge/releases/tag/v1.0.0
