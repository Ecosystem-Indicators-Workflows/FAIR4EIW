# EIW FAIR check kit

Scores a workflow repository against the ARDC FAIR Software Checklist (v0.2)
and the EIW targets in FAIR4EIW Appendix D. After every merge to `main` it
updates a FAIR section in the repository README with a badge, a summary table,
the list of gaps and a per-question plot.

## Files

| File | Purpose | Edit per workflow? |
|------|---------|--------------------|
| `.fair/fair_check.R` | Detection rules, scoring, plot, README update | No (shared) |
| `.fair/fair-checklist.yml` | Answers that cannot be detected, hints, overrides | Yes |
| `.github/workflows/fair.yml` | GitHub Action: run on merge, commit results | No (shared) |

Outputs written to the workflow repository:

- `fair/fair-scores.png`: plot shown in the README
- `fair/fair-score.json`: scores and evidence, for the EIW catalogue
- `README.md`: block between `<!-- FAIR:START -->` and `<!-- FAIR:END -->`

## Add to a workflow repository

```bash
cp -R fair-kit/.fair fair-kit/.github <path-to-workflow-repo>/
```

Then:

1. Edit `.fair/fair-checklist.yml` (formats, website, hints).
2. Put the markers where the section should appear in the README;
   otherwise it is appended at the end.
3. Commit and merge to `main`. The section appears after the first run;
   **Actions → FAIR check → Run workflow** runs it on demand.

Run locally from the repository root:

```bash
Rscript .fair/fair_check.R
```

## Updating the rules

Change `.fair/fair_check.R` here, then copy it into each workflow repository.
Each detection rule is one function named after its ARDC question ID.

## Steps

1. Bring three files with exact folder locations to your new workflow repo
2. Make sure the `.fair/fair-checklist.yml` is all reflecting the current process of the workflow we are assessing.
3. Put markers in `README.md`
   ```
   <!-- FAIR:START -->
   <!-- FAIR:END -->
   ```
4. run locally from your branch to test
