# Agents

## Module Identity

This repository is the standalone Autodoree Factory integration program. It
owns top-level factory behavior that requires both Autodoree host/effect
orchestration and Flowdoree Extend Factory projection.

Treat this repository as a complete program and REPL boundary. It must be
usable as the top-level composition program without pushing integration logic
down into its dependencies.

## Dependency Direction

- This repository may depend on `Autodoree`.
- This repository may depend on `flowdoree_extend_factory`.
- Do not make either dependency learn about this top-level integration layer.
- Do not copy lower protocol schemas into this repository as new authority;
  consume the dependency-owned protocol contracts instead.

## Program Boundary

This repository must treat `Autodoree` and `flowdoree_extend_factory` as
independent programs. Integration code should launch or connect to each through
its repo-owned protocol or IPC boundary rather than importing private modules
across repo boundaries.

The default local IPC standard is NDJSON over stdio. If a WebSocket transport
is used for an existing dependency service, it remains an optional transport,
not the default REPL boundary.

## Protocol Contract

- Protocol names owned here should describe only top-level factory integration
  operations.
- Protocol payloads must be versioned and schema-backed before another program
  consumes them.
- The canonical request envelope is:
  `{ "id": "...", "method": "...", "params": { ... } }`.
- The canonical success response is:
  `{ "id": "...", "ok": true, "result": ... }`.
- The canonical error response is:
  `{ "id": "...", "ok": false, "error": { "message": "..." } }`.
- This repository owns only its top-level method names, parameter schemas,
  result schemas, and compatibility policy. Lower contracts remain owned by
  their source repositories.

## Cross Platform

All program and REPL entrypoints must work on Linux, Windows, and macOS.
Avoid OS-specific shell syntax, path separators, daemon assumptions, and
terminal behavior in portable commands. Prefer portable process launch,
stdio, JSON, and path handling.

## Verification

Before changing protocol or module-boundary behavior:

- Check that lower dependencies do not mention this top-level repository.
- Confirm submodule status is clean and points at intended dependency commits.
- Confirm `git diff --stat` contains only the intended documentation or
  protocol-surface changes.
