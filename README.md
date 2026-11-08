# Contributor License Agreement

One [Contributor License Agreement](CONTRIBUTOR_LICENSE_AGREEMENT.md) (CLA) covers every open-source project under [github.com/paularlott](https://github.com/paularlott), including projects created later. Contributors sign it once.

## For contributors

1. Read the [agreement](CONTRIBUTOR_LICENSE_AGREEMENT.md).
2. Sign it with [this form](https://forms.gle/47ZfWHQaqCF35MTU6), giving your GitHub username.

A maintainer then adds your username to the list of signers. Every pull request you open on any of the projects is checked against that list: it is labelled **cla: ok** when you have signed, and **cla: required**, with a comment explaining how to sign, when you have not.

## For maintainers

### The list of signers

The single list of signers is [`.clabot.json`](.clabot.json) in this repository. To accept a signer, add their GitHub username to it on `main`:

```json
{
  "contributors": ["paularlott", "new-signer"]
}
```

The `individuals` and `companies` shape is accepted too. Names are compared without regard to case.

A pull request that was blocked passes on its next run: when the contributor pushes, or when you re-run the **Check CLA status** job from the pull request's Checks tab.

### Adding the check to a project

Add `.github/workflows/cla-check.yml` to the project:

```yaml
name: CLA

on:
  pull_request_target:
    types: [opened, reopened, synchronize]

permissions:
  pull-requests: write
  issues: write

jobs:
  cla-check:
    uses: paularlott/cla/.github/workflows/cla-check.yml@main
```

The check appears on pull requests as **cla-check / Check CLA status**. Make it a required status check in the branch protection rules to block merging until the CLA is signed.

The workflow runs on `pull_request_target` so that pull requests from forks get a token that can label and comment. It never checks out or runs code from the pull request.

### Changing the agreement

Section 17 of the agreement says changes apply only to Contributions made after the new version takes effect. Note the date of each change in the commit message.
