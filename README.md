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
    wash-version: v2.0.1 # Optional
```

### Inputs

| Name         | Description                                 | Default        |
| ------------ | ------------------------------------------- | -------------- |
| wash-version | The version of wash to install              | v2.0.1    |

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
     wash-version: v2.0.1
   - name: Check wash version
    run: wash --version
```
