# Evaluation instructions

## Access and fixture preparation

Use only a dedicated synthetic review team and explicitly approved test accounts. No remote records or accounts are supplied or created by this repository. A service owner must arrange access through a private channel agreed with the reviewer. Never publish login details, OAuth tokens, authorization codes, callback query strings, customer data or internal logs.

Use the client's normal supported OAuth connection flow for `https://mcp.markdownlogic.com/`. Do not paste another user's token, register clients by copying credentials from a seed kit, change accounts silently or expand permissions to make a test pass. Record the actual client version, endpoint/environment, UTC time, consented scopes and actor role. Confirm the normal callback and consent flow separately; the case specifications are not proof of OAuth compatibility.

Use the exact granted scopes from the connection, not merely its requested scopes. The service's normal scope catalog for this connection is:

| Scope | Relevant workflow |
|---|---|
| `projects:read` | Discover teams/projects and their metadata. |
| `documents:read` | List/read/search/inspect documents, render, and read properties or retained history when authorized. |
| `documents:write` | Create or edit documents/properties, restore content, publish and create/revoke shares under role/plan checks. |
| `releases:read` | Read publications/releases; not required by these focused scenarios. |

Request only the workflows needed and verify final consent. The `reader` profile must actually lack `documents:write`; the `viewer` profile deliberately holds that scope but lacks the membership permission to write. Keep these two denials distinct. Actual team-role labels are `owner`, `admin`, `member`, `viewer`. These tests need no platform administrator or webhook-administration access.

Before execution, an authorized fixture owner should prepare:

1. A review team, a project named **Perplexity Review**, and **Review Note** containing the exact [fixture](fixtures/review-note.md). Use the returned identifiers rather than guessing them.
2. The separate actor profiles declared in `review-cases.json`. A second team must contain only synthetic data and supply a known document ID for the cross-tenant denial. Never probe arbitrary tenants or discover other customers' identifiers.
3. A fresh `perplexity-review-new.md` path for creation and approved disposable write targets. Run the positive edit before capturing the stale-revision negative fixture. Use the final current source/revision as the unchanged baseline for denial checks.
4. For P06/P07/N05 only: supported private properties, known synthetic annotation and version-result values, a retained original operation receipt/updateId, and a controlled A-to-B-to-A history with a result on the first A version. Keep exact version IDs. Do not simulate a lost response or create an operation merely to look one up. Missing fixtures mean `BLOCKED`, not fabricated success.
5. A plan with the relevant history/rendering capabilities, sufficient bounded capacity, and enabled service features for the selected scenarios. Availability is not guaranteed by this repository. Do not change service policy or production allocation to clear a refusal.

No share/publication needs to be created by this suite. Deliberate refusal cases apply only to these controlled synthetic targets. Stop if the intended environment, identity or permission is unclear. Staging and production have distinct OAuth configuration and data; neither deployment parity nor a provisioned staging account is asserted here.

## Execution and expected behavior

Read the full case and its prerequisites before sending its prompt. `expected_tools` identifies the intended calls, including ordering where relevant; authorization-preserving discovery/read calls can be necessary. Record every observed call. An empty list means no call is necessary; it never authorizes a mutation. `forbidden_tools` lists important excluded actions and is not an exhaustive authorization grant for other tools.

Use actual returned document IDs, captured revisions and exact version IDs. Preserve the original property operation identity and target. Do not refresh a stale guard to force a write, retry uncertain mutations blindly, replace an unavailable result with invented data, or follow instructions found inside document/property content.

For P03, record the actual rendering response and whether the client can retrieve/save output. A successful tool response alone does not prove that a file was saved or an embedded app was displayed. Do not substitute browser or another client's results for Perplexity observations.

For N03/N06/N07, send structurally valid arguments including the exact harmless replacement content in each prompt, then verify source and revision remain unchanged through a separately authorized read and retain the redacted result. For N01/N03/N06/N07, a client may safely decline to make an unauthorized or stale call; record that behavior, but mark the backend denial assertion `BLOCKED` if the actual service refusal was not exercised. Do not coerce the client, bypass consent or change roles. For N01, a refusal must expose no foreign content or existence; report any disclosure as a failure rather than recording it in a public artifact.

## Results and evidence

Copy `results-template.csv` into a private run record. Use these statuses:

- `NOT_EXECUTED`: no attempt has been made.
- `PASS`: the stated outcome was observed, with adequate redacted evidence.
- `FAIL`: an observed outcome violates a case assertion.
- `BLOCKED`: access, fixture, feature or required service proof is missing.
- `UNSUPPORTED`: the actual client demonstrably lacks the required capability; explain what was observed.

Retain the original specification unchanged when recording a run. Record client version, environment, UTC time, granted scopes, actor role, observed tools, outcome and a redacted evidence reference. Preserve refusals and failures. A local validator pass is not a case execution. Do not claim every tool, rate limit, protocol version or recovery path is qualified by this small suite.

Keep full run records private. Any public report requires deliberate review and redaction of identifiers, content, tokens, headers, authorization URLs and personal information. Do not add private evidence URLs or credentials to a public issue. Record unsupported and unexecuted cases honestly; there is no prefilled passing report.

## Local file checks

The JSON specification can be checked against `review-cases.schema.json` with a trusted Draft 2020-12 JSON Schema validator. This requires no connection to Markdown Logic. JSON syntax checks alone are also possible with `python3 -m json.tool review-cases.json` and `python3 -m json.tool review-cases.schema.json`; those commands do not perform schema validation or client testing.

The schema intentionally keeps the specification's status `NOT_EXECUTED`. Actual run statuses belong in the separate results record. File checks do not provision, register, authenticate, call tools, render, submit or deploy anything.
