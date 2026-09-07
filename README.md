# Scelith

**Bringing PSP homebrew to the PlayStation 2 without rewriting the whole project.**

Scelith is an experimental compatibility layer for running PSP homebrew source code on the PS2.

The idea is pretty simple: keep the original project as intact as possible and handle the platform differences outside of it.

Instead of going through a codebase replacing PSP-specific code by hand, Scelith provides compatible implementations, build-time adaptations and a PS2 backend for the parts that need it.

It's not an emulator, and it's not a binary converter.
You need the source code.

## How it works

A PSP project normally expects the PSP environment, its libraries and its hardware-specific behavior.

Scelith sits in the middle and adapts that environment to the PS2.

```text
PSP homebrew source
        │
        ▼
   Scelith build
        │
        ├── compatibility layer
        ├── source adaptations
        ├── platform replacements
        └── PS2-specific backend
        │
        ▼
      PS2 ELF
```

Some adaptations are done through a **shadow build**.

That means Scelith can modify temporary copies of files during the build without touching the original project.

The original source stays original.

## What Scelith handles

The project is gradually implementing the parts PSP homebrew usually depends on, including:

* graphics
* input
* filesystem / I/O
* audio
* threading and synchronization
* display
* memory-related behavior
* PSP-specific runtime assumptions

Under the hood, PSP APIs can be mapped to PS2 equivalents where possible, while other features need their own implementation.

Graphics are one of the bigger parts of the project, especially things like textures, blending, depth, viewport state and other GU behavior that doesn't map directly to the PS2 GS.

## Current state

Scelith is still experimental.

It can already build and run fairly complex PSP code on the PS2, but compatibility is nowhere near complete yet.

Some projects may get surprisingly far, while others may hit an unimplemented API almost immediately.

Right now the focus is less on making one specific game work through hacks and more on fixing things inside Scelith so the same fix can help other homebrew too.

If something has to be adapted for the PS2, the goal is to put that logic here instead of modifying the original project.

## What this project is not

Scelith does **not**:

* run PSP binaries directly
* emulate a PSP
* convert retail PSP games to PS2
* magically make every PSP project work

It's meant for **source-based homebrew ports**.

## Goal

The long-term goal is to get as close as possible to this:

```text
existing PSP homebrew
        ↓
      Scelith
        ↓
       PS2
```

with little or no manual modification to the original source.

There will always be projects that depend heavily on PSP-specific hardware or behavior, so perfect compatibility with everything isn't realistic.

But the more compatibility that can live inside Scelith, the less work each individual port should need.

## Status

Very much a work in progress.

Expect missing APIs, broken rendering, weird edge cases and things that simply don't work yet.

That's part of the project.

## License

See the repository license for details.

---

Scelith is an independent homebrew project and is not affiliated with or endorsed by Sony Interactive Entertainment.
