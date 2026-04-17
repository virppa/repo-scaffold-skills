# repo-scaffold-skills

Claude Code skill files for the [repo-scaffold-desktop](https://github.com/virppa/repo-scaffold-desktop) hybrid workflow.

Repos scaffolded with the `full_agentic` preset reference this repo in their `.claude/settings.json`:

```json
{
  "skills_source": "github:virppa/repo-scaffold-skills",
  "skills_version": "v1.0.0"
}
```

Skills are fetched from the pinned version at scaffold time and written to `.claude/commands/`. They are free to drift locally — this repo is the upstream, not a lock file.

## Skills

| Skill | Purpose |
|---|---|
| `/groom-ticket` | PO review: scope, acceptance criteria, splitting |
| `/start-ticket` | Architect plan: files, tests, branch, Linear status |
| `/implement-ticket` | Local worker entrypoint: executes within manifest bounds |
| `/finalize-ticket` | Coverage check, docs, PR creation, Linear → In Review |
| `/close-epic` | Security + coverage review, epic → main PR |
| `/security-check` | Bandit scan + OWASP diff review |
| `/prioritize` | Pull and rank open Linear issues |
| `/update-skills` | Fetch latest skills from this repo, bump `skills_version` |
| `/contribute-skill` | Open a PR here with a locally modified skill |

## Updating skills in a scaffolded repo

```
/update-skills
```

Fetches `.claude/commands/` at the latest release tag and updates `skills_version` in your `settings.json`. Run this when you want improvements from a newer release.

## Contributing a local change back

```
/contribute-skill <name>
```

Example: `/contribute-skill groom-ticket`

Diffs your local version against the upstream base, opens a PR against this repo. The change is yours to curate — only what you explicitly contribute flows back.

## Versioning

Releases follow `v<major>.<minor>.<patch>`. Breaking changes (renamed or removed skills) increment the minor version. Patch releases are additive or fix-only.

Scaffolded repos stay pinned at their `skills_version` until `/update-skills` is run — they never auto-update.

## Forking

To host your own skills source, fork this repo and update `skills_source` in your scaffold template:

```json
"skills_source": "github:<your-org>/your-skills-repo"
```

The `fetch_skills()` generator function resolves any `github:<owner>/<repo>` source.

## License

MIT
