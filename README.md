<div align="center">

<img src=".github/logo.svg" alt="Chock logo" width="90">

# chock-threat-intel

**A weekly digest of agentic-AI threats — scored against an enforceable policy catalog.**

[the framework →](https://github.com/open-coder-ai/chock) ·
[the policy catalog →](https://github.com/open-coder-ai/chock-catalog) ·
[latest digest →](digests/)

</div>

Most threat feeds tell you what to worry about. This one also tells you what a policy
already **enforces** about it, what is only **advisory**, and what is an open
**`policy wanted`** — an invitation to contribute a gate to the
[catalog](https://github.com/open-coder-ai/chock-catalog).

## How it works

- **Weekly sweep.** An automated review checks the published threat frameworks (OWASP
  GenAI/ASI, MITRE ATLAS, NIST, CISA, CSA, vendor taxonomies) and the week's disclosed
  agent vulnerabilities, and drafts a delta digest against the running baseline.
- **Human review before publish.** Every digest lands as a pull request and is read and
  approved by a maintainer before it merges. Nothing on this repo's `main` is
  unreviewed automation output — an unverified security claim is worse than none.
- **Coverage honesty.** Each entry is tagged with its status against the catalog:
  `enforced` (a gate blocks a slice of it), `advisory` (rule text an agent reads),
  or `policy wanted` (nothing covers it — linked to a contributor issue). The tags use
  the same tiers the catalog's own README defines, and the same rule: never claim more
  than the mechanism does.

## Reading a digest

One file per week in [`digests/`](digests/), newest first. Entries reference the OWASP
Agentic Threats spine (T1–T17) and MITRE ATLAS technique IDs, so the same threat is
traceable across frameworks and across weeks.

## Contributing a policy from a `policy wanted` entry

1. Open the linked issue and claim it.
2. `chock init` a scratch repo and ask your agent to run the `policy-init` skill — it
   scaffolds a conformant policy folder.
3. Follow the catalog's
   [contributing guide](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md):
   a policy claims only what it can do, and evals are the argument.

Corrections are contributions too — including "this entry overstates the threat" and
"this coverage tag claims too much". Especially those.

## License

Apache-2.0 — see [LICENSE](LICENSE). Threat framework names and identifiers belong to
their publishers (OWASP, MITRE, NIST, and others); each digest links its sources.
