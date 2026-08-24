# Contributing

This repository holds runnable GitHub Actions workflows that back up written
claims about CI/CD and cloud cost. The whole point is that someone else can
reproduce the numbers, so contributions are judged on whether they keep that
true.

## Ground rules

A pair of workflows should differ in exactly one thing. If two knobs change at
once, the comparison doesn't prove anything.

Anyone with a fork should be able to run both sides and see the same shape of
result, without extra setup.

Any number that ends up in a README needs either a link or a run in this
repository that produced it.

Keep secrets out of the repository. That includes tokens, tenant ids,
subscription ids and internal hostnames, and it also includes placeholders that
look real enough to be copied by mistake.

## Making a change

1. Fork the repository and branch off `main`.
2. Add or edit workflows under `.github/workflows/`, one recipe per pull request.
3. Run both sides of the comparison from the Actions tab on your fork.
4. Update `README.md` with what the recipe isolates, how to reproduce it, and the
   numbers you measured. Include the cases where the optimisation doesn't pay off.
5. Open a pull request and fill in the template, with links to your runs.

## Workflow style

- pin actions to a released major version (`actions/checkout@v5`)
- give every job and step an explicit `name`
- set the narrowest `permissions` block the job actually needs
- prefer `workflow_dispatch` for demo recipes so nobody burns minutes by accident
- `actionlint` runs on every pull request and its findings block the merge
