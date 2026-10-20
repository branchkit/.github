<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/branchkit/.github/main/profile/assets/branchkit-lockup-dark.png">
    <img src="https://raw.githubusercontent.com/branchkit/.github/main/profile/assets/branchkit-lockup-light.png" alt="BranchKit" width="320">
  </picture>
</p>

<p align="center">
  An accessibility plugin platform for the desktop.
</p>

<p align="center">
  <strong>Pre-launch.</strong> The app is in private development and not yet
  released. The SDKs, tooling and the public plugins below are published and
  usable today.
</p>

---

## What it does

The app ships with plugins for:

- **Dictation.** Hold a key, speak, release: the text appears at the cursor,
  transcribed on the machine.
- **Commands.** Speak a command, or bind it to a key. What you say is matched
  against the commands that make sense in the current context, so a short word
  can mean the right thing.
- **Browser control.** A companion extension puts a short code word on every
  link, button and field on the page. Say it to click, type into, or move that
  tab to another window or desktop.
- **Any window's controls.** The same code words on the buttons, menus and
  switches of the app in front.
- **Windows.** Put any window at a position, on another screen or another
  desktop, without a pointer.
- **Keyboard and mouse.** Press keys, click and scroll, and every key has a
  name you can say.
- **Apps and audio.** Open or switch to any app by the name you call it;
  change volume and the devices you hear and speak through.
- **Spoken feedback.** What went wrong, the mode you are in and the choices it
  offers, said aloud as well as shown.
- **Scripts.** One file in Lua, JavaScript, TypeScript or Python for a command,
  an event handler or a timer, with no plugin to build or install.

Every one of these is an ordinary plugin. It is loaded, confined, granted and
routed exactly like one you write, so replacing one with your own is a
supported thing to do.

## How it works

The platform loads plugins, confines them, keeps track of what is true right
now (which app has focus, which mode is on, what is on screen) and routes each
command to the plugin that claims it. It has no behaviour of its own.

- **Any language.** A plugin is a process speaking JSON-RPC over stdio. SDKs
  for Go, TypeScript and Python are kept at parity by one conformance suite.
- **Confined.** A plugin's manifest declares what it needs: its commands, the
  folders it may read and write, the hosts it may reach. The platform enforces
  exactly that. Each grant is a visible record the person can turn off, and a
  plugin the platform cannot sandbox does not start. Bundled plugins get no
  exemption.
- **On the machine.** Speech recognition, matching and routing run locally,
  and the platform makes no network requests of its own. A plugin reaches only
  the hosts its manifest names and the person allows.
- **Every desktop.** Runs on macOS today. Linux and Windows are in active
  development and not yet usable end to end.

## Write a plugin

```bash
go install github.com/branchkit/branchkit-cli@latest
branchkit-cli dev init --name my-plugin --template go   # or: ts | py
```

| Language | Install | SDK |
|---|---|---|
| Go | `go get github.com/branchkit/plugin-sdk-go` | [plugin-sdk-go](https://github.com/branchkit/plugin-sdk-go) |
| Python | `pip install branchkit` | [plugin-sdk-py](https://github.com/branchkit/plugin-sdk-py) (standard library only) |
| TypeScript | `bun add github:branchkit/plugin-sdk-ts` | [plugin-sdk-ts](https://github.com/branchkit/plugin-sdk-ts) |

[snippets](https://github.com/branchkit/branchkit-plugin-snippets) is the
worked example: say "snippet shrug" and `¯\_(ツ)_/¯` is typed where you are
writing, in about as little code as a real plugin takes. The starter templates
([Go](https://github.com/branchkit/branchkit-plugin-helloworld-go) ·
[TypeScript](https://github.com/branchkit/branchkit-plugin-helloworld-ts) ·
[Python](https://github.com/branchkit/branchkit-plugin-helloworld-py)) are
exact copies of what `dev init` creates.

Input sources and stream transforms (audio capture, speech recognition,
device and system monitors) are pipeline stages rather than plugins, written
in Rust against [stage-sdk](https://github.com/branchkit/stage-sdk).

## Public repositories

**Plugins**, MIT and bundled with the app:

| | |
|---|---|
| [browser](https://github.com/branchkit/branchkit-plugin-browser) | Browser control, with the companion extension |
| [badges](https://github.com/branchkit/branchkit-plugin-badges) | A code word on each control of the window in front |
| [placement](https://github.com/branchkit/branchkit-plugin-placement) | Put any window at a position, screen or desktop |
| [keyboard](https://github.com/branchkit/branchkit-plugin-keyboard) | Presses keys, clicks and scrolls, and names every key |
| [apps](https://github.com/branchkit/branchkit-plugin-apps) | Open, switch to or start a new window of any app by name |
| [audio](https://github.com/branchkit/branchkit-plugin-audio) | Volume, mute, and audio devices by name |
| [announcements](https://github.com/branchkit/branchkit-plugin-announcements) | Says aloud what went wrong, the current mode and its choices |
| [scripts](https://github.com/branchkit/branchkit-plugin-scripts) | Single-file scripts in Lua, JavaScript, TypeScript or Python |
| [address](https://github.com/branchkit/branchkit-plugin-address) | Say a file's name to type its `@path` |
| [snippets](https://github.com/branchkit/branchkit-plugin-snippets) | Speak a name, type its expansion (the worked example) |

**SDKs and tooling**

| | |
|---|---|
| [plugin-sdk-go](https://github.com/branchkit/plugin-sdk-go) · [plugin-sdk-ts](https://github.com/branchkit/plugin-sdk-ts) · [plugin-sdk-py](https://github.com/branchkit/plugin-sdk-py) | Plugin SDKs |
| [stage-sdk](https://github.com/branchkit/stage-sdk) | Pipeline stages, in Rust |
| [branchkit-cli](https://github.com/branchkit/branchkit-cli) | Install, inspect and scaffold plugins |
| [branchkit-gen](https://github.com/branchkit/branchkit-gen) | Typed action parameters generated from a manifest |
| [registry](https://github.com/branchkit/registry) | The public plugin registry |

The app itself, the platform, the voice and tiling plugins and the browser
extension are closed source.

## Status

The plugin contract is stable enough to build against but is not yet versioned
for compatibility. It changes without deprecation cycles until the first
release.

## Contributing

Issues and questions are welcome on any public repository.

Each repository above except the registry is published from BranchKit's main
repository, which is private, so pull requests are not merged on GitHub. A
change that is accepted is applied in the main repository and comes back with
the next publish, with you as its author. If you plan more than a small fix,
open an issue first so the work is not wasted.

The starter templates are generated by `dev init`, so changes to them belong in
[branchkit-cli](https://github.com/branchkit/branchkit-cli).
