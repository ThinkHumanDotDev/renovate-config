# renovate-config

ThinkHuman's shared [Renovate](https://docs.renovatebot.com) settings. Every repo in the org has a
root `renovate.json` that extends this preset and adds only its own rules:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>ThinkHumanDotDev/renovate-config"]
}
```

| File | Role |
| --- | --- |
| `default.json` | The preset: Mondays before 07:00 Europe/London, Dependency Dashboard on, `dependencies` label, plain commit subjects, no automerge unless a repo opts in. npm minor/patch in one weekly PR, Payload's packages in their own. Postgres majors as their own PR with a dump-and-reload warning. SHA pins on any ThinkHumanDotDev reusable workflow (`infrastructure`, `.github`) move to that repo's latest `main` in one PR. |
| `org-inherited-config.json` | Read by the Mend Renovate app for every repo. It sets only the onboarding config, so an onboarding PR proposes the `renovate.json` above instead of Renovate's stock one. |

Repos with Conventional Commits add `":semanticCommits"` after the preset. A change here reaches
every repo on its next Renovate run, so CI validates both files on every PR.

The Renovate app runs in Interactive mode with "Require config file" and "Create onboarding PRs" on
([org settings](https://developer.mend.io/github/ThinkHumanDotDev)).
