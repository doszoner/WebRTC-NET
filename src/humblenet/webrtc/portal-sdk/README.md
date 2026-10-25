# Portal SDK overlay v2

This directory carries the exact SDK source patch, public header and locked
offline build recipe. It does not by itself enable portal send capability 0x08.
V2 measures actual retained payload/records separately from the source-proven
reservation potential, including peer restart. The wrapper must pass prospective
peer/global admission, actual proxy send/drain/close controls and review before
advertising that capability.

Supply the pinned 6422.8505a9.224 SDK and the five original `.cc` files from
WebRTC revision `8505a9838ea91c66c96c173d30cd66f9dbcc7548`, preserving their
relative paths in `source-root`. Their SHA256 values are in `inputs.lock.json`.
The recipe verifies those sources, affected original SDK headers, static
libraries, compiler, archiver, patch and public header before writing output.
It does not fetch, sync, configure a foreign SDK, or modify a gitlink.

```sh
python3 build.py --sdk-root /path/to/pinned-sdk --source-root /path/to/pinned-sources \
  --output-dir /path/to/fresh-output --cxx /path/to/pinned-clang++ --ar /path/to/pinned-ar
```

Output contains a full matching include/lib SDK plus the compiled overlay,
commands and hashes. Five uniquely named archive members are replaced in a copy;
unchanged members retain the supplied base provenance. Build paths in rebuilt
objects are normalized. This is a new mixed SDK identity, not reproduction of
the original upstream compiler/GN build. Select it explicitly using existing
`HUMBLENET_EXTERNAL_WEBRTC_PROVIDER_ROOT`, `_INCLUDE_DIR` and `_LIB_DIR` CMake
inputs, with a fresh output directory outside the source tree. There is no
automatic SDK build or download target.

Controls and runtime evidence belong outside this directory. Full send
qualification additionally requires prospective payload/record bounds, whole
accepted/backpressure/closed propagation, actual drain/resumption and safe
callback/socket destruction. Snapshot/build success alone does not qualify it.
The original v1 candidate is retained separately in recovery evidence; this
product selects v2.
