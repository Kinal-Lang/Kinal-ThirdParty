# Kinal - CivetWeb dependency repository

## [简体中文版](README.zh-CN.md)

# CivetWeb dependency layout

This directory contains the CivetWeb dependency used by Kinal `IO.Web`.

It is intended to keep:

- pinned public headers in `include/`
- pinned source files in `src/`
- small metadata files in `manifests/`

It should not permanently track target-specific generated objects or local machine build outputs.

## Layout

- `include/`
  - public CivetWeb headers used by Kinal runtime and native glue
- `src/`
  - pinned upstream CivetWeb source tree
- `manifests/`
  - version pins, notes, and future native build metadata

## How Kinal uses this directory

The main repository treats this directory as a sibling dependency repository:

- `../Kinal-ThirdParty/civetweb`

From here it uses:

- `include/` for public headers
- `src/` for native rebuild inputs
- `manifests/` for small metadata and pinned version notes

## Build intent

Kinal should build CivetWeb native artifacts from source when needed instead of keeping long-lived prebuilt outputs in this repository.

That keeps the repository cleaner and avoids mixing:

- upstream source
- generated objects
- host-local build products

## Notes

- `VERSION.txt` is the pinned reference for the upstream version or commit
- `LICENSE.md` and `SECURITY.md` are retained as part of the vendored dependency metadata
- if a future build cache is needed, it should live in ignored working directories rather than committed repository structure
