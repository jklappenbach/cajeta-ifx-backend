# cajeta-ifx-backend

`dev.cajeta.ifx-backend` — the **required melt** for **ifx**, the Cajeta interface-framework facade
for window / input / audio.

`ifx` (the portable contract) is **stdlib** — built into the toolchain, never declared. To actually
get a window, input, and audio, an app adds **this one melt**, which resolves the correct per-OS
backend(s) for the build target:

| Build target | Resolves |
|---|---|
| Windows | [`cajeta-ifx-windows`](https://github.com/jklappenbach/cajeta-ifx-windows) |
| Linux | [`cajeta-ifx-linux`](https://github.com/jklappenbach/cajeta-ifx-linux) (Wayland + X11) |
| macOS | [`cajeta-ifx-macos`](https://github.com/jklappenbach/cajeta-ifx-macos) |
| iOS | [`cajeta-ifx-ios`](https://github.com/jklappenbach/cajeta-ifx-ios) |
| Android | [`cajeta-ifx-android`](https://github.com/jklappenbach/cajeta-ifx-android) |

```jsonc
// an interactive app's entire platform dependency surface:
"capabilities": ["window", "input", "audio"],
"dependencies": { "ifx-backend": "1.0.*" }   // ifx itself is stdlib — implicit
```

A **headless** build (server / CI / offscreen render) adds **nothing** and rides the stdlib `null`
floor; for deterministic capture/replay testing add the optional
[`cajeta-ifx-harness`](https://github.com/jklappenbach/cajeta-ifx-harness) backend.

Why a melt and not one fat library: each OS backend is **versioned on its own vendor's cadence**
(an Apple deprecation bumps only the macOS backend); the melt restores the one-line convenience
without the monolith. Full rationale: the cajeta repo's `documents/cajeta-gfx/cajeta-gfx-spec.md`
§9.3.

## Status
**v0.1 — melt skeleton.** See [`documents/`](documents/) for the spec and plan.

## License
MIT © 2026 Julian Klappenbach. See [LICENSE](LICENSE).
