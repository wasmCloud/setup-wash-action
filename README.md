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
    wash-version: wash-1.0.0-beta.9 # Optional
    plugins: "ghcr.io/wasmcloud/plugin-name:v1.0" # Optional, comma-delimited list of plugin URIs
```

### Inputs

| Name         | Description                                                                       | Default            |
| ------------ | --------------------------------------------------------------------------------- | ------------------ |
| wash-version | The version of wash to install. Note this uses tags until 1.0 is released         | wash-v1.0.0-beta.9 |
| plugins      | YAML array of plugin URIs to install (OCI artifacts from registries like ghcr.io) | (none)             |

### Plugin Caching

When plugins are specified, this action automatically caches them using `actions/cache` to improve performance across workflow runs. The action dynamically determines the correct cache and plugin directories using `wash config info`, ensuring compatibility across different wash configurations and operating systems.

Since Wasm plugins are platform-agnostic, the cache is shared across different operating systems, maximizing cache hit rates across your workflows.

The cache key includes:

- Action configuration hash
- Plugin list (OCI URIs and tags)

Cached directories:

- Plugin directory (from `wash config info -o json | jq .data.plugin_dir`)

Plugins are re-downloaded when the plugin list changes. Note that mutable tags like `:latest` will only update when you modify your workflow configuration, not automatically when the underlying image changes.

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
     wash-version: wash-1.0.0-beta.9
     plugins: "ghcr.io/wasmcloud/example-plugin:v0.1.0,ghcr.io/wasmcloud/another-plugin:v1.2.3"
   - name: Check wash version
    run: wash --version
   - name: List installed plugins
    run: wash plugin list
```
