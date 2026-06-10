# python-bootstrap

`python-bootstrap` is a composite GitHub Action that sets up a requested Python runtime and
optionally normalizes `pip` before installing dependencies for the calling job.

## Usage

Use a released tag in downstream workflows:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: Dagitali/python-bootstrap@v1
        with:
          python-version: '3.13'
          pip-install: '-r requirements.txt'
      - run: python --version
```

Use the action from a checked-out copy when developing this repository:

```yaml
steps:
  - uses: actions/checkout@v6
  - uses: ./
    with:
      python-version: '3.14'
      upgrade-pip: 'false'
```

## Inputs

| Name | Required | Default | Description |
| --- | --- | --- | --- |
| `python-version` | Yes | N/A | Python version passed to `actions/setup-python`. |
| `pip-version` | No | `''` | Exact `pip` version to install. When set, this takes precedence over `upgrade-pip`. |
| `pip-install` | No | `''` | Arguments passed to `python -m pip install`. Empty skips dependency installation. |
| `upgrade-pip` | No | `'true'` | Upgrade `pip` to the latest available version before dependency installation. Use `'false'` to skip. |

Treat `pip-install` as trusted workflow configuration. Do not build it from untrusted issue, pull
request, or user-supplied text.

## Outputs

This action does not define outputs. It changes the calling job environment by making the requested
Python version active on `PATH` and, when requested, installing dependencies into that Python
environment.

## Supported Matrix

The repository CI validates the action on GitHub-hosted `ubuntu-latest`, `macos-latest`, and
`windows-latest` runners with Python `3.11`, `3.12`, `3.13`, and `3.14`.

## Permissions

The action itself does not require repository or token permissions. Calling workflows should grant
only the permissions needed by their own jobs.

## Version Pinning

Prefer a release tag such as `Dagitali/python-bootstrap@v1` or an exact version tag for normal use.
Pin to a full commit SHA when your workflow requires maximum supply-chain immutability.
