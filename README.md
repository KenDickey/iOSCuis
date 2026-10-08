# iOSCuis

A Cuis Smalltalk VM for iOS and macOS, written as a clean C++ interpreter.

## Overview

This fork was made to change image invocation in src/Interpreter.cpp for Cuis Smalltalk internals, which differ from Pharo.

Original comment reads:

iospharo runs standard Pharo 13 and Pharo 14 images on iOS devices and Mac
(via Catalyst). It is a from-scratch interpreter implementation — not a port
of the Cog JIT VM — with full support for the Sista V1 bytecode set, FFI with
callbacks, and the standard Pharo test suite.

See 
- https://github.com/avwohl/iospharo
- https://cuis.st

## Status

In Progress (Nothing here to see yet!)

**Requirements:**
- iPad (5th gen / 2017 or newer) or iPhone (6s / 2015 or newer) or Mac (Apple Silicon or Intel)
- iOS / iPadOS 15.0 or later, macOS 14.0 or later
- ~150 MB free storage (app + image + sources)

## Building

Building needs Xcode 15+, CMake, and a few Homebrew tools. The short version:

```bash
scripts/build-libffi.sh
scripts/build-sdl2.sh
scripts/build-third-party.sh
open ioscuis.xcodeproj
```

The full steps, code signing, and the headless Mac development build are in
[docs/building.md](docs/building.md).

## Documentation

- [Building](docs/building.md) - prerequisites, xcframework builds, Xcode app, headless dev build
- [Architecture](docs/architecture.md) - project structure, app/VM layers, startup patches, VM configuration
- [Programmer's overview](docs/programmers-overview.md) - deeper tour of the VM internals
- [Startup system](docs/startup-system.md) - the Smalltalk patches applied on every launch
- [Known issues](docs/known-issues.md) - current bugs and limitations
- [Test results](docs/test-results.md) - Pharo test suite results
- [Standalone apps](docs/building-standalone-apps.md) - packaging a Pharo image as its own app
- [Credits](docs/credits.md) - upstream projects, bundled and linked libraries

## Related

Other repos in this collection:

- [smalltalk80-2026](https://github.com/avwohl/smalltalk80-2026) — C++17 virtual machine for Smalltalk-80 on macOS, Mac Catalyst, Linux, and Windows. It boots the 1983 Xerox virtual image to the desktop.
- [validate_smalltalk_image](https://github.com/avwohl/validate_smalltalk_image) — Standalone validator and export tool for Spur-format Smalltalk images. It checks the heap, and it writes SHA-256 manifests and reference graphs.
- [pharo-headless-test](https://github.com/avwohl/pharo-headless-test) — Headless test runner for Pharo Smalltalk with a fake GUI. It clicks menus, takes screenshots, and runs the SUnit suite without a display. This project extracted it and includes it as a submodule at `scripts/pharo-headless-test/`.
- [soogle](https://github.com/avwohl/soogle) — Search engine for Smalltalk source code. It indexes packages and labels each one with its dialect, such as Pharo, Squeak, or GemStone.
- [claude-skills](https://github.com/avwohl/claude-skills) — Collection of open source skills for Claude Code. Each skill is a Markdown file in `.claude/skills/` that holds reusable knowledge and algorithms.

## License

MIT — see [LICENSE](LICENSE) and [THIRD_PARTY_LICENSES](THIRD_PARTY_LICENSES).

## Credits

iospharo is a clean C++ reimplementation of the architecture defined by the Pharo
Squeak, and Cuis projects, and iospharo bundles or links many upstream libraries. The
full list with versions and licenses is in [docs/credits.md](docs/credits.md).

This software is based in part on the work of the Independent JPEG Group.
