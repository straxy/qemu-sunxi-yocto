# qemu-sunxi-yocto

Base repo for qemu-sunxi yocto

## INSTRUCTIONS

1) Initialize repo

```bash
repo init -u https://github.com/straxy/qemu-sunxi-yocto -m default.xml -b scarthgap
repo sync -j4
```

2) Setup environment

```bash
source setup-environment build_fb
```

3) Start build

```bash
DISTRO=mistra-framebuffer MACHINE=cubieboard bitbake mistra-image
```

Output image is in `./tmp/deploy/images/cubieboard`.

4) Resize `.sunxi-sdimg` image to 1GiB

```bash
qemu-img resize core-image-minimal-cubieboard.sunxi-sdimg 1G
```

SD card is ready to use.
