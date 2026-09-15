# Demo materials

Files in this folder exist only for the 2-minute demo recording. None of them is loaded in production.

| File | Used by | Notes |
|---|---|---|
| `dashboard-seed.json` | `TLH_DEMO_SEED` (see the [GitHub App runbook](../runbooks/github-app.md)) | 30-day history added to the dashboard **at aggregation time**. The page shows a `Demo data` chip while it is loaded. No snapshot or receipt rows are created. |
| `recording-checklist.md` | the person recording | Pre-flight checks for the screen capture. |
| `storyboard.md`, `storyboard-v2.md` | script review | Earlier storyboard drafts kept for reference; the current script lives outside the repo. |

## Seed file shape

```json
{
  "_comment": "…",
  "totals": {"merged": 41, "gated": 13, "attested": 11, "forced": 2, "waiting": 0},
  "zones": [
    {"zone": "sample-app/app/auth/", "owner": "@daeungo1",
     "merged": 1, "gated": 1, "attested": 0, "forced": 1, "answerers": 0, "prs": [27]}
  ]
}
```

- `totals` are repository-wide counts for the window; `zones` are per-CODEOWNERS-zone counts.
- A gated merge is either verified (`attested`) or an exception (`forced`), so `gated == attested + forced` in every zone. The loader rejects a file that breaks this.
- `answerers` is a count, never a list of names. `prs` are the PR numbers shown in the Evidence column; numbers in the seed may not exist in the repository.
- Real merges recorded by the app are added on top of the seed, so the demo's live increment (for example `sample-app/app/auth/` going from 0 to 1 answerers) comes from an actual merge event.
