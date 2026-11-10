# Performance improvement ideas

This repository is small, but the same patterns apply to larger workflows. These are the ten highest-value performance improvements to look for in automation and CI pipelines:

1. Use shallow checkouts in GitHub Actions with `fetch-depth: 1` to avoid downloading full git history.
2. Restrict workflow triggers with `paths` and `paths-ignore` so jobs only run when relevant files change.
3. Add `concurrency` groups to cancel redundant runs and keep the latest build result visible.
4. Cache dependency folders (for example `~/.npm`, `~/.cache`, or package manager caches) between runs.
5. Split long jobs into parallel tasks so independent work can finish simultaneously instead of serially.
6. Guard expensive steps with `if:` conditions to skip no-op work when prerequisites are not satisfied.
7. Reuse outputs from earlier steps instead of re-fetching the same repository or repeating API calls.
8. Keep external repositories and templates checked out in a single, minimal fetch rather than downloading repeated copies.
9. Pin external actions to a stable commit or version and prefer reusable workflows to reduce repeated setup overhead.
10. Reduce log volume and comment churn by only posting updates when values actually change or when a job reaches a meaningful milestone.

## Selected improvement for this PR

The highest-impact, lowest-effort improvement here is #1: shallow checkouts. It reduces clone time on every workflow run without changing behavior, which makes the dataset exercise feel faster immediately.

This PR applies that optimization across the exercise workflows by adding `fetch-depth: 1` to each checkout step.
