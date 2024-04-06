# qemu-sunxi-yocto
Base repo for qemu-sunxi yocto

INSTRUCTIONS
============

1) Initialize repo

`repo init -u https://github.com/straxy/qemu-sunxi-yocto -m default.xml`

`repo sync -j4`

2) Setup environment

`source setup-environment build_fb`

3) Start build

`DISTRO=mistra-framebuffer MACHINE=cubieboard bitbake core-image-minimal`

Output image is in `./tmp/deploy/images/cubieboard`.

4) Resize `.sunxi-sdimg` image to 1GiB

`qemu-img resize core-image-minimal-cubieboard.sunxi-sdimg 1G`

SD card is ready to use.
