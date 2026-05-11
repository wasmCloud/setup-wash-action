# setup-wash-action

**GitHub Action to install the wash CLI for wasmCloud development.**

## Overview

This action installs the [wash](https://github.com/wasmCloud/wasmCloud) CLI, a tool for developing and managing WebAssembly (Wasm) components with [wasmCloud](https://wasmcloud.com/).

## Usage

Add the following step to your workflow to install `wash`:

```yaml
- name: Setup wash CLI
  uses: wasmCloud/setup-wash-action@main
  with:
    wash-version: latest # Optional
```

When `wash-version` is `latest` (the default), the action resolves the most recent release of [wasmCloud/wasmCloud](https://github.com/wasmCloud/wasmCloud) on each run and uses the resolved tag as the cache key, so a new release is picked up automatically without serving a stale cache.

### Inputs

| Name         | Description                    | Default |
| ------------ | ------------------------------ | ------- |
| wash-version | The version of wash to install | latest  |

## Example Workflow

```yaml
name: wasmCloud Build

on: [push]

jobs:
 build:
  runs-on: ubuntu-latest
  steps:
   - uses: actions/checkout@v4
   - name: Setup wash CLI
    uses: wasmCloud/setup-wash-action@main
    with:
     wash-version: latest
   - name: Check wash version
    run: wash --version
```
