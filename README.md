# ulc

A canvas editor you embed in your own app: a whiteboard today, a design tool next. It runs in the browser, has no backend of its own, and is built so people and AI can edit the same board.

This repository holds **built releases only** (JavaScript packages and fonts). ulc is proprietary and closed source; see [LICENSE](LICENSE). Early software: versions below 1.0 may change between minor releases.

## What it does

- **Whiteboard**: select, move, resize, rotate; rectangle, diamond, ellipse, line, arrow, freehand, text, sticky notes, images; groups, layers, lock, align and distribute; snapping, grid, find, command palette; eraser; touch pan and pinch.
- **Connectors**: arrows glue to shapes and follow them, straight, elbow (steers around other shapes) or curved.
- **Looks**: stroke styles, fills (solid, hachure, cross-hatch), sketchy drawing, rounded corners, arrowheads, dark theme, text with weights, spacing and alignment, inside shapes too.
- **Design mode**: nested frames, auto layout, constraints, styles, components, multi-frame export, prototype links and preview.
- **Export and files**: PNG, SVG (optionally with the scene embedded), PDF, clipboard, scene files and reusable libraries.
- **People and AI together**: every change is a command with an attribution (user, remote, ai, system), so undo, collaboration and AI edits share one history and merge rules. The `@ulc/mcp-schema` package defines one tool per command, validates tool calls, and is what an MCP server uses.
- **Realtime hooks**: remote cursors, laser pointer and follow mode are inputs and outputs of the editor; the editor itself has no network, storage or login code, so you keep those.
- **Fast**: only visible elements are drawn; 10,000 elements pan and zoom smoothly on a laptop.
- **Own fonts**: `ulc Hand` (handwriting) and `ulc Mono` (coding font); see [FONTS.md](FONTS.md).

## Install

Each release has four packages. Install the ones you need **in one command**, from the release files (no account or token needed). Replace `0.1.0` with the version you want (see [Releases](../../releases)):

```sh
V=0.1.0
B=https://github.com/ulab24/ulc/releases/download/ulc-$V
npm install $B/ulc-engine-$V.tgz $B/ulc-renderer-$V.tgz $B/ulc-editor-$V.tgz
# a server that checks AI tool calls also needs:  $B/ulc-mcp-schema-$V.tgz
```

| Package | What |
|---|---|
| `@ulc/engine` | scene model, commands, history, merge rules (no DOM; runs headless) |
| `@ulc/renderer` | Canvas 2D drawing, export, fonts |
| `@ulc/editor` | `createEditor`, the API your app calls |
| `@ulc/mcp-schema` | command and MCP tool definitions, validation of tool calls |

ES modules, ES2022, no globals. Each release also has `install.txt`, `checksums.txt` and its signature.

## Use

```ts
import { createEditor } from '@ulc/editor';

const editor = createEditor(document.getElementById('stage')!, {
  fonts: [{ family: 'ulc Hand', source: '/fonts/ulc-hand.woff2', weight: '400' }],
});

editor.onChange((e) => save(e.attribution, editor.getElements())); // e.attribution.origin: user | remote | ai | system
editor.loadScene(savedElements);                                   // validated like any untrusted input
```

Your app owns login, storage, sharing and sync. Send local changes to your server; pass changes from others to `editor.applyRemoteChanges`. The editor never decides permissions: `setReadOnly` is a hint for the UI, and your server stays the authority.

## Verify a download

Releases carry `checksums.txt` signed with the ulab24 release key (`checksums.txt.asc`). The public key is [ulab24-release-signing-key.asc](ulab24-release-signing-key.asc).

```sh
gpg --import ulab24-release-signing-key.asc
gpg --verify checksums.txt.asc checksums.txt
sha256sum -c checksums.txt          # shasum -a 256 -c checksums.txt on macOS
```

## Licence and support

Proprietary. No licence is granted to use, copy or distribute the packages or fonts except under a written agreement with ulab24, or, for the fonts, the [ulab24 Font Licence](licenses/ulab24-Font-Licence-1.0.txt). Questions and agreements: udara@ulab24.com. Bug reports are welcome as issues here; the source is not published, so there are no pull requests.
