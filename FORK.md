# Fork maintenance

This fork tracks zetier/jxl-sys. Keep libjxl and its dependencies as upstream Git submodules; do not copy their sources into consuming repositories.

The application pins a full fork commit. For local debugging Cargo supports a temporary path override; do not commit machine-specific paths.

## Build changes

- Select target C++ linkage from Cargo TARGET, not the build host.
- Optional `static-cxx` links the target Linux libstdc++.a; the default retains upstream dynamic linkage. macOS uses system libc++.
- Build native codecs with Release optimizations even for debug Rust. Disable optional plugins, devtools and tcmalloc.
- On MSVC, CMake's runtime selection follows Cargo crt-static. Default Rust builds use the release DLL CRT; crt-static uses the static release CRT.
- Preserve upstream encoder code, package version, submodule revisions and licenses. No LTO or host-native instruction flags are enabled by these changes.

## Updating upstream

Fetch upstream, merge its release commit into this branch, inspect changes to build.rs, and update submodules recursively. Keep modifications restricted to build options and fork documentation/workflows. Test Windows MSVC, macOS and Linux GNU/musl, including real encode/decode, before updating the application's commit and lockfile. An upstream-supported equivalent should replace a local build patch.
