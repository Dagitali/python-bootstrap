# python-bootstrap

A composite GitHub Action that sets up a requested Python runtime environment,
optionally normalizes pip, and optionally installs a provided dependency list to
keep workflow jobs consistent.

## Usage

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
```

### Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `python-version` | **Yes** | — | Python version to install via `actions/setup-python`. |
| `pip-version` | No | `''` | Exact pip version to install instead of upgrading to latest. |
| `pip-install` | No | `''` | Arguments passed to `python -m pip install`. Empty skips dependency installation. |
| `upgrade-pip` | No | `'true'` | Upgrade pip to the latest available version before installing dependencies. Ignored when `pip-version` is set. |

### Examples

#### Minimal — Python only

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
```

#### Pin a specific pip version

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
    pip-version: '25.0.1'
```

#### Install project dependencies

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
    pip-install: '-r requirements.txt'
```

#### Install the current package in editable mode with extras

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
    pip-install: '-e ".[dev,test]"'
```

#### Skip pip upgrade

```yaml
- uses: Dagitali/python-bootstrap@v1
  with:
    python-version: '3.13'
    upgrade-pip: 'false'
```

## License

Copyright © 2026 Dagitali LLC. All rights reserved.

See [LICENSE](LICENSE) for details.
