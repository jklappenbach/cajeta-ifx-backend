# cajeta-ifx-backend — Spec

**Status:** Draft. Requirements for the `ifx-backend` melt — the required selector that maps a
build target to its `ifx` window/input/audio backend(s).

## 1. Overview & why
`ifx` (the portable contract) is stdlib and always present, but it carries no OS code. To get real
window/input/audio an app must include a backend; rather than make developers hand-pick per OS,
`ifx-backend` is a **melt** (BOM) that resolves the right backend(s) for the active build target
from one dependency line. This both keeps the per-OS backends independently versioned (vendor
churn) and restores SDL-style one-line ergonomics. Umbrella design: the cajeta repo's
`documents/cajeta-gfx/cajeta-gfx-spec.md` §9.3.

## 2. Capabilities
- **Target → backend resolution.** Windows→`ifx.windows`, Linux→`ifx.linux`, macOS→`ifx.macos`,
  iOS→`ifx.ios`, Android→`ifx.android`. A backend that cannot compile for a target is not linked
  (selection is target-conditional, not "link all").
- **Coherent version pinning.** One curated set of backend versions consumers inherit.
- **Within-OS variants stay runtime.** e.g. Wayland vs X11 is chosen by the linux backend's
  `probe()`/`priority()` at launch, not by the melt.

## 3. Goals
- One required dependency line lights up the platform for the common app.
- Per-OS backends remain independently versioned and published.
- Headless builds need *not* include the melt (stdlib `null` floor covers them).

## 4. Non-goals
- No code — a melt ships only a manifest.
- No runtime dispatch logic (that is `ifx`'s `BackendRegistry`).
- No harness/codec selection (separate optional libraries).

## 5. References
- Umbrella: `cajeta-gfx-spec.md` §9.3 (packaging) + §9.4 (binding model).
- Members: `cajeta-ifx-{windows,linux,macos,ios,android}`.
- Contract: stdlib `cajeta.ifx`.
