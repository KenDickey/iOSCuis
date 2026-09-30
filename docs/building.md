# Building iospharo

Back to the [README](../README.md).

## Prerequisites

Install these before building:

```bash
# Xcode command-line tools (includes clang, make, etc.)
xcode-select --install

# CMake (build system)
brew install cmake

# For third-party library builds (cairo, freetype, etc.)
brew install meson ninja pkg-config autoconf automake libtool
```

You also need:
- **Xcode 15+** (for the iOS/Mac Catalyst app)
- **A Pharo 13 or 14 image** — download from https://pharo.org/download

## Building

### Step 1: Build libffi and SDL2 xcframeworks

```bash
scripts/build-libffi.sh
scripts/build-sdl2.sh
```

This downloads, cross-compiles, and packages libffi (FFI/callbacks) and SDL2
(display driver) as xcframeworks for iOS device, simulator, Mac Catalyst, and
macOS. Takes about 10 minutes. The xcframeworks are gitignored due to size.

### Step 2: Build third-party libraries

Cairo, freetype, harfbuzz, pixman, libpng, OpenSSL, libssh2, and libgit2
are cross-compiled as static xcframeworks:

```bash
scripts/build-third-party.sh
```

This downloads source tarballs and builds for iOS device, Simulator, and Mac Catalyst.
Takes about 15 minutes on first run. Use `--no-crypto` to skip OpenSSL and libssh2
(libgit2 is always built for local repository support).

### Step 3: Build the app

```bash
open iospharo.xcodeproj
```

Select your target (iOS device, Simulator, or My Mac - Catalyst) and build.

Xcode has a "Check XCFramework Freshness" build phase that automatically runs
`scripts/build-xcframework.sh` whenever VM source files (`src/vm/`, `src/platform/`)
are newer than the xcframework. The first Xcode build will take several minutes
while it compiles the VM; subsequent builds are fast unless you change VM sources.

To manually rebuild the VM xcframework (e.g. after a git pull):

```bash
scripts/build-xcframework.sh
```

This produces `Frameworks/PharoVMCore.xcframework` with slices for iOS device
(arm64), iOS Simulator (arm64 + x86_64), and Mac Catalyst (arm64 + x86_64).

**Code signing (optional):** To deploy to a physical device or the App Store,
copy `Local.xcconfig.example` to `Local.xcconfig` and fill in your Apple
Developer Team ID. `Local.xcconfig` is gitignored.

### Quick development build (Mac only)

For faster iteration on VM internals. This builds a headless command-line binary
(not the iOS/Catalyst app). Requires Steps 1 and 2 above — the cmake build
links against the xcframeworks in `Frameworks/`.

```bash
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build

# Run headless with a Pharo image
./build/test_load_image /path/to/Pharo.image
```

