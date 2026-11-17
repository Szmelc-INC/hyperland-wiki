---
weight: 1
title: Installation
---

> [!WARNING]
> Hyperland is not meant to be a full and user-friendly Desktop Environment. In a nutshell, it's a set of
> tools to allow you to create your own Desktop Environment.
>
> Apps, integrations, shells, etc, are **your** responsibility to pick, install and configure.
>
> This wiki is _very_ verbose. It's highly recommended to scour and read the wiki first before
> assuming something is not working or not available.

> [!NOTE]
> NVIDIA GPUs are often not usable out-of-the-box, follow the [Nvidia page](../../Nvidia) after installing
> Hyperland if you plan to use one. Blame NVIDIA for this.

## Distros

Hyperland is developed and tested on **Arch Linux** and **NixOS**. Other rolling-release
distributions with current hypr\* libraries (aquamarine, hyprlang, hyprutils, hyprcursor,
hyprgraphics, hyprwire) should work when building from source.

> [!IMPORTANT]
> Packages named `hyprland` in distribution repositories are the **official Hyprland**, not
> Hyperland. Hyperland is installed from its own repository:
> [github.com/Szmelc-INC/Hyperland](https://github.com/Szmelc-INC/Hyperland).

## Installation

### Arch Linux

```sh
git clone https://github.com/Szmelc-INC/Hyperland
cd Hyperland/packaging/arch
makepkg -si
```

The `hyperland` package `provides` and `conflicts` with `hyprland`: it replaces the official
package and satisfies everything that depends on it (portals, plugins, utilities).

### Nix

```sh
nix run github:Szmelc-INC/Hyperland     # try it
nix build github:Szmelc-INC/Hyperland   # packages.default = hyperland
```

The flake keeps every `hyprland*` package name, so existing NixOS / Home Manager setups only need
the flake URL changed to `github:Szmelc-INC/Hyperland`.

### Names

Every Hyperland name has its Hyprland twin, so this wiki works with either spelling:
`Hyperland` / `Hyprland`, `hyperctl` / `hyprctl`, `hyperpm` / `hyprpm`,
`start-hyperland` / `start-hyprland`, `~/.config/hypr/hyperland.conf` /
`~/.config/hypr/hyprland.conf`, `HYPERLAND_*` / `HYPRLAND_*` environment variables.

### Manual

Dependencies:

> [!NOTE]
> Please note that Hyperland uses the C++26 standard, so both your compiler and your
> C++ standard library has to support that (`gcc>=15` or `clang>=19`).

{{% details title="Arch" closed="true" %}}

```plain
yay -S ninja gcc cmake meson libxcb xcb-proto xcb-util xcb-util-keysyms libxfixes libx11 libxcomposite libxrender libxcursor pixman wayland-protocols cairo pango libxkbcommon xcb-util-wm xorg-xwayland libinput libliftoff libdisplay-info cpio tomlplusplus hyprlang-git hyprcursor-git hyprwayland-scanner-git hyprwire-git xcb-util-errors hyprutils-git glaze hyprgraphics-git aquamarine-git re2 hyprland-qtutils-git muparser
```

_(Please make a pull request or open an issue if any packages are missing from
the list)_

{{% /details %}}

{{% details title="openSUSE" closed="true" %}}

```sh
zypper in gcc-c++ git meson cmake "pkgconfig(cairo)" "pkgconfig(egl)" "pkgconfig(gbm)" "pkgconfig(gl)" "pkgconfig(glesv2)" "pkgconfig(libdrm)" "pkgconfig(libinput)" "pkgconfig(libseat)" "pkgconfig(libudev)" "pkgconfig(pango)" "pkgconfig(pangocairo)" "pkgconfig(pixman-1)" "pkgconfig(vulkan)" "pkgconfig(wayland-client)" "pkgconfig(wayland-protocols)" "pkgconfig(wayland-scanner)" "pkgconfig(wayland-server)" "pkgconfig(xcb)" "pkgconfig(xcb-icccm)" "pkgconfig(xcb-renderutil)" "pkgconfig(xkbcommon)" "pkgconfig(xwayland)" "pkgconfig(xcb-errors)" glslang-devel Mesa-libGLESv3-devel tomlplusplus-devel
```

(this should also work on RHEL/Fedora if you remove `Mesa-libGLESv3-devel` and
`pkgconfig(xcb-errors)`)

{{% /details %}}

{{% details title="FreeBSD" closed="true" %}}

```sh
pkg install git pkgconf gmake gcc evdev-proto cmake wayland-protocols wayland libglvnd libxkbcommon libinput cairo pango pixman libxcb
pkg install meson jq hwdata libdisplay-info libliftoff
export CC=gcc CXX=g++ LDFLAGS="-static-libstdc++ -static-libgcc"
```

{{% /details %}}

{{% details title="Ubuntu" closed="true" %}}

Ubuntu 26.04 LTS - A build script available at [gitlab.com/kralos/hyprbuntu](https://gitlab.com/kralos/hyprbuntu).

{{% /details %}}

> [!WARNING]
> Additionally to those, you will also need a few hypr\* dependencies which may or may not be
> packaged for your distro of choice:
>
> - aquamarine
> - hyprlang
> - hyprcursor
> - hyprutils
> - hyprgraphics
> - hyprwayland-scanner (build-only)

### CMake (recommended)

```sh
git clone --recursive https://github.com/Szmelc-INC/Hyperland
cd Hyperland
make all && sudo make install
```

_CMake is always recommended as it's the intended way Hyperland should be
installed._

## Crash on launch

See [Crashes and Bugs](../../Crashes-and-Bugs).

## Custom installation (debug build, etc)

1. cd into the Hyperland repo.
2. for debug build:

```bash
make debug
sudo make install
```

3. Any other config: (replace `<PRESET>` with your preset: `release`, `debug`)

```bash
make <PRESET> && sudo cp ./build/Hyperland /usr/bin && sudo cp ./example/hyperland.desktop /usr/share/wayland-sessions
```

## Custom Build flags

To apply custom build flags, you'll have to ditch make.

Supported custom build flags on CMake:

```bash
NO_XWAYLAND - Removes XWayland support
NO_SYSTEMD - Removes systemd dependencies
NO_UWSM - Does not install the hyprland-uwsm.desktop file
NO_HYPRPM - Does not build and install hyprpm
```

Flags can be passed to CMake like this:

```bash
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -D<FLAG>:STRING=true -B build
```

Change `<FLAG>` to one of the custom build flags. Multiple flags can be used at
once, by adding more `-D<FLAG_2>:STRING=true`.

The `BUILD_TYPE` can also be changed to `Debug`.

To build, run:

```bash
cmake --build ./build --config Release --target all -j`nproc 2>/dev/null || getconf NPROCESSORS_CONF`
```

If you configured in `Debug`, change the `--config` to `Debug` as well.

To install, run:

```bash
sudo cmake --install ./build
```

## Running In a VM

_YMMV, this is not officially supported._

Read through the
[libvirt Arch wiki page](https://wiki.archlinux.org/title/Libvirt) and get
`libvirt`, `virsh`, and `virt-viewer` setup and installed.

```bash
# Install libvirt and qemu things.
sudo pacman -S libvirt virt-viewer qemu-common
# Add yourself to the libvirt group.
sudo usermod -a -G libvirt USER # Replace 'USER' with your username.
# Enable and start libvirtd.
systemctl enable --now libvirtd
```

Go to the
[arch-boxes gitlab](https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages)
and download the latest arch qemu basic image. You can also download via any of
arch's mirrors.

```bash
curl https://geo.mirror.pkgbuild.com/images/latest/Arch-Linux-x86_64-basic.qcow2 \
  -o ~/Downloads/arch-qemu.qcow2 # Or download wherever you want.
```

Create the VM with virsh.

```bash
# Use virt-install (included with libvirt) to install the vm from the image.
virt-install \
  --graphics spice,listen=none,gl.enable=yes,rendernode=/dev/dri/renderD128 \
  --name hypr-vm \
  --os-variant archlinux \
  --memory 2048 \
  --disk ~/Downloads/arch-qemu.qcow2 \
  --import
```

Connect with `virt-viewer`, this will open a `virt-viewer` graphical session on
the tty. The default login is 'arch' for user and 'arch' for password.

> [!WARNING]
> Make sure the --attach flag is used, enabling virgl makes it so that
> we had to disable listen. This means that we can't make a direct TCP/UNIX
> socket connection to the remote display. --attach asks libvirt to provide a
> pre-connected socket to the display.\*

```sh
virt-viewer --attach hypr-vm
```

Finally on the guest follow the instructions above for either
[installing hyprland-git from the aur](#installation) or
[building manually](#manual-manual-build).
> [!WARNING]
> Make sure you install `mesa` as the OpenGL driver. The virgl drivers are
> included in `mesa`.
