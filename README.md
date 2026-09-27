# Media EQ Panel for Omarchy

An MPRIS now-playing bar widget + control panel for Omarchy's Quickshell
desktop. Works with Spotify and any player exposing the standard Linux
MPRIS interface. No polling scripts, no `playerctl` dependency.

Cloned from Omarchy's stock `omarchy.media` widget, with two additions
the stock widget lacks:

- **Player volume slider** in the popup, driving the player's own MPRIS
  volume (independent of system/master volume).
- **Animated 28-bar equalizer** in the popup — purely aesthetic, dances
  while music plays, freezes while paused.

Everything else is stock behavior: scrolling `track · artist` label,
left-click = play/pause, middle-click = next, scroll = prev/next,
right-click = control panel with album art, ⏮ ▶/⏭ buttons, and
multi-source switching.

## Install

```bash
omarchy plugin add https://github.com/<you>/omarchy-media-eq.git --enable
```

Enabling replaces the built-in `omarchy.media` widget (same mechanism as
`omarchy plugin clone`). Add it to the bar if it isn't placed automatically:

```bash
omarchy bar move justin.media --section center
```

## Usage

- The widget appears in the bar whenever a player exposes track metadata.
- Right-click the track label to open the panel with controls, volume,
  and equalizer.

## Tweaks

In `BarWidget.qml`, `eqRow` block:

| Setting            | Effect                    |
|--------------------|---------------------------|
| bar count (`28`)   | number of EQ bars         |
| `interval: 130`    | EQ animation speed (ms)   |
| `height: ... (36)` | EQ strip height           |
| `maxLabelWidth`    | scrolling label max width |

In the volume row: `step: 0.05` controls slider granularity.

## Validate

```bash
omarchy plugin validate /path/to/justin.media
```

## Credits

Derived from Omarchy's first-party `omarchy.media` plugin
([basecamp/omarchy](https://github.com/basecamp/omarchy)). Service logic
(`Service.qml`, `MediaModel.js`) is unchanged stock code; the volume
slider follows the `PanelSlider` pattern from Omarchy's audio panel.
