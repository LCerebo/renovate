## Changes

Add basic experimental support for OCI DevOps hosted Git repositories through `platform: 'oci'`.
The initial integration supports a manual-review dependency update workflow.

Related discussion: [OCI DevOps hosted Git repository support (#47592)](https://github.com/renovatebot/renovate/discussions/47592).

- Authenticate REST API requests using an OCI SDK configuration profile and request signing through the Renovate HTTP client
- Clone and push branches using HTTPS credentials or environment-configured SSH
- Discover repositories by project OCID or compartment, excluding mirrored repositories
- Read repository files and resolve local configuration presets by repository OCID
- List, create, update, retarget, close, and reopen pull requests, and recognize manually merged or closed PRs
- Derive stable numeric identifiers from OCI PR OCIDs for the Renovate platform interface
- Add reviewers by user OCID and manage bot-authored, top-level PR comments
- Exclude incoming fork PRs from managed PR lists and lookups
- Block PR and branch automerge, including branch automerge with `ignoreTests` enabled
- Handle pagination, signed requests, temporary API failures, and interrupted PR updates
- Keep truncated PR descriptions stable and adapt the generated Markdown for OCI
- Document authentication, IAM policies, project setup, configuration, and experimental limitations

Issues, the Dependency Dashboard, draft PRs, labels, assignees, commit status checks, platform automerge, and fork creation are unsupported.
Branch status is reported as pending.
Unsupported operations are rejected or reported through warnings as documented.

Validation on Node.js 24.11.0:

- `pnpm check --all lib/modules/platform/oci lib/modules/platform/scm.ts lib/modules/platform/default-scm.spec.ts lib/workers/repository/update/branch/automerge.spec.ts`
- `pnpm check --no-test` for repository-wide lint, formatting, type, schema, and documentation checks
- `git diff --check`

All checks passed.
The OCI implementation has full statement, function, and branch coverage, with regression tests for branch automerge, cross-repository PR matching, and description truncation.
The validation used unit tests and mocked OCI API and Git operations.

## Context

Please select one of the following:

- [ ] This closes an existing Issue, Closes: # <!-- NOTE that this should NOT be a Discussion -->
- [x] This doesn't close an Issue, but I accept the risk that this PR may be closed if maintainers disagree with its opening or implementation. Because this does not close an Issue, I will add a minimal reproduction repository as part of this PR.

## AI assistance disclosure

Did you use AI tools to create any part of this pull request?

Please select one option and, if yes, briefly describe how AI was used (e.g., code, tests, docs) and which tool(s) you used.

- [ ] No — I did not use AI for this contribution.
- [ ] Yes — minimal assistance (e.g., IDE autocomplete, small code completions, grammar fixes).
- [x] Yes — substantive assistance (AI-generated non-trivial portions of code, tests, or documentation).
- [ ] Yes — other (please describe):

OpenCode with GPT-6 Astra reviewed the implementation, produced fixes and regression tests, updated documentation, and drafted this PR description.

### Use of AI in replying to PR comments

Who answers review comments:

- [x] @LCerebo will read and reply directly. **Name the account.**
- [ ] An agent will draft replies and @LCerebo will read them before they are posted. **Name the account.**
- [ ] An agent will draft replies and reply autonomously. **This is heavily discouraged, and we prefer that there are humans in the loop**
- [ ] Nobody has explicitly committed to replying.

## Documentation (please check one with an [x])

- [x] I have updated the documentation, or
- [ ] No documentation update is required

## How I've tested my work (please select one)

I have verified these changes via:

- [ ] Code inspection only, or
- [x] Newly added/modified unit tests, or
- [ ] No unit tests, but ran on a real repository, or
- [ ] Both unit tests + ran on a real repository

## Reproduction (please check one with an [x])

A reproduction is compulsory for PRs that do not close an Issue.
If this PR closes an Issue, confirm the fix against the Issue's reproduction instead.

- [ ] Reproduction repository that shows the bug or the new behavior: <URL>
- [x] A public reproduction is not possible, and I have stated the reason below

```markdown
This PR adds experimental support for a new platform.
I do not have the resources to provide a public OCI repository for testing.
The use case is an internal repository hosted in OCI DevOps, and I plan to test the integration on a private repository.
The scope is OCI DevOps platform support rather than a specific repository layout.
```

PRs without a reproduction or a stated reason will not be reviewed and may be closed.
