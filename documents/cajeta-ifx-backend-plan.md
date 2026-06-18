# cajeta-ifx-backend — Plan

Derived from `cajeta-ifx-backend-spec.md`. Outline numbering `1` / `a` / `1`.
Checkbox legend: `[x]` done · `[~]` partial · `[ ]` not started.

## 1. Melt manifest
The curated BOM listing the per-OS backends + pinned versions.

   **TDD**
   a. [ ] Manifest validates against the build tool's melt schema.
   b. [ ] Importing the melt with `"ifx-backend": "*"` resolves the constraints.

   **Deliverables**
   a. [ ] `cajeta.json` `melt` block with all five backends + a coherent version set.

   **Acceptance Criteria**
   a. [ ] A consumer adds one line and the backend set resolves.

## 2. Target-conditional selection
Link only the backend matching the active build target.

   **TDD**
   a. [ ] Building `--target=windows` resolves only `ifx.windows`; `=linux` only `ifx.linux`; etc.
   b. [ ] A backend that cannot compile for the target is not linked.

   **Deliverables**
   a. [ ] Target → member mapping honored by the build tool (or documented escape hatch:
      depend on a specific backend directly).

   **Acceptance Criteria**
   a. [ ] Per-target builds each link exactly their OS backend with no app changes.

## 3. Coherence & docs
   **TDD**
   a. [ ] Version bumps to one backend do not force re-release of the others (independent cadence).

   **Deliverables**
   a. [ ] README mapping table; note headless builds omit the melt.

   **Acceptance Criteria**
   a. [ ] The "one line for the common app, nothing for headless" contract holds.

## Dependencies & sequencing
- Gated on the stdlib `cajeta.ifx` contract and the five backend libraries existing.
- Build-tool target-conditional dependency resolution is the one mechanism this relies on; if not
  yet present, document direct per-backend dependence as the interim.
