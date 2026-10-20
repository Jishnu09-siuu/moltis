# Beads - AI-Native Issue Tracking

Welcome to Beads! This repository uses **Beads** for issue tracking - a modern, AI-native tool designed to live directly in your codebase alongside your code.

## What is Beads?

Beads is issue tracking that lives in your repo, making it perfect for AI coding agents and developers who want their issues close to their code. No web UI required - everything works through the CLI and integrates seamlessly with git.

**Learn more:** [github.com/steveyegge/beads](https://github.com/steveyegge/beads)

## Quick Start

### Essential Commands

```bash
# Create new issues
bd create "Add user authentication"

# View all issues
bd list

# View issue details
bd show <issue-id>

# Claim and close an issue
bd update <issue-id> --claim
bd close <issue-id> --reason "Completed"

# Sync when a Dolt remote is configured
bd dolt push
```

### Working with Issues

Issues in Beads are:
- **Git-native**: Stored in Dolt database with version control and branching
- **AI-friendly**: CLI-first design works perfectly with AI coding agents
- **Worktree-aware**: Attach worktrees to the main database with `./scripts/bd-worktree-attach.sh`
- **Explicit sync**: Cross-machine sync requires a configured Dolt remote

### Local storage and upgrades

This checkout uses Beads 1.3.1 with embedded Dolt in `.beads/embeddeddolt/`.
No separate SQL server is required. Database files and runtime locks are ignored
by Git; committing `.beads/metadata.json` does not back up the issue database.

Use `bd context --json`, `bd ready --json`, and `bd hooks list --json` to check
the active database and integration. Full `bd doctor` is not supported in
embedded mode in 1.3.1; its `--check=artifacts`, `--check=conventions`, and
`--check=pollution` checks are available.

No Dolt remote was configured at the 2026-10-19 cutover. To back up the full
database, configure a destination with `bd backup init <path-or-url>` and run
`bd backup sync`. JSONL export is useful for interchange, but does not preserve
Dolt history or configuration.

The legacy server-mode workspace was preserved locally under
`.git/beads-upgrade-20261019/original.beads/`. Migration artifacts and the
checksum-verified historical exporter are in that directory's `migration/`
sibling. The legacy database and its export contained zero issues; missing
historical records are tracked separately in `moltis-cz3`. These recovery
artifacts are local-only and are not included in Git pushes.

For later upgrades, follow the
[official upgrade guide](https://github.com/gastownhall/beads/blob/v1.3.1/docs/getting-started/upgrading.md).
Take backups with the current binary before installing a newer one, and refresh
hooks with `bd hooks install` afterwards.

## Why Beads?

✨ **AI-Native Design**
- Built specifically for AI-assisted development workflows
- CLI-first interface works seamlessly with AI coding agents
- No context switching to web UIs

🚀 **Developer Focused**
- Issues live in your repo, right next to your code
- Works offline, syncs when you push
- Fast, lightweight, and stays out of your way

🔧 **Git Integration**
- Versioned Git hook integration
- Branch-aware issue tracking
- Dolt-native three-way merge resolution

## Get Started with Beads

Try Beads in your own projects:

```bash
# Install Beads
curl -sSL https://raw.githubusercontent.com/steveyegge/beads/main/scripts/install.sh | bash

# Initialize in your repo
bd init

# Create your first issue
bd create "Try out Beads"
```

## Learn More

- **Documentation**: [github.com/steveyegge/beads/docs](https://github.com/steveyegge/beads/tree/main/docs)
- **Quick Start Guide**: Run `bd quickstart`
- **Examples**: [github.com/steveyegge/beads/examples](https://github.com/steveyegge/beads/tree/main/examples)

---

*Beads: Issue tracking that moves at the speed of thought* ⚡
