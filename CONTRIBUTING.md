# Contributing

Thanks for taking the time. This repository holds runnable GitHub Actions
workflows that back up written claims about CI/CD and cloud cost. The value is
that the numbers can be reproduced, so contributions are judged on whether they
keep that true.

## Ground rules

- **One variable per recipe.** A pair of workflows must differ in exactly one
  thing. If two knobs change, the comparison proves nothing.
- **Reproducible by anyone.** A reader with a fork and no extra setup must be
  able to run both workflows and see the same shape of result.
- **Claims carry sources.** Any number in a README needs either a link or a run
  in this repository that produced it.
- **No secrets.** No tokens, tenant ids, subscription ids, or internal hostnames,
  not even as realistic-looking placeholders.

## Making a change

1. Fork the repository and branch off `main`.
2. Add or edit workflows under `.github/workflows/`, one recipe per pull request.
3. Run both sides of the comparison from the Actions tab on your fork.
4. Update `README.md` with what the recipe isolates, how to reproduce it, and the
   numbers you measured — including the case where the optimisation does not pay off.
5. Open a pull request and fill in the template, including the run links.

## Workflow style

- Pin actions to a released major version (`actions/checkout@v5`)
- Give every job and step an explicit `name`
- Set the narrowest `permissions` block the job actually needs
- Prefer `workflow_dispatch` for demo recipes so nobody burns minutes by accident
- The pull-request CI runs `actionlint`; findings block the merge
