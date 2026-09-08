# Contributing to chock-threat-intel

Everything here is a claim about a published source or about what the
[catalog](https://github.com/open-coder-ai/chock-catalog) enforces, so the rules are the
same ones the catalog uses: never claim more than the mechanism does, and cite the canonical
source for every entry.

## Ways to contribute

- **Claim a `policy wanted` entry.** Open its linked issue, then write the policy in the
  catalog — `chock init` a scratch repository and ask your agent to run the `policy-init`
  skill, which scaffolds a conformant folder. The catalog's
  [contributing guide](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md) covers the rest.
- **Report a miss.** Open an issue with the canonical link, the publisher's version and the
  date. The weekly sweep adds it to the ledger with that citation.
- **Correct an entry.** "This entry overstates the threat" and "this coverage tag claims too
  much" are the contributions we want most. Say which entry, and link the source that shows
  the correction.
- **Review a digest.** Digests land as pull requests and merge only after a human review.
  Comments from anyone who knows the source are welcome on the open pull request.

## Rules

- **Cite, never paraphrase from memory.** Every entry carries publisher, version, date and
  canonical link. An entry that cannot be traced does not merge.
- **Coverage tags follow the catalog.** `enforced` means a catalog gate exits non-zero on a
  slice of the threat; `advisory` means rule text an agent reads; `policy wanted` means
  nothing covers it. A tag is changed here only when the catalog changed.
- **The ledger is refreshed in place; digests are dated and immutable.** Correct a past
  digest by noting the correction in the next one, not by editing history.
- **Sign your commits.** `git commit -s` adds the Developer Certificate of Origin trailer,
  the same one the rest of the family requires.

Security vulnerabilities in the tools this repository points at go to that repository's
`SECURITY.md`, never to a public issue here.
