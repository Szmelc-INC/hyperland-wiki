<div align="center">

<img src="static/android-chrome-192x192.png" width="96" alt="Hyperland">

# Hyperland Wiki

[![Deploy](https://github.com/Szmelc-INC/hyperland-wiki/actions/workflows/pages.yml/badge.svg)](https://github.com/Szmelc-INC/hyperland-wiki/actions/workflows/pages.yml)
[![License: BSD-3-Clause](https://img.shields.io/badge/license-BSD--3--Clause-105c5c)](LICENSE)

Documentation for [Hyperland](https://github.com/Szmelc-INC/Hyperland), served at
**[szmelc-inc.github.io/hyperland-wiki](https://szmelc-inc.github.io/hyperland-wiki/)**.

</div>

> [!IMPORTANT]
> Hyperland is an **independent fork of Hyprland v0.54.0**, not affiliated with or endorsed by
> Hyprland Development / hyprwm. This wiki starts from the official Hyprland wiki as it was for
> the 0.54.0 release and is maintained for Hyperland from there. "Hyprland" and its logo are
> registered trademarks of Hyprland Development in the EU.

## Contributing

Open an issue or a PR and state the reason for the change. Commit titles use the form
`Dir/Page: summary of changes`, one logical change per commit.

Hyperland stays compatible with Hyprland 0.54: documentation must keep describing the original
names (`hyprctl`, `hyprland.conf`, `HYPRLAND_*`) as valid next to the Hyperland ones.

## Local development

Install `go` and `hugo` (extended), then:

```sh
hugo serve
```

and open the printed local URL. Every push to `main` deploys to GitHub Pages.

## License

BSD 3-Clause, see [LICENSE](LICENSE). Original content by the Hyprland wiki contributors.
