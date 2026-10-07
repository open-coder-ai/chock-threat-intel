<div align="center">

<p><img src="https://raw.githubusercontent.com/open-coder-ai/chock/main/docs/assets/readme/cover-chock-threat-intel.png" alt="Chock mark on a dusk-blue background." width="100%"></p>

</div>

# Teach your AI agent what not to do.

Open-source guardrails for AI coding agents: rules the agent reads, checks that run as it writes, and gates at commit and in CI. This repo is the weekly threat ledger those policies answer to.

[chock](https://github.com/open-coder-ai/chock) · [chock-catalog](https://github.com/open-coder-ai/chock-catalog) · chock.sh (launching soon)

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

chock-threat-intel is a human-reviewed, weekly compilation of published agentic-AI threat frameworks (OWASP, MITRE ATLAS, NIST, CISA, the Cloud Security Alliance and others), each entry scored against what the [Chock catalog](https://github.com/open-coder-ai/chock-catalog) does about it: enforced for a slice, advisory, `policy wanted`, or out of scope. Chock is open-source application security for code written by AI coding agents, with deterministic local checks, no model and no upload. Start with [the threat ledger](reference/agentic-threat-ledger.md) or the [weekly digests](digests/).

> **Unofficial compilation, verify at the source.** We are not an authoritative source for the frameworks cited here. Full disclaimer: [`docs/README.md`](docs/README.md).

## Application security for the code your agents write

Chock's policies exist because agents write code, run commands and install tools, and published threats describe how that goes wrong. This ledger is the list the catalog is checked against, so a gap is visible rather than implied. It does not stop any attack itself: the policies live in the [catalog](https://github.com/open-coder-ai/chock-catalog), and the ledger says which threats they reach and which they do not.

| Area | What gets refused | Policy | Tier |
| :--- | :--- | :--- | :--- |
| Java & Kotlin | injection, XXE, SSRF, unsafe deserialization, weak crypto, dependencies below a known fix | `java-security` | commit |
| Unsafe code, IAM | `eval`, `shell=True`, `os.system`, `pickle`; IAM `Action: *` | `block-unsafe-code-execution`, `block-wildcard-iam` | commit |
| Supply chain | dependencies off an allowlist, Actions on a mutable tag, MCP servers and images at `@latest` | `verify-dependency-exists`, `pin-github-actions`, `block-unpinned-agent-components` | commit |
| Agent code | host execution, unpinned MCP servers, approvals switched off, credential leaks | `agentic-code-security` | commit |
| OWASP Agentic Top 10 | a policy for each of ASI01 to ASI10; 7 have a slice refused at commit; 0 are fully covered | `owasp-asi01-agent-goal-hijack` to `owasp-asi10-rogue-agents` | advisory |
| Accessibility | a stripped `alt`, `aria-label`, label or `lang` | `no-a11y-regression` | commit |
| Prompt injection, memory | bidi and tag characters; secrets written into agent memory | `block-invisible-unicode`, `guard-memory-writes` | commit |
| Test integrity | deleted tests, lost assertions, new skips | `protect-test-integrity` | commit |
| Also included | secrets, destructive commands, agent self-protection | `scan-secrets`, `block-destructive-commands`, `protect-agent-config` | commit, in-agent |

### This week: [2026-10-02 digest](digests/2026-10-02.md)

The week's one substantive addition is a backfill: **GitSpawn**, a class in which a repository's own `.git/config` makes a command-line coding agent run attacker-chosen code through `core.fsmonitor`, disclosed on Sep 2–4, 2026 and affecting seven agents (per the Cloud Security Alliance research notes, corroborated by press). The digest records no new catalog-mapped entries and flags a verification item against the local-execution guards.

| Entries | Catalog answer | Status |
| :--- | :--- | :--- |
| GitSpawn, on the AML.T0112 row | `block-unsafe-code-execution`, `block-destructive-commands` | enforced (slice); open verification flag, not a status change |
| MITRE ATLAS | no release newer than v2026.09 | no change |

Every weekly digest is in [`digests/`](digests/). Each is dated and immutable.

## Install

chock is on PyPI, but the release there (0.15.2, 30 Sep 2026) is older than the engine this page describes. Install the frozen engine from its commit (Python 3.11 or newer):

```bash
pip install "chock @ git+https://github.com/open-coder-ai/chock@992711af4cf8d4fd9c4c861f10ef6e53374d75d7"
```

### Two ways to adopt it

The ledger itself needs no install. To put the policies it points at into your own repo:

1. **In your repository, for teams.** Run `chock init .`, then `chock add <id> --ref <catalog commit> --verify-sha <sha256> --skip-compile` for each policy, then `chock sync --repo . --ci`. Commit the result. Every clone runs `chock sync --repo .` once, because git never clones hooks. The commit gates are enforced at commit and in CI.
2. **In your coding agent, as plugins.** Best-effort, and they fail open: the client's hook does not run in CI. One repo per client: [Claude Code](https://github.com/open-coder-ai/chock-claude-plugins), [Copilot](https://github.com/open-coder-ai/chock-copilot-plugins), [Cursor](https://github.com/open-coder-ai/chock-cursor-plugins), [Codex](https://github.com/open-coder-ai/chock-codex-plugins), [Devin](https://github.com/open-coder-ai/chock-devin-plugins). Each README has the install line for its client. Templates: [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) and [chock-example](https://github.com/open-coder-ai/chock-example).
3. **One Claude Code plugin from a selection.** The chock.sh builder (launching soon) gives a `chock install --selection '…' --apply` command.

## How it works

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
| [`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md) | The running ledger, refreshed in place, with a "Chock coverage against this ledger" table and the honest totals |
| [`digests/`](digests/) | One dated, immutable file per weekly sweep |
| [`docs/README.md`](docs/README.md) | The disclaimer, how to read a digest, how to contribute a policy |

## What it stops

This repo stops nothing. It records what the catalog does and does not reach, and it declines to show a matrix of green checkmarks: the slice a repo-local governance tool can deterministically enforce is small. The catalog it scores has 71 policies: 35 enforced at commit, 11 in the agent (best-effort, fails open), 25 advisory (`registry.yaml` at chock-catalog `f25f5a3`). Every OWASP Agentic (ASI01 to ASI10) risk has at least one catalog policy mapped, 7 of them (ASI01 to ASI05, ASI07, ASI09) with a slice refused at commit, and every mapping is partial: [`docs/coverage.md`](https://github.com/open-coder-ai/chock-catalog/blob/main/docs/coverage.md).

## Guardrails, not guarantees

Tiers: `commit` is a git hook or CI gate that exits non-zero. `in-agent` is the agent's own pre-tool hook: best-effort, and it fails open. `advisory` is rule text the agent reads. No agent reaches `enforced` today. OWASP mappings are partial, none of the 10 Agentic risks is fully covered, and the engine is frozen at the commit above. Chock does not stop every attack: it closes common, known entry points before they ship.

## FAQ for people and agents

**Does Chock use an LLM?** No. Each check is a deterministic script. The weekly sweep that drafts digests is a separate, human-reviewed process.

**Does my code leave my machine?** Chock adds no new place your code goes. The agent still sends context to its own model provider.

**Which agents does it work with?** See the plugin repos above and the [catalog](https://github.com/open-coder-ai/chock-catalog).

**How do I install it?** See [Install](#install).

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

## Part of open-coder-ai

The 13 public repositories:

| Repository | What it is |
| :--- | :--- |
| [agentseam](https://github.com/open-coder-ai/agentseam) | Core: One handler API over every coding agent. |
| [chock](https://github.com/open-coder-ai/chock) | Core: Author a policy once, enforce it on every agent. |
| [chock-catalog](https://github.com/open-coder-ai/chock-catalog) | Policies: The policies, each labelled by what it enforces, with replayed evals. |
| [context-report](https://github.com/open-coder-ai/context-report) | Evidence: A signed report of whether an agent artifact works. |
| [chock-threat-intel](https://github.com/open-coder-ai/chock-threat-intel) | Evidence: A weekly threat ledger, each entry scored against the catalog. |
| [chock-claude-plugins](https://github.com/open-coder-ai/chock-claude-plugins) | Plugins: The catalog as Claude Code plugins (generated). |
| [chock-copilot-plugins](https://github.com/open-coder-ai/chock-copilot-plugins) | Plugins: The catalog as Copilot CLI and VS Code plugins (generated). |
| [chock-cursor-plugins](https://github.com/open-coder-ai/chock-cursor-plugins) | Plugins: The catalog as Cursor plugins (generated). |
| [chock-codex-plugins](https://github.com/open-coder-ai/chock-codex-plugins) | Plugins: The catalog as Codex plugins (generated). |
| [chock-devin-plugins](https://github.com/open-coder-ai/chock-devin-plugins) | Plugins: The catalog as Devin plugins (generated). |
| [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) | Template: What chock init leaves behind. |
| [chock-example](https://github.com/open-coder-ai/chock-example) | Template: A working adoption, one policy per layer. |
| [.github](https://github.com/open-coder-ai/.github) | Community: Org profile and community health files. |

## Contributing

| You found | Do this |
| :--- | :--- |
| A published advisory or framework entry the ledger lacks | Open an issue with the canonical link, the publisher's version and the date; the next sweep picks it up |
| An entry that overstates the threat, or a tag that claims too much | Open an issue naming the entry and the source; these are the contributions we want most |
| A `policy wanted` entry you can close | Claim its linked issue and write the policy in the [catalog](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md) |
| A digest pull request you know the source for | Review it before it merges |

Conventions, including `git commit -s` sign-off, are in [CONTRIBUTING.md](CONTRIBUTING.md).

Apache-2.0, see [LICENSE](LICENSE). Threat framework names and identifiers belong to their publishers (OWASP, MITRE, NIST and others); each digest links its sources.

