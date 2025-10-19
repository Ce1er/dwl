# Fork Info:

This is my personal fork of [dwl]. It is based on release 0.7 and contains custom
patches and a custom `config.h`.

It is not intended for general use, some parts of it will rely on my specific hardware
and software preferences. I will try to document these below.

## Building dwl for Gentoo linux

Will add ebuild for this fork in the future but for now build manually.

Normal dwl Dependencies:
From `=dwl-0.7::gentoo`

```sh
COMMON_DEPEND="
    gui-libs/wlroots-0.18:=[libinput,session,X?]
    dev-libs/libinput:=
    dev-libs/wayland
    x11-libs/libxkbcommon
    X? (
        x11-libs/libxcb:=
        x11-libs/xcb-util-wm
    )
"

RDEPEND="
    ${COMMON_DEPEND}
    X? (
        x11-base/xwayland
    )
"

DEPEND="
    ${COMMON_DEPEND}
    sys-kernel/linux-headers
"

BDEPEND="
    >=dev-libs/wayland-protocols-1.32
    >=dev-util/wayland-scanner-1.23
    virtual/pkgconfig
"
```

**Note:**
Unlike upstream XWayland is enabled by default, so dependencies required by X use flag are required by default as well.
XWayland can be disabled by commenting out the lines below `# XWayland Support` in `config.mk` and uncommenting the lines below `No XWayland Suport`.

`=dwl-0.7::gentoo` respects user defined `CC` and `PKG_CONFIG`. Building manually will not. If you want to use something other than `gcc` and `pkg-config` set that in `config.mk`.
You may want to set other options as well. e.g. `make CFLAGS="-march=native -O2 -pipe"`

Additional Dependencies:

- kitty: used in `termcmd` in `config.h`
- wofi: used in `menucmd` in `config.h`

```sh
RDEPEND+="
    x11-terms/kitty
    gui-apps/wofi
"
```

Useful non-dependencies:

- `wlr-randr` available in `gui-apps/wlr-randr::guru`. Helps check monitor config being applied correctly.

## Parts Specific To Hardware

- `MonitorRule` in `config.h`

[dwl]: https://codeberg.org/dwl/dwl
