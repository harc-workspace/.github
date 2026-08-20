# Automatic instruction synchronization

The workflow at `.github/workflows/sync-instructions.yml` copies the shared instruction contexts from `instruction-source/` into the four HARC repositories and opens one review-ready pull request per repository.

## Required organization secret

Create an organization-level fine-grained personal access token and save it as:

```text
INSTRUCTION_SYNC_TOKEN
```

The token should be limited to these repositories:

- `harc-api`
- `harc-fe`
- `harc-gateway`
- `harc-aspire-host`

Required repository permissions:

- `Contents: Read and write`
- `Pull requests: Read and write`
- `Metadata: Read`

Add the token under the `harc-workspace` organization settings as an Actions secret. Do not commit the token or place it in a workflow file.

## Triggering synchronization

The workflow runs automatically when files under `instruction-source/` are changed on `main`. It can also be started manually from the Actions tab using **Run workflow**.

The workflow creates or updates the branch `automation/sync-shared-instructions` in each target repository. If there are no changes, no PR is opened.

Only shared context files are synchronized. Project-specific `AGENTS.md`, `copilot-instructions.md`, and language/framework instruction files remain owned by each target repository.
