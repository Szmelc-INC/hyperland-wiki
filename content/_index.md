---
cascade:
  type: docs
title: Hyperland Wiki
---

> [!IMPORTANT]
> **Hyperland is not Hyprland.** Hyperland is an independent fork of **Hyprland v0.54.0**,
> maintained by [Szmelc-INC](https://github.com/Szmelc-INC). It is not affiliated with, endorsed
> by or supported by Hyprland Development / hyprwm. Report problems
> [here](https://github.com/Szmelc-INC/Hyperland/issues), not upstream.
>
> "Hyprland" and the Hyprland logo are registered trademarks of Hyprland Development in the
> European Union; they are mentioned only to say where Hyperland and this wiki come from.

Welcome to the Hyperland Wiki!

This wiki is the Hyprland 0.54.0 wiki, kept and maintained for Hyperland. Everything in it
applies to Hyperland: the configuration language (hyprlang), options, dispatchers, IPC and
plugins are those of Hyprland 0.54, and every original name keeps working (`hyprctl` and
`hyperctl`, `hyprland.conf` and `hyperland.conf`, `HYPRLAND_*` and `HYPERLAND_*`).

**Micro-manifesto:** your config keeps working; nothing is removed just because it is old;
changes are additive; stability over novelty; pragmatic and logical over fashionable.

Take a tour of the pages on the left and read the ones you need. Check your build with
`hyperctl version` (or `hyprctl version`).

## Wayland info (especially useful for Xorg users)

A Wayland compositor is a fully autonomous Display Server, like Xorg itself. It
is **not** possible to mix'n'match Wayland compositors like you could on Xorg
with window managers and compositors. It is also not entirely possible, nor
recommended, to try and use all Xorg applications on Wayland. See
[this page](../Useful-Utilities/) for a list of recommended Wayland
native/compatible programs.

Wayland **compositors** should not be confused with Xorg **window managers**.

## IMPORTANT

If you are having issues, please try [reading the FAQ](../FAQ) and configuring
sections — chances are your issue is described somewhere there. If not, you can
try [searching the issues](https://github.com/Szmelc-INC/Hyperland/issues).
