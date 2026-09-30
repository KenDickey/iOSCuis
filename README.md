# iospharo

A Pharo Smalltalk VM for iOS and macOS, written as a clean C++ interpreter.

## Overview

iospharo runs standard Pharo 13 and Pharo 14 images on iOS devices and Mac
(via Catalyst). It is a from-scratch interpreter implementation — not a port
of the Cog JIT VM — with full support for the Sista V1 bytecode set, FFI with
callbacks, and the standard Pharo test suite.

**Note:** Pharo 12 and earlier use a different class table layout that the VM
does not yet handle.

## Status

**VM core (solid):**
- **99.90% test pass rate** on Mac Catalyst (13,040 / 13,053)
- **99.55% test pass rate** on iOS Simulator
- FFI with callbacks (sigsetjmp/siglongjmp)
- All standard VM plugins built-in (B2D, JPEG, DSA, SSL, etc.)
- Third-party libraries: cairo, freetype, harfbuzz, pixman, libpng, OpenSSL, libssh2, libgit2

**GUI (working):**
- Metal rendering pipeline — Pharo desktop renders correctly
- Menu bar, world menu, and context menus all functional
- Touch-to-mouse event translation (tap, long-press, two-finger, pinch, drag)
- Hardware keyboard support with modifier keys
- Image library with download, import, and catalog management

## Install from the App Store

Available for iPad, iPhone, and Mac:

[Download on the App Store](https://apps.apple.com/us/app/pharosmalltalk/id6759073615)

**Requirements:**
- iPad (5th gen / 2017 or newer) or iPhone (6s / 2015 or newer) or Mac (Apple Silicon or Intel)
- iOS / iPadOS 15.0 or later, macOS 14.0 or later
- ~150 MB free storage (app + image + sources)

Pharo images are downloaded in-app (no separate download needed).

## Beta Testing (TestFlight)

There may be a newer pre-release version available via TestFlight:

1. Install **TestFlight** from the App Store (free, ~30 MB)
2. Open this invite link on your iPad or iPhone: [Join the Beta](https://testflight.apple.com/join/kGmPQFr9)
3. Tap "Accept" then "Install" — the app appears on your home screen

TestFlight builds expire after 90 days but auto-update when new builds
are published.

## Building

Building needs Xcode 15+, CMake, and a few Homebrew tools. The short version:

```bash
scripts/build-libffi.sh
scripts/build-sdl2.sh
scripts/build-third-party.sh
open iospharo.xcodeproj
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
and Squeak projects, and iospharo bundles or links many upstream libraries. The
full list with versions and licenses is in [docs/credits.md](docs/credits.md).

This software is based in part on the work of the Independent JPEG Group.
