<div align="center">

<img src="https://raw.githubusercontent.com/open-coder-ai/chock/main/docs/assets/readme/cover-chock-threat-intel.png" alt="chock-threat-intel: a weekly, human-reviewed ledger of agentic-AI threats, each scored against what the Chock catalog enforces." width="760">

# Teach your AI agent what not to do.

**Open-source guardrails for AI coding agents: rules the agent reads, checks that run as it writes, and gates at commit and in CI. This repo is the weekly threat ledger those policies answer to.**

[the threat ledger →](reference/agentic-threat-ledger.md) ·
[weekly digests →](digests/) ·
[the framework →](https://github.com/open-coder-ai/chock) ·
[the policy catalog →](https://github.com/open-coder-ai/chock-catalog)

</div>

**What this is.** chock-threat-intel is a human-reviewed, weekly compilation of published agentic-AI threat frameworks (OWASP, MITRE ATLAS, NIST, CISA, the Cloud Security Alliance and others), each entry scored against what the [Chock catalog](https://github.com/open-coder-ai/chock-catalog) does about it: enforced for a slice, advisory, `policy wanted`, or out of scope. Chock is open-source application security for code written by AI coding agents, with deterministic local checks, no model and no upload.

> **Unofficial compilation, verify at the source.** We are not an authoritative source for the frameworks cited here. Full disclaimer: [`docs/README.md`](docs/README.md).

## Application security for the code your agents write

Chock's policies exist because agents write code, run commands and install tools, and published threats describe how that goes wrong. This ledger is the list the catalog is checked against, so a gap is visible rather than implied. It does not stop any attack itself: the policies live in the [catalog](https://github.com/open-coder-ai/chock-catalog), and the ledger says which threats they reach and which they do not.

## This week: [2026-10-02 digest](digests/2026-10-02.md)

The week's one substantive addition is a backfill: **GitSpawn**, a class in which a repository's own `.git/config` makes a command-line coding agent run attacker-chosen code through `core.fsmonitor`, disclosed on Sep 2–4, 2026 and affecting seven agents (per the Cloud Security Alliance research notes, corroborated by press). The digest records no new catalog-mapped entries and flags a verification item against the local-execution guards.

| Entries | Catalog answer | Status |
| :--- | :--- | :--- |
| GitSpawn, on the AML.T0112 row | `block-unsafe-code-execution`, `block-destructive-commands` | enforced (slice); open verification flag, not a status change |
| MITRE ATLAS | no release newer than v2026.09 | no change |

Every weekly digest is in [`digests/`](digests/). Each is dated and immutable.

## Install

The ledger needs no install. To put the policies it points at into your own repo, install the frozen engine (not on PyPI; Python 3.11 or newer):

```bash
pip install "chock @ git+https://github.com/open-coder-ai/chock@992711af4cf8d4fd9c4c861f10ef6e53374d75d7"
```

## Two ways to adopt

<img src="https://raw.githubusercontent.com/open-coder-ai/chock/main/docs/assets/readme/adopt.png" alt="The two adoption routes: policies installed in your repository, or Chock plugins installed in your coding agent." width="760">

| | In your repository (for teams) | In your coding agent, as plugins |
| :--- | :--- | :--- |
| Steps | `chock init .`, then `chock add <id> --ref <catalog commit> --verify-sha <sha256> --skip-compile` for each policy, then `chock sync --repo . --ci` | Install the plugin for your client from its repo (below) |
| Where it runs | Your agent's hook where its client has one, at commit, and in CI | The client's pre-tool hook only |
| Strength | The commit gates are enforced at commit and in CI. Commit the result; every clone runs `chock sync --repo .` once, because git never clones hooks | Best-effort: the client's hook fails open, and it does not run in CI |

Plugin repos, with per-client install lines in each README: [Claude Code](https://github.com/open-coder-ai/chock-claude-plugins), [Copilot](https://github.com/open-coder-ai/chock-copilot-plugins), [Cursor](https://github.com/open-coder-ai/chock-cursor-plugins), [Codex](https://github.com/open-coder-ai/chock-codex-plugins), [Devin](https://github.com/open-coder-ai/chock-devin-plugins). Templates: [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) and [chock-example](https://github.com/open-coder-ai/chock-example). A third route, one Claude Code plugin from a selection of policies, comes from the chock.sh builder (launching soon).

## How it works: the ledger and its tags

- **Weekly sweep.** An automated review checks the published threat frameworks and the week's disclosed agent vulnerabilities, and drafts a delta digest against the running baseline.
- **Human review before publish.** Every digest lands as a pull request, read and approved by a maintainer before it merges.
- **Coverage honesty.** Each entry is tagged with the catalog's own tiers.

| Tag | Meaning |
| :--- | :--- |
| `enforced (slice)` | A deterministic gate or guard blocks a concrete slice of the threat, never the whole threat |
| `advisory` | Committed rule text every agent reads: real influence, no mechanism |
| `policy wanted` | In scope, nothing covers it, linked to a contributor issue |
| out of scope | Not addressable by a repo-local tool governing coding agents, declared rather than omitted |

Tags follow the catalog and can lag it between sweeps. For a policy's current tier, read the catalog's [`registry.yaml`](https://github.com/open-coder-ai/chock-catalog/blob/main/registry.yaml). Chock checks cost no tokens, because each is a script rather than a model, and Chock adds no new place your code goes.

| Where | What is there |
| :--- | :--- |
| [`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md) | The running ledger, refreshed in place: 14 sections, with a "Chock coverage against this ledger" table and the honest totals |
| [`digests/`](digests/) | One dated, immutable file per weekly sweep |
| [`docs/README.md`](docs/README.md) | The disclaimer, how to read a digest, how to contribute a policy |

## What it stops

This repo stops nothing. It records what the catalog does and does not reach. The ledger states its own scope: of its 400+ entries across 22 frameworks, the slice a repo-local governance tool can deterministically enforce is small, and it declines to show a matrix of green checkmarks. The catalog it scores has 71 policies: 35 enforced at commit, 11 in the agent (best-effort, fails open), 25 advisory (`registry.yaml` at `9a64623`). No agent reaches "enforced" today. Every OWASP Agentic (ASI01–ASI10) risk has at least one catalog policy mapped, and every mapping is partial: [`docs/coverage.md`](https://github.com/open-coder-ai/chock-catalog/blob/main/docs/coverage.md).

## FAQ for people and agents

**Does Chock use an LLM?** No. Each check is a deterministic script. The weekly sweep that drafts digests is a separate, human-reviewed process.

**Does my code leave my machine?** Chock adds no new place your code goes. The agent still sends context to its own model provider.

**Which agents does it work with?** See the plugin repos above and the [catalog](https://github.com/open-coder-ai/chock-catalog).

**How do I install it?** See the two routes above.

**What does it cost?** Free and open source (Apache-2.0).

**Does it replace SAST or code review?** No, and this ledger does not replace the sources it cites.

**Which OWASP and MITRE items does it cover?** The ledger lists every entry with its tag. The catalog's coverage report is the source for OWASP ASI.

## For tools and agents

- [`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md) and [`digests/`](digests/): the ledger and every weekly delta
- [`registry.yaml`](https://github.com/open-coder-ai/chock-catalog/blob/main/registry.yaml): every policy, its tier and eval counts
- Policy manifests, with `compliance` mappings: [`base/*/manifest.yaml`](https://github.com/open-coder-ai/chock-catalog/tree/main/base)
- [`docs/coverage.md`](https://github.com/open-coder-ai/chock-catalog/blob/main/docs/coverage.md): OWASP coverage
- Plugin `marketplace.json` in each plugin repo above
- chock.sh `/llms.txt` and `/api/index.json`: launching soon

## Contribute a threat or a fix

| You found | Do this |
| :--- | :--- |
| A published advisory or framework entry the ledger lacks | Open an issue with the canonical link, the publisher's version and the date; the next sweep picks it up |
| An entry that overstates the threat, or a tag that claims too much | Open an issue naming the entry and the source; these are the contributions we want most |
| A `policy wanted` entry you can close | Claim its linked issue and write the policy in the [catalog](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md) |
| A digest pull request you know the source for | Review it before it merges |

Conventions, including `git commit -s` sign-off, are in [CONTRIBUTING.md](CONTRIBUTING.md).

## Part of open-coder-ai

| Repository | What it is |
| :--- | :--- |
| [chock](https://github.com/open-coder-ai/chock) | The framework: write a policy once, enforce it on git hooks, CI and every agent |
| [chock-catalog](https://github.com/open-coder-ai/chock-catalog) | The policies, each graded by what it actually enforces |
| [agentseam](https://github.com/open-coder-ai/agentseam) | One handler API over every coding agent's hooks, instruction files and plugin packaging |
| [context-report](https://github.com/open-coder-ai/context-report) | A signed report format for whether a plugin, hook, skill or `AGENTS.md` works |
| [chock-claude-plugins](https://github.com/open-coder-ai/chock-claude-plugins) · [copilot](https://github.com/open-coder-ai/chock-copilot-plugins) · [cursor](https://github.com/open-coder-ai/chock-cursor-plugins) · [codex](https://github.com/open-coder-ai/chock-codex-plugins) · [devin](https://github.com/open-coder-ai/chock-devin-plugins) | The catalog compiled into each client's plugin format |
| [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) · [chock-example](https://github.com/open-coder-ai/chock-example) | Template repositories: what `chock init` leaves behind, and a working adoption |

Apache-2.0, see [LICENSE](LICENSE). Threat framework names and identifiers belong to their publishers (OWASP, MITRE, NIST and others); each digest links its sources.
