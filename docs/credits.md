# Credits and Acknowledgements

Back to the [README](../README.md). License texts are in [LICENSE](../LICENSE) and [THIRD_PARTY_LICENSES](../THIRD_PARTY_LICENSES).

This project would not exist without the decades of work by the Smalltalk
community. The VM's interpreter, object memory, and primitives are a clean
C++ reimplementation of the architecture defined by the Pharo and Squeak
projects.

**Pharo and predecessors:**
- [Pharo](https://pharo.org) — the Smalltalk environment this VM executes
  (MIT; Copyright 2008-2019 The Pharo Project, Inria)
- [OpenSmalltalk-VM](https://github.com/OpenSmalltalk/opensmalltalk-vm) —
  the reference VM from which VMMaker-generated plugin code and headers
  are taken (MIT; Copyright 2013 3D Immersive Collaboration Consulting, LLC)
- [Squeak](http://squeak.org) — the original open source Smalltalk from which
  Pharo descends (MIT; Copyright 1996-2008 Viewpoints Research Institute,
  Apple Inc.)

**VMMaker-generated plugins included in this repo:**
- BalloonEnginePlugin (B2DPlugin.c) — vector graphics
- DSAPlugin (DSAPrims.c) — digital signature algorithm
- JPEGReaderPlugin, JPEGReadWriter2Plugin — JPEG codec wrappers
- SqueakSSLPlugin (SqueakSSL.c, sqMacSSL.c by Andreas Raab and Tobias Pape)

**Bundled libraries:**
- [Independent JPEG Group](http://www.ijg.org) libjpeg 6b by Thomas G. Lane
  (IJG license) — bundled in src/vm/plugins/jpeg/

**Statically linked libraries (cross-compiled as xcframeworks):**
- [libffi](https://github.com/libffi/libffi) 3.5.2 — Foreign Function Interface (MIT)
- [SDL2](https://www.libsdl.org) 2.26.5 — Simple DirectMedia Layer (zlib)
- [cairo](https://cairographics.org) 1.18.2 — 2D graphics (LGPL-2.1 / MPL-1.1)
- [FreeType](https://freetype.org) 2.13.3 — font rendering (FTL)
- [pixman](https://cairographics.org) 0.43.4 — pixel manipulation (MIT)
- [HarfBuzz](https://github.com/harfbuzz/harfbuzz) 10.1.0 — text shaping (MIT)
- [libpng](http://libpng.org) 1.6.43 — PNG support (libpng license)
- [OpenSSL](https://www.openssl.org) 3.4.0 — cryptography (Apache-2.0)
- [libssh2](https://www.libssh2.org) 1.11.1 — SSH client (BSD-3-Clause)
- [libgit2](https://libgit2.org) 1.8.4 — Git library (GPL-2.0 with linking exception)

This software is based in part on the work of the Independent JPEG Group.
