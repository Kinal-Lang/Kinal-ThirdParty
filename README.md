## Kinal-ThirdParty

## [简体中文版](README.zh-CN.md)

This repository stores large external dependencies or vendored source trees used by Kinal.

It exists separately from the main `Kinal` repository so the language/runtime/tooling source tree
stays smaller and easier to clone, review, and search.

[This link goes to the main Kinal repository](https://github.com/Kinal-Lang/Kinal)

### Current layout

- `llvm/`
  - `src/` upstream LLVM source snapshots or extracted trees
  - `manifests/` metadata for bootstrap/download rules
- `civetweb/`
  - `include/` public headers
  - `src/` pinned source tree
  - `manifests/` metadata for native build rules

### Design intent

- Keep Kinal source and third-party assets in separate repositories.
- Allow `Kinal` to discover this repository through a sibling directory:
  - `../Kinal-ThirdParty`
- Keep heavyweight archives and prebuilt toolchains out of the main language repository.

### Generated artifacts

This repository should prefer:

- upstream source trees
- headers
- manifests and version pins

It should not permanently track machine-local prebuilt binaries as part of the repository layout.

If build scripts need downloaded toolchains or generated native artifacts, they should go into ignored
directories such as:

- `.cache/`
- `artifacts/`
- tool-specific working directories created outside Git

### Notes

- This repository is for external code and binary assets only.
- It should prefer source snapshots and manifests over checked-in prebuilt outputs.
- Kinal-owned applications, runtime logic, and tools belong in the `Kinal` repository.
- If a dependency becomes large, versioned, and independently maintained, keeping it here is still preferable to mixing it into the main repository history.
