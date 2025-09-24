Betonquest Dialog Visualiser

Visual desktop editor for creating, validating, simulating, importing and exporting BetonQuest conversations. Built as a personal learning project with AI collaboration.

What is BetonQuest (in short)

[BetonQuest] is a popular quest & dialogue plugin for Minecraft. Conversations are stored in YAML and typically contain:

A conversations: root with one or more named conversations (e.g., santa).

Two “folders” of blocks inside each conversation:

NPC_options: — NPC lines.

player_options: — player replies.

first: — one or more starting block IDs.

Pointers that connect blocks:

NPC blocks must point to player blocks.

Player blocks must point to NPC blocks.

A block may have no pointers → that simply ends the chat (valid and intentional).

References to shared conditions, events and objectives, usually defined in separate YAML files and referenced by ID.

Manually keeping this consistent can be error-prone; that’s what this tool aims to help with.

What this program is supposed to do

Visual graph editor for conversations:

Drag blocks (NPC / Player), draw pointers, edit texts and IDs.

Strong validation of pointers (existence + correct target type).

Live lint panel with clickable errors.

Simulation:

Click through a conversation from first, switch branches like in game.

Optional “console” to show which events would fire and which conditions passed.

Cross-file awareness:

Load and manage conditions.yml, events.yml, objectives.yml.

Palette to insert existing IDs into blocks with one click.

Validation that every referenced condition/event/objective exists.

I/O:

Export valid BetonQuest YAML.

Export a custom JSON format for round-trip editing.

Import existing YAML (round-trip friendly).

Quality of life:

Search, quick jump to blocks, ID refactoring with safe propagation, keyboard shortcuts.

Why this stack

This is also a learning project I’m building together with AI (pair-programming style). The stack is chosen to maximize velocity and quality:

TypeScript — safer data modeling, great tooling and refactors.

React — fast, component-based UI.

Electron — ships as a desktop app with file system access.

React Flow — battle-tested node/edge canvas for the editor.

Vite — fast dev server and builds.

yaml — reading/writing YAML cleanly.

Zustand — simple app state.

Zod — schema validation for imports and internal models.

Development plan (phases)
Phase 0 — Repo & CI (✅ done)

GitHub repo, MIT license, .editorconfig, .gitattributes, .gitignore.

GitHub Actions workflow to build Windows artifacts with electron-builder.

Issue & PR templates.

Basic rules for main branch (PRs required).

Phase 1 — Skeleton app

Electron main + preload (secure bridge).

React + Vite renderer.

“Hello” window runs with npm run dev.

Phase 2 — Shell UI

Tabbed layout: Canvas, Code, Simulator (placeholders).

Global state wiring (Zustand).

Phase 3 — Graph editing (no I/O yet)

Add NPC/Player blocks on canvas.

Draw pointers with drag-to-connect.

Enforce pointer direction (NPC → Player, Player → NPC).

Inspector to edit id and text.

Export preview into Code tab (not saved to disk yet).

Phase 4 — Model, normalization, validation

Normalize lists ("a,b" → ["a","b"]) for pointers, conditions, events, first.

Validate:

Every pointer exists and targets the correct category.

All first IDs exist.

Problems panel with deep links to blocks.

Phase 5 — Three windows “for real”

Canvas fully editable.

Code shows generated YAML (read-only, copy button).

Simulator lets you click through from first; end on blocks with no pointers.

Phase 6 — Conditions / Events / Objectives

Open project folder; load conditions.yml, events.yml, objectives.yml.

Palette to insert IDs into the active block.

Cross-file validation: every referenced ID exists.

(Optional) Create/rename/delete items with safe reference propagation.

Phase 7 — Simulator + Console

Player context (tags, simple variables) to influence conditions.

Console log of “would run” events and condition checks.

Phase 8 — Export

Save BetonQuest YAML to disk (valid & readable).

Save custom JSON (versioned) for lossless round-trip.

Phase 9 — Import

Import existing conversations into the canvas.

Round-trip test: Import → Export → equivalent result.

Status

Active WIP. I’m developing this incrementally and using AI to assist with design, scaffolding, refactors, and tests. Expect frequent changes until the core workflow (Phases 1–5) is settled.

Contributing

Ideas, bug reports and small PRs welcome. Please:

Open an issue with the included templates.

Keep conversations small and focused (one change per PR).

Prefer clear IDs (ASCII, no spaces) for block identifiers.

License

MIT. See LICENSE.
