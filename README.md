<div align="center">

<img src=".github/logo.svg" alt="chock-threat-intel: a weekly digest of agentic-AI threats, each scored against an enforceable policy catalog — what a policy already enforces, what is only advisory, and what is still an open gap. The mark is chock's: a wheel held by a chock wedge." width="110">

# chock-threat-intel

**Weekly threat ledger the catalog's policies answer to.**<br>
Every agentic-AI threat the frameworks publish — MITRE ATLAS, OWASP ASI, NIST, CISA, CSA and
more — scored against the [chock-catalog](https://github.com/open-coder-ai/chock-catalog):
**enforced**, **advisory**, or **`policy wanted`**.

[![Cadence: weekly](https://img.shields.io/badge/cadence-weekly-D9B45C?labelColor=0D1626)](digests/)
[![Human-reviewed](https://img.shields.io/badge/every_digest-human--reviewed-D9B45C?labelColor=0D1626)](#how-the-ledger-is-updated)
[![Frameworks tracked: 22](https://img.shields.io/badge/frameworks_tracked-22-D9B45C?labelColor=0D1626)](reference/agentic-threat-ledger.md)
[![Ledger entries: 400+](https://img.shields.io/badge/ledger_entries-400%2B-D9B45C?labelColor=0D1626)](reference/agentic-threat-ledger.md)
[![MITRE ATLAS v2026.09](https://img.shields.io/badge/MITRE_ATLAS-v2026.09-D9B45C?labelColor=0D1626)](reference/agentic-threat-ledger.md#mitre-atlas--mitre)
[![OWASP Agentic Top 10](https://img.shields.io/badge/OWASP_Agentic_Top_10-10%2F10_have_a_policy-D9B45C?labelColor=0D1626)](https://github.com/open-coder-ai/chock-catalog)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

[the threat ledger →](reference/agentic-threat-ledger.md) ·
[weekly digests →](digests/) ·
[the framework →](https://github.com/open-coder-ai/chock) ·
[the policy catalog →](https://github.com/open-coder-ai/chock-catalog)

</div>

> **Unofficial compilation — verify at the source.** We are not an authoritative source for
> the frameworks cited here. Full disclaimer: [`docs/README.md`](docs/README.md).

## Why teams need it

Agentic-AI threats move **weekly**: MITRE ATLAS ships new technique IDs, OWASP adds companion
documents, researchers disclose a zero-click plugin RCE, CISA adds the first MCP flaw to its Known
Exploited Vulnerabilities catalog. A security review done last quarter is already out of date.

A framework tells you what *could* go wrong. This ledger answers the question a team adopting
coding agents actually has to answer: **which of these threats is blocked in our repositories
today, which only rests on an instruction the agent reads, and which is still an open gap?**

- **Nothing is overclaimed.** `enforced` means a deterministic gate exits non-zero on a named
  slice of the threat — never the whole threat. *A rule an agent reads is advice. A hook that
  exits non-zero is a control.*
- **Nothing is silently dropped.** Threats a repo-local tool cannot reach are listed and marked
  `out of scope`, not omitted.
- **Every gap is a front door.** A `policy wanted` entry links to a contributor issue in the
  catalog.

Of the ledger's 400+ entries, the slice a repo-local governance tool can deterministically
enforce is small, and the ledger says so: see
[the honest totals](reference/agentic-threat-ledger.md#the-honest-totals).

## This week: [2026-09-04 digest](digests/2026-09-04.md)

MITRE ATLAS v2026.08 added 19 IDs; the two in scope for a repo-local coding-agent guard
are already covered:

| Entries | Catalog answer | Status |
| :--- | :--- | :--- |
| AML.T0118, .000–.001 (agent-to-agent comms) | `owasp-asi07-insecure-inter-agent-communication` | advisory |
| AML.T0016.004, T0017.002 (malicious agent tools) | `block-unpinned-agent-components` (hash-pinned `chock.lock` installs) | enforced (slice) |

Newer digests: [2026-09-11](digests/2026-09-11.md) · [2026-09-18](digests/2026-09-18.md) ·
[2026-09-25](digests/2026-09-25.md).

## Coverage

Every new entry from this week's digest, mapped to a catalog policy where the digest names
one — never guessed:

| MITRE ATLAS v2026.08 entry | Catalog policy | Status |
| :--- | :--- | :--- |
| AML.T0118, T0118.000–.001 | `owasp-asi07-insecure-inter-agent-communication` | advisory |
| AML.T0016.004, T0017.002 | `block-unpinned-agent-components` | enforced (slice) |
| AML.T0116, T0117, T0119–T0128, T0016.003, T0017.001 (14 IDs) | — | out of scope — adversary tradecraft outside a repo-local coding-agent guard |

The full historical mapping lives in
[`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md), refreshed in
place by each sweep.

## How to read the ledger

Each entry carries the publisher's own ID, a catalog answer, and one status — the catalog's own
honesty tiers, plus `out of scope`:

| Status | What it means | What protects you | What to do |
| :--- | :--- | :--- | :--- |
| ✅ **enforced (slice)** | a deterministic gate or guard blocks a concrete, named slice of the threat — never the whole threat | a git hook, CI gate or pre-tool hook that exits non-zero | adopt the named policy; challenge the tag if you find a bypass |
| ◐ **advisory** | committed rule text every agent reads | the agent's compliance — real influence, no mechanism | treat as guidance; a gate that enforces a slice is a welcome contribution |
| ◻ **`policy wanted`** | in scope for a repo-local guard, and nothing covers it yet | nothing | claim the linked catalog issue |
| — **out of scope** | not addressable by a repo-local tool governing coding agents (training pipelines, model weights, RAG infrastructure, org identity) | controls outside the repo | listed anyway, so the gap is visible |

| Where | What it holds |
| :--- | :--- |
| [`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md) | the running ledger: every framework, entry by entry, with publisher, version, date and canonical link, then the coverage crosswalk (OWASP ASI01–10, OWASP T1–T17, OWASP LLM Top 10, MITRE ATLAS) |
| [`digests/`](digests/) | one dated, immutable file per week — the delta against the prior week, starting from the [2026-08-16 baseline](digests/2026-08-16-baseline.md) |
| [`docs/README.md`](docs/README.md) | the full disclaimer, how to read a digest, and how to turn a `policy wanted` entry into a policy |

Entries reference the OWASP Agentic Threats spine (T1–T17) and MITRE ATLAS technique IDs, so the
same threat is traceable across frameworks and across weeks.

<details>
<summary>What <code>enforced</code> looks like in practice</summary>

<p align="center">
  <img src="https://raw.githubusercontent.com/open-coder-ai/chock/main/docs/assets/demo.gif" width="760" alt="Terminal: five security guards adopted from the catalog; a hard-coded AWS key, an MCP server at @latest, a wildcard IAM grant, model output piped into os.system and a Trojan Source bidi override are each refused at commit; the fixed file commits cleanly.">
</p>

Each guard in the recording is a catalog policy in the enforced tier: the change is refused at
commit, with a non-zero exit, before it lands. That is the bar an `enforced (slice)` tag in
this ledger points at.

</details>

## How the ledger is updated

- **Weekly sweep.** An automated review checks the published threat frameworks (OWASP
  GenAI/ASI, MITRE ATLAS, NIST, CISA, CSA, vendor taxonomies) and the week's disclosed agent
  vulnerabilities, and drafts a delta digest against the running baseline.
- **Human review before publish.** Every digest lands as a pull request, read and approved
  by a maintainer before it merges. Nothing on `main` is unreviewed automation output.
- **Coverage honesty.** Each entry is tagged `enforced` (a gate blocks a slice of it),
  `advisory` (rule text an agent reads), or `policy wanted` (nothing covers it, linked to
  a contributor issue) — the catalog's own tiers.

More on reading a digest and contributing a policy: [`docs/README.md`](docs/README.md).

## Contribute a threat or a fix

None of these need code, except the last:

| You have… | Do this |
| :--- | :--- |
| **A threat the ledger lacks** — a published advisory or framework entry | open an [issue](https://github.com/open-coder-ai/chock-threat-intel/issues/new) with the canonical link and the publisher's version and date; the next weekly sweep picks it up |
| **A coverage tag that claims too much** | `enforced` claims a gate blocks a slice of the threat. A case the gate lets through is a finding for the [catalog](https://github.com/open-coder-ai/chock-catalog/issues/new/choose), and the tag here follows the catalog |
| **An entry that overstates the threat** | say which entry and link the source that shows the correction — the contribution we want most |
| **Knowledge of a source** | review an open digest pull request before it merges; that is what the human-review step is for |
| **Time to close a `policy wanted` gap** | claim the linked catalog issue, `chock init` a scratch repository and ask your agent to run the `policy-init` skill, then follow the catalog's [contributing guide](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md) — a policy claims only what it can do, and evals are the argument |

Every entry cites publisher, version, date and canonical link; sign your commits with
`git commit -s` (DCO). Conventions: [CONTRIBUTING.md](CONTRIBUTING.md). Security vulnerabilities
in the tools this repository points at go to that repository's `SECURITY.md`, never to a public
issue here.

## Part of open-coder-ai

Everything under [open-coder-ai](https://github.com/open-coder-ai) is built on one rule: a claim
must match a mechanism. Together they are security guardrails for coding agents — Chock refuses
the dangerous action before it lands, as a git hook, a CI gate, or the agent's own pre-tool hook.
Where this repository sits among the others:

| Repository | What it is |
| :--- | :--- |
| [agentseam](https://github.com/open-coder-ai/agentseam) | the primitives — one handler API over every coding agent's hooks, instruction files, plugin packaging and config, with a verified capability matrix across 16 agents |
| [chock](https://github.com/open-coder-ai/chock) | the compiler — one policy into git hooks, CI gates and native pre-tool hooks |
| [chock-catalog](https://github.com/open-coder-ai/chock-catalog) | the policies — 48 (19 enforced-at-commit, 9 best-effort in-agent, 20 advisory), 1,179 eval cases, 1,019 replayed deterministically in CI |
| [context-report](https://github.com/open-coder-ai/context-report) | the evidence — a signed report of whether a plugin, hook, skill or `AGENTS.md` actually works |
| **chock-threat-intel** | the threat ledger the catalog's policies answer to (this repository) |
| [chock-claude-plugins](https://github.com/open-coder-ai/chock-claude-plugins) · [copilot](https://github.com/open-coder-ai/chock-copilot-plugins) · [cursor](https://github.com/open-coder-ai/chock-cursor-plugins) · [codex](https://github.com/open-coder-ai/chock-codex-plugins) | the catalog compiled into each client's native plugin format; generated only, rebuilt and diffed in CI |
| [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) · [chock-example](https://github.com/open-coder-ai/chock-example) | template repositories: exactly what `chock init` leaves behind, and a working adoption with one policy per layer |

## License

Apache-2.0 — see [LICENSE](LICENSE). Threat framework names and identifiers belong to
their publishers (OWASP, MITRE, NIST, and others); each digest links its sources.
