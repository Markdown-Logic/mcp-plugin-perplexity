# Markdown Logic: Perplexity connector evaluation

Synthetic evaluation materials for the private Markdown Logic MCP connector in Perplexity. They provide prompts, expected tool use, scope and role prerequisites, and positive/negative outcomes for review.

**Actual Perplexity execution: NOT_EXECUTED.** This repository does not demonstrate a passing Perplexity integration, an approved directory listing, or a provisioned reviewer account. Specification version **1.0.0** is the version of these materials, not the hosted server or protocol version.

## Start here

- [Evaluation instructions](EVALUATION.md): access prerequisites, safe execution and evidence rules.
- [Review cases](review-cases.json): seven positive and seven negative scenarios.
- [JSON Schema](review-cases.schema.json): Draft 2020-12 structure for the specification.
- [Results template](results-template.csv): one `NOT_EXECUTED` row per case; record actual observations separately.
- [Review Note fixture](fixtures/review-note.md): fictional content with a marker and an explicitly untrusted instruction sample.

The connection under review is **https://mcp.markdownlogic.com/**, using per-user browser OAuth with PKCE S256 and dynamic client registration. Account access, granted scopes, team roles, plan capabilities and service availability still apply. This repository grants no access and contains no credentials.

The anonymous converter at `https://markdownlogic.com/mcp` is a separate service profile and is outside this evaluation. These materials contain no installable plugin manifest, launcher, account-creation script or automatic test runner. They do not assert which MCP, OAuth, rendering or file-saving capabilities Perplexity currently supports.

## What the cases cover

Authorized discovery and document reads; one requested draft; revision-protected editing; rendering without implicit sharing; current notes versus exact-version results; receipt lookup; tenant boundaries; ambiguous sharing intent; stale revisions; untrusted document instructions; repeated source bytes with distinct versions; missing write scope; and viewer-role denial.

An expected result is a test specification. Mark a case passed only after observing its stated outcome. Missing accounts, fixtures, plan features or client capabilities remain blocked or unsupported, with the reason recorded. Local JSON/schema validation does not execute OAuth, call tools, seed data, render a file or prove client conformance.

## Documentation and support

- [Connect an AI assistant](https://markdownlogic.com/help/en/connect-an-ai-assistant)
- [Privacy](https://app.markdownlogic.com/#/privacy)
- [Security](https://app.markdownlogic.com/#/security)
- Support: support@markdownlogic.com

The app policy links are browser routes. Test access must be arranged privately; do not put secrets, tokens, customer records or unredacted transcripts in this public repository.

## License

[MIT License](LICENSE), copyright 2026 Lemuridae Labs. [Provenance and scope](NOTICE.md). Product names and trademarks do not imply endorsement.
