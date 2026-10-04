# release-drafter-example

Test and example repository demonstrating the [Release Drafter](https://github.com/juftin/release-drafter) reusable workflow (`workflow_call`) and zero-config Conventional Commits preset.

## How it works

This repository invokes Release Drafter via its reusable workflow:

```yaml
name: Release Drafter

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, reopened, synchronize]

permissions:
  contents: write
  pull-requests: write

jobs:
  draft-release:
    uses: juftin/release-drafter/.github/workflows/workflow.yml@main
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

With zero local configuration (no `.github/release-drafter.yml`), Release Drafter automatically resolves `preset:conventional-commits` to:
- Categorize changes into Conventional Commits categories (Features, Bug Fixes, Documentation, etc.)
- Calculate SemVer increments from commit messages (`feat:` -> minor bump, `fix:` -> patch bump, breaking change -> major bump)
- Draft release notes from direct commits and pull requests
