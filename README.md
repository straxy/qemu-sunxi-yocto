# qemu-sunxi-yocto

Base repo for qemu-sunxi yocto

## Introduction

This repository contains the manifest file for building the Yocto image for Cubieboard,
which can be used in QEMU to follow tutorials from [MistraSolutions blog](https://www.mistrasolutions.com).

### Supported branches

There are two branches supported right now:

- scarthgap
- kirkstone

### Supported MACHINEs

The two `MACHINE`s that are supported are:

- the default `cubieboard`
- the customized `cubieboard-ng`, which is used with custom QEMU components.

### Supported images

There are three supported images

- mistra-image - the basic image used as the starting point
- mistra-swupdate - the mistra-image adjusted for A/B partitioning and OTA updates using SWupdate
- update-image - the image based on mistra-swupdate which generates the update SWU file

## Build instructions for cubieboard and mistra-image

1) Initialize repo

```bash
repo init -u https://github.com/straxy/qemu-sunxi-yocto -m default.xml -b scarthgap
repo sync -j4
```

2) Setup environment

```bash
source setup-environment build_fb
```

3) Start the build

```bash
DISTRO=mistra-framebuffer MACHINE=cubieboard bitbake mistra-image
```

Output image is in `./tmp/deploy/images/cubieboard`.

4) Create an empty SD card with

```bash
qemu-img create sd.img 1G
```

5) Copy `.wic` image to the SD card

```bash
gunzip -c tmp/deploy/images/cubieboard/mistra-image-cubieboard.rootfs.wic.gz | dd of=sd.img bs=1M iflag=fullblock oflag=direct conv=fsync
```

6) Resize image to 1GiB

```bash
qemu-img resize sd.img 1G
```

SD card is ready to use.
