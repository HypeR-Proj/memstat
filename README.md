<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# memstat

Allocation, retained-page and cache diagnostics.

Reads the Native memory inspector into a structured snapshot. Text and JSON output share
the same snapshot; baseline comparison validates that both samples belong to the same
boot.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

In a Native session with the required capabilities:

```sh
memstat --save /tmp/before.json
memstat --diff /tmp/before.json --classes
```

## Boundaries

Saving creates a new file and refuses to overwrite an existing one. Counters are
observations, not a request to reclaim memory; baselines from another boot are rejected.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
