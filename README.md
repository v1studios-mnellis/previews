# Previews

A pane beside your terminal for the images your coding agent draws — and a
one-key way to send the annotated feedback back to the agent.

![Previews](preview.png)

## What it does

- **Watches `<project>/.herdr-previews/`** — the folder of the terminal the
  pane is split beside. A PNG an agent saves there shows up within a few
  seconds, with a toast and a sound.
- **A card list.** `alt-p` splits the pane in beside the terminal and shows
  cards grouped by file stem (`homepage-v1.png`, `homepage-v2.png` →
  `homepage`), newest group first, the 40 newest images overall.
- **Status per image**: `new`, `reviewed` (once opened), `approved`.
- **Pop-out viewer**: the image at its real aspect ratio, zoom and pan, a
  numbered pin wherever you click, a pen and a circle tool for drawings, a note
  on every pin and every drawing, and `Compare` to put an older draft beside
  the current one.
- **Send notes** types the feedback into the space's agent through `hc send` —
  `Feedback on draft: <path>` plus one line per pin — and `Approve` adds
  `Approved: <path>`. Notes live next to the images in `notes.json`.
- **Works in a space on another machine**: images are copied over ssh, notes are
  written with `exec`.

## Keys

| Key | Does |
|---|---|
| `alt-p` | open the previews pane beside the terminal |
| `j` / `k` | move between cards |
| `x` `x` | delete the image (armed; press again) |
| `Esc` | back to the terminal |
| `[` / `]` | previous / next draft in the pop-out |

## Install

```sh
cp -r mods/previews ~/.config/herdr-app/mods/previews
# merge keys.json into ~/.config/herdr-app/keys.json
herdr-app check ~/.config/herdr-app/mods/previews
```

No layout edit: the pane opens with `alt-p` wherever you are, and closes like
any pane.

**Teach your agent the convention**: paste `mods/previews/agent-snippet.md` into
the project's `AGENTS.md`, so captures land in `.herdr-previews/<target>-vN.png`
and the pane picks them up by itself.

## Notes

- The project is the sibling terminal's working directory, not the space
  folder.
- Shown images are copied into the mod's own `.cache/`; the originals are never
  modified.
- It runs `find`, `rm`, `sh`/`ssh`/`base64`/`mv` (remote copies and writes) and
  `hc send`. Nothing else touches the network.

`RECIPE.md` is the full build brief — every dimension, colour, state and
command.

Part of [herdr-mods](https://github.com/v1studios-mnellis/herdr-mods), the
working repo for all of my herdr-app mods.
