# YAML Lint - GitHub Action

GitHub Action for linting YAML files using yamllint.

This action is derived from [ibiqlik/action-yamllint@v3](https://github.com/ibiqlik/action-yamllint), with modifications to support execution on `ubuntu-slim` and other GitHub runners.

## Usage

Simple as:

```yaml
- uses: khiemdoan/yaml-linting-action@v1
```

### Optional input parameters

- `files` - Enter file/folder (space separated), wildcards accepted. Examples:
  - `.` - run against all yaml files in a directory recursively (default)
  - `file1.yaml`
  - `file1.yaml file2.yaml`
  - `kustomize/**/*.yaml mychart/*values.yaml`
- `config_file` - Path to custom configuration
- `config_data` - Custom configuration (as YAML source)
- `format` - Format for parsing output `[parsable,standard,colored,github,auto] (default: parsable)`
- `strict` - Return non-zero exit code on warnings as well as errors `[true,false] (default: false)`
- `no_warnings` - Output only error level problems `[true,false] (default: false)`

**Note:** If `.yamllint` configuration file exists in your root folder, yamllint automatically uses it.

### Example usage in workflow

```yaml
---
name: YAML Lint

on:  # yamllint disable-line rule:truthy
  push:
  pull_request:

jobs:
  yaml-lint:
    runs-on: ubuntu-slim
    steps:
      - uses: actions/checkout@v6

      - name: yaml-lint
        uses: khiemdoan/yaml-linting-action@v1
        with:
          files: .
```
