# setup-wash-action

**GitHub Action to install the wash CLI for wasmCloud development.**

## Overview

This action installs the [wash](https://github.com/wasmCloud/wasmCloud) CLI, a tool for developing and managing WebAssembly (Wasm) components with [wasmCloud](https://wasmcloud.com/).

> **_NOTE:_** This action sets up the next version of `wash` which does not yet have a stable 2.0 release.

## Usage

Add the following step to your workflow to install `wash`:

```yaml
- name: Setup wash CLI
  uses: wasmCloud/setup-wash-action@main
  with:
    wash-version: wash-v2.0.0-rc.8 # Optional
```

### Inputs

| Name         | Description                                                               | Default          |
| ------------ | ------------------------------------------------------------------------- | ---------------- |
| wash-version | The version of wash to install. Note this uses tags until 2.0 is released | wash-v2.0.0-rc.8 |

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
     wash-version: wash-v2.0.0-rc.8
   - name: Check wash version
    run: wash --version
```
