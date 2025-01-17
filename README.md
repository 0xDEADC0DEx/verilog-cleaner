# Verilog Cleaner

## Introduction

This action lints Verilog code by running [`Verible`](https://google.github.io/verible/) and outputs its findings with [`reviewdog`](https://github.com/reviewdog/reviewdog) through GitHub APIs such as [GitHub Checks](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-status-checks).

## Inputs

### `github_token`

**required** The secret token for authenticating action work.

A good choice is to just input `${{ secrets.GITHUB_TOKEN }}`.

### `workdir`

**optional** The action working directory, relative to `${GITHUB_WORKSPACE}`.

Defaults to root directory of repository (`.`).

### `reporter`

**optional** A comprehensive list of reporters can be found [here](https://github.com/reviewdog/reviewdog#reporters).

Defaults to `github-check`.

## Minimal Example

```yaml
on: [push]

jobs:
  clean-verilog:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2 # Checkout source
    - uses: reviewdog/action-setup@v1 # Setup reviewdog
    - uses: SuibianP/verilog-cleaner@v1 # lint and format
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
    - uses: peter-evans/create-pull-request@v3 # Creates pull request with formatting results
      with:
        delete-branch: true
```
