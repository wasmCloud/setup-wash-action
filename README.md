# setup-wash-action

**GitHub Action to install the wash CLI for wasmCloud development.**

## Overview

This action installs the [wash](https://github.com/wasmCloud/wash) CLI, a tool for developing and managing WebAssembly (Wasm) components with [wasmCloud](https://wasmcloud.com/).

### Security Features

This action implements secure installation practices:
- **Direct binary download** from official GitHub releases
- **SHA256 checksum verification** to prevent man-in-the-middle attacks
- **HTTPS-only downloads** with proper error handling
- **Cross-platform support** for Linux, macOS, and Windows

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
