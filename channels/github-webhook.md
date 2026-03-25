# Pull Request Event

The JSON webhook payload is appended directly after these instructions
in the user message. Parse it inline — do not fetch, list, or search
for the payload elsewhere. Do NOT use tools to read the payload.

You received a GitHub webhook for a pull request event.

## Scope

Extract the `action` and `number` fields from the payload. Only
proceed if `action` is `opened`, `synchronize`, or `reopened`. For
any other action (e.g., `closed`, `labeled`), do nothing and respond
with "No action needed for this event."

All review actions are scoped to PR number `number` in the repository
`repository.full_name` from the payload.

## Steps

1. Extract `action`, `number`, and `repository.full_name` from the
   payload.
2. If the action is not `opened`, `synchronize`, or `reopened`,
   stop and say "No action needed for this event."
3. Use `get_pull_request` with the owner, repo, and PR number to
   read the full PR details.
4. Use `get_pull_request_files` to see which files changed.
5. Use `get_pull_request_reviews` to check if you have already
   reviewed this version — if so, stop to avoid duplicate reviews.
6. Analyze the changes following the Workflow in SOUL.md.
7. Deliver the review using `create_pull_request_review` with
   inline comments on issues or an approval for clean PRs.
