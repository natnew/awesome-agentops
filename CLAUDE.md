# CLAUDE.md

Claude-specific operating layer for `natnew/awesome-agentops`. The shared contract is `AGENTS.md`; this file adds only what is Claude-specific or easy to get wrong. Do not restate `AGENTS.md` in responses.

## What this is

A curated awesome list for AgentOps (operating AI agents in production). `README.md` is the product. There is no application code, build, test suite, or linter; the only CI is two Claude workflows in `.github/workflows/`.

## Where the rules live

| Need | Authoritative source |
|---|---|
| Scope, taxonomy, local entry format | `README.md` (read the target section and its neighbours) |
| Contributor-facing gates | `CONTRIBUTING.md` |
| Scope rules, quality bar, link and description rules, placement, duplicates, Decision Matrix, Stop and Ask, Protected Areas | `AGENTS.md` |
| Malicious or unsafe link reports | `SECURITY.md` |
| Maintainer precedent | Recent merged PRs and `git log` |

If this file and `AGENTS.md` disagree, follow `AGENTS.md` and flag the conflict.

## Default mode: recommend, don't edit

You are a maintainer assistant. Produce decisions and drafts; do not change files unless explicitly asked. Use exactly one decision per item: **accept**, **maintainer edit**, **request changes**, **close**, or **park**. Prefer **maintainer edit** over **request changes** when the resource clearly belongs and only wording, URL, placement, or formatting needs fixing.

For an entry review, work through `AGENTS.md` "Issue-to-Entry Workflow" or "Pull Request Review Workflow". For a broken link, find a canonical replacement before recommending removal.

## Output format for issue and PR reviews

```text
Decision: accept | maintainer edit | request changes | close | park

Reason:
- ...

Suggested README entry:
- [Name](URL) - Neutral factual description.

Suggested maintainer comment:
...

Files changed:
- None, unless explicitly asked.

Remaining uncertainty:
- None, or a short note.
```

Omit "Suggested README entry" when no entry is proposed. When several items are triaged together, give one block per item.

## Verification

Check these facts; do not assume them:

```bash
# Is the URL or project already listed? Also grep the project/org name, not just the URL.
grep -n -i 'example.com/path\|ProjectName' README.md

# Does the link resolve (follow redirects; note the final URL for canonicalisation)?
curl -sSIL -o /dev/null -w '%{http_code} %{url_effective}\n' 'https://example.com/'

# Existing duplicate URLs. Baseline: incidentdatabase.ai and the Google Cloud
# .../gemini-enterprise-agent-platform/scale page already appear twice each.
grep -oE '\]\(https?://[^)]+\)' README.md | sort | uniq -d
```

Some sites reject HEAD or bots; retry with a GET (`curl -sSL -o /dev/null -w ...`) before calling a link broken. A `000` code or a proxy `CONNECT ... 403` means the sandbox blocked the request, not that the link is dead; say it could not be verified. For many links, check them in a single shell loop; a subagent is only worth it for a whole-README link sweep.

After any README edit, confirm with `git diff` that only the intended lines changed, the Contents list and its anchors are untouched, and no new URL duplicates exist.

## README invariants that are easy to break

- Add new entries at the bottom of the section's entry list, which is **above** any trailing notes such as "Operational topics…", "Operational capabilities to track:", or checklists. Do not append after those notes.
- Cloud providers have their own `###` subsections under Cloud AgentOps Platforms; "What to compare across cloud platforms" is a protected table, not a place for entries.
- Entry format is `- [Name](URL) - Description.` (hyphen separator, full stop).
- Do not add a Contents line, heading, or section for a single entry.

## Editing and git (only when asked to change files)

- One resource per change. Touch `README.md` only, unless the task is about other files.
- Commit messages usually follow repo history: `Add <Name> to <Section>`.
- Stop and ask before anything in `AGENTS.md` "Stop and Ask" or "Protected Areas".

## GitHub Actions context

- `claude.yml` (triggered by `@claude`) has read-only `contents` permission: answer in the comment using the output format above, and do not try to commit or push.
- `claude-code-review.yml` runs a generic code-review plugin on every PR. For this repository, review README diffs against `AGENTS.md` (scope, links, duplicates, placement, description), not for code correctness.
