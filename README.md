# mz-omarchy-framework13-studiodisplay

Hyprland monitor configuration for running **Framework Laptop 13** with an **Apple Studio Display** on [Omarchy Linux](https://omarchy.org/).

## Hardware

| Component | Details |
|-----------|---------|
| Laptop | Framework Laptop 13 (latest model) |
| External Display | Apple Studio Display (27", 5K, 5120×2880) |
| Cable | Original Apple Thunderbolt cable |
| Display position | Studio Display on the **left**, Laptop on the **right** |

## The Problem

The Apple Studio Display uses internal display tiling to deliver its 5K resolution over Thunderbolt. This causes Hyprland to detect the display as **two separate monitors** (e.g. `DP-7` and `DP-8`) instead of one — resulting in three active screens instead of two.

The fix: explicitly configure each output and disable the phantom tile (`DP-8`).

## Configuration

### File location

Copy `monitors.conf` to:

```
~/.config/hypr/monitors.conf
```

### What the config does

| Output | Role | Resolution | Scale | Position |
|--------|------|------------|-------|----------|
| `DP-7` | Apple Studio Display | 5120×2880 @ 60Hz | 2x | Left |
| `eDP-1` | Framework Laptop 13 | 2880×1920 @ 120Hz | 2x | Right, vertically centered |
| `DP-8` | Phantom tile (disabled) | — | — | — |

The laptop screen is vertically centered relative to the Studio Display:
- Studio Display logical height: 1440px (2880 ÷ 2)
- Laptop logical height: 960px (1920 ÷ 2)
- Y-offset: (1440 − 960) ÷ 2 = **240px**

### Note on port names

The port names `DP-7` and `DP-8` may change if you plug the Thunderbolt cable into a different port. Run `hyprctl monitors` to check the current names and update the config accordingly.

## Applying changes

Hyprland reloads config automatically on save. To force a reload:

```bash
hyprctl reload
```
