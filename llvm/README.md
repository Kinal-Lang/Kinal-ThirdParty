# Kinal - LLVM dependency repository

## [简体中文版](README.zh-CN.md)

# LLVM dependency layout

This directory contains the LLVM dependency used by Kinal.

It is intentionally kept in `Kinal-ThirdParty` instead of the main `Kinal` repository because:

- the extracted LLVM source tree is very large
- prebuilt LLVM packages are large and noisy in Git history
- code search and repository indexing become worse when full LLVM is mixed into the language repository

## Layout

- `src/`
  - LLVM source snapshots or extracted trees
  - current expected tree: `src/llvm-project/...`
- `manifests/`
  - version pins, download metadata, and bootstrap notes

## How Kinal uses this directory

The main repository looks for this directory as a sibling repository:

- `../Kinal-ThirdParty/llvm`

From there it resolves:

- source trees under `src/`
- manifests and version pins under `manifests/`

## Bootstrap entry point

Use the helper from the main repository:

```powershell
python ..\Kinal\infra\toolchains\setup_llvm.py --help
```

Common examples:

```powershell
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-prebuilt
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-src  
python ..\Kinal\infra\toolchains\setup_llvm.py --fetch-prebuilt --fetch-src
```