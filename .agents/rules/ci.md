---
trigger: glob
globs: ".github/workflows/**"
description: GitHub Actions CI workflow architecture, action versioning policies, and caching strategies.
---

# CI & GitHub Actions Guidelines

Guidelines for maintaining GitHub Actions workflows in this repository.

## 1. Action Versioning Policy

- **Major Version Floating Tags**: Always reference the latest major version tag (e.g. `actions/checkout@v7`, `voidzero-dev/setup-vp@v1`, `actions/cache@v6`, `actions/upload-artifact@v7`).
- **Never Pin Exact Versions**: Do not lock actions to patch/minor versions (e.g. avoid `voidzero-dev/setup-vp@v1.21.2`) to allow non-breaking security patches and runtime optimizations to roll out seamlessly.

## 2. Toolchain & Runner Configuration

- **Vite+ Action**: Use `voidzero-dev/setup-vp@v1` with `node-version-file: package.json` and `cache: true` for automatic dependency cache and Node.js LTS resolution.
- **Vite Task Caching**: Cache `node_modules/.vite/task-cache` with `actions/cache@v6` across workflow runs to leverage Vite task replay.
- **Playwright Binary Caching**: Cache Playwright browser binaries (`${{ env.PLAYWRIGHT_BROWSERS_PATH }}`) keyed to the Playwright CLI version.
- **Artifact Retention**: Configure `actions/upload-artifact@v7` on failure with explicit `retention-days: 7` and `if-no-files-found: ignore`.

## 3. Shift-Left Validation & Offline Guardrail

- **Local Linting**: Whenever `.github/workflows/` files are modified, run `vpr agent:lint:ci` (`actionlint`) locally.
- **Zero Errors / Warnings**: Workflows must pass `actionlint` with 0 errors and 0 warnings before staging.
- **Offline Guardrail**: `actionlint` is strictly a local pre-commit check; NEVER embed `actionlint` into remote GitHub Actions YAML workflow files.
