# Add Changeset to Dependabot PRs

Automatically add a changeset to Dependabot pull requests. 

This GitHub Action helps streamline your dependency update workflow by automatically creating changesets for PRs created by Dependabot.

## Features

- 🤖 Automatically creates changesets for Dependabot PRs
- 📝 Uses the commit message from Dependabot as the changeset summary
- ⚙️ Configurable release type (patch, minor, major)
- 🔄 Skips changeset creation if one already exists
- 🚀 Automatically commits the changeset to the PR

## Minimum Usage

Add this action to your workflow file (e.g., `.github/workflows/dependabot-changeset.yml`):

```yaml
name: Add Changeset to Dependabot PRs

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  add-changeset:
    # Only run on Dependabot PRs
    if: github.actor == 'dependabot[bot]'
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Add changeset
        uses: IzumiSy/simple-dependabot-changeset@main
        with:
          pkgName: 'your-package-name'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `pkgName` | The package name to create a changeset for | Yes | - |
| `releaseType` | The type of release to create (`patch`, `minor`, `major`) | No | `patch` |
| `prefix` | The prefix to use for the changeset commit message | No | `[add changeset]` |

## How It Works

1. The action checks out your repository and sets up Node.js to install `@changesets/write` package
2. It retrieves the commits from the pull request
3. If a changeset commit already exists (identified by the prefix), it skips creation
4. Otherwise, it creates a new changeset using:
   - The first line of the Dependabot commit message as the summary
   - The specified package name
   - The specified release type
5. The changeset is automatically committed to the PR

## Requirements

- Your project must be using [Changesets](https://github.com/changesets/changesets)
- The workflow needs `contents: write` permission to commit changesets

## Usecase

- [IzumiSy/kyrage](https://github.com/IzumiSy/kyrage/)
- [IzumiSy/mcp-duckdb-memory-server](https://github.com/IzumiSy/mcp-duckdb-memory-server)
- [IzumiSy/mcp-universal-db-client](https://github.com/IzumiSy/mcp-universal-db-client)

## License

See [LICENSE](LICENSE) file for details.
