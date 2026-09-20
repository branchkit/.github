<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/branchkit/.github/main/profile/assets/branchkit-lockup-dark.png">
    <img src="https://raw.githubusercontent.com/branchkit/.github/main/profile/assets/branchkit-lockup-light.png" alt="BranchKit" width="320">
  </picture>
</p>

<p align="center">
  A runtime for plugins that control a computer.
</p>

<p align="center">
  <strong>Pre-launch.</strong> The application is in private development and is
  not yet publicly released. The SDKs and tooling below are published and usable
  today.
</p>

---

## What this is

The platform itself does nothing a user would notice. It loads plugins,
confines them, tracks what is true right now — which application has focus,
which mode is active, what the user is looking at — and routes commands to
whichever plugin claims them.

All behavior lives in plugins: dictation and voice commands, window management,
keyboard remapping, browser control, system state. A plugin is a process
speaking JSON-RPC over stdio, so it can be written in anything; three SDKs are
maintained at parity against a shared conformance suite. Nothing
plugin-specific is allowed into the core.

Plugins run confined. A plugin declares what it needs in a manifest — commands,
filesystem scope, network hosts — and the platform enforces exactly that: no
home directory, no other plugin's data, no unlisted host. Every grant is a
visible, revocable record. A plugin that cannot be sandboxed does not start,
and first-party plugins get no exemption from any of it.

Everything runs on the machine. Speech recognition, matching, and routing are
local; no input data leaves the device.

**Platforms.** macOS today. Linux and Windows are in active development and not
yet usable end to end.

## What it ships with

The app arrives as a working voice-controlled desktop. That is entirely the
bundled plugins' doing — the runtime contributes none of it.

- **Dictation** — hold a key, speak, release; text appears at the cursor,
  transcribed on-device.
- **Voice commands** — a separate hold for commands, matched live against what
  is eligible in the current context rather than against everything at once.
- **Window control** — snapping, moving between spaces and displays, mission
  control.
- **Browser control** — hint badges on any page, so links, buttons and fields
  can be named aloud instead of clicked.
- **Keyboard** — a global hotkey registry and remapping, so any command can be
  reached by a key instead of a word.
- **System** — launching and switching applications, audio devices and volume,
  system settings.
- **Scripting** — user Lua scripts, for automating something without writing
  and installing a plugin.
- **Spoken feedback** — errors, the mode you are in, and the choices it offers,
  reported aloud rather than only on screen.

Dozens of spoken commands work the moment it starts.

None of it is privileged. Every bundled plugin is loaded, sandboxed, granted
and routed exactly like one you write yourself — same contract, same permission
records, same revocation. Replacing one with your own is a supported thing to
do, not a fork.

## Write a plugin

```bash
go install github.com/branchkit/branchkit-cli@latest
branchkit-cli dev init --template go   # or: --template ts | --template py
```

| Language | Install | Repository |
|---|---|---|
| Go | `go get github.com/branchkit/plugin-sdk-go` | [plugin-sdk-go](https://github.com/branchkit/plugin-sdk-go) |
| Python | `pip install branchkit` | [plugin-sdk-py](https://github.com/branchkit/plugin-sdk-py) |
| TypeScript | `bun add github:branchkit/plugin-sdk-ts` | [plugin-sdk-ts](https://github.com/branchkit/plugin-sdk-ts) |

## Repositories

**Plugin SDKs**

| | |
|---|---|
| [plugin-sdk-go](https://github.com/branchkit/plugin-sdk-go) | Go SDK |
| [plugin-sdk-ts](https://github.com/branchkit/plugin-sdk-ts) | TypeScript SDK |
| [plugin-sdk-py](https://github.com/branchkit/plugin-sdk-py) | Python SDK, standard library only |

**Tooling**

| | |
|---|---|
| [branchkit-cli](https://github.com/branchkit/branchkit-cli) | Install, inspect, and scaffold plugins |
| [branchkit-gen](https://github.com/branchkit/branchkit-gen) | Generate typed action parameters from a manifest |
| [registry](https://github.com/branchkit/registry) | Public plugin registry |

**Worked examples** —
[snippets](https://github.com/branchkit/branchkit-plugin-snippets) is the
teaching plugin: speak a name, get its expansion typed, in about as little code
as a real plugin takes. The starter templates —
[Go](https://github.com/branchkit/branchkit-plugin-helloworld-go) ·
[TypeScript](https://github.com/branchkit/branchkit-plugin-helloworld-ts) ·
[Python](https://github.com/branchkit/branchkit-plugin-helloworld-py) — are
exact mirrors of what `dev init` generates. Several of the bundled plugins are
MIT and public too; they are listed on this page's repository index.

**Other extension points.** Input sources and stream transforms — audio
capture, speech recognition, device and system event monitors — are pipeline
stages rather than plugins, written in Rust against
[stage-sdk](https://github.com/branchkit/stage-sdk).

## Status

The application, the runtime, and several of the bundled plugins are closed
source and in private development. The SDKs, tooling, contracts, and the
example plugins are MIT and public.

The plugin contract is stable enough to build against but is not yet versioned
for compatibility. It changes without deprecation cycles until the first
release.

## Contributing

Issues and questions are welcome on any public repository. Pull requests may
sit until the first release; if you are planning more than a small fix, open an
issue first so the work is not wasted.

Template repositories (`branchkit-plugin-helloworld-*`) are generated — changes
belong in [branchkit-cli](https://github.com/branchkit/branchkit-cli).
