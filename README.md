# setup-wash-action

**GitHub Action to install the wash CLI for wasmCloud development.**

## Overview

This action installs the [wash](https://github.com/wasmCloud/wash) CLI, a tool for developing and managing WebAssembly (Wasm) components with [wasmCloud](https://wasmcloud.com/).

> **_NOTE:_** This action sets up the next version of `wash` which does not yet have a stable 1.0 release.

## Usage

Add the following step to your workflow to install `wash`:

```yaml
- name: Setup wash CLI
 uses: wasmCloud/setup-wash-action@main
 with:
  wash-version: 0.51.1 # Optional: specify a version, e.g. "1.0.0-beta.2"
```

### Inputs

| Name         | Description                                                               | Default            |
| ------------ | ------------------------------------------------------------------------- | ------------------ |
| wash-version | The version of wash to install. Note this uses tags until 1.0 is released | wash-v1.0.0-beta.2 |

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
