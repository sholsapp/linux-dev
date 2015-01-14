# linux-dev

This is just a set of scripts to rebuild a known working kernel for ARM
devices. This git repo contains just scripts/patches to build a specific kernel
for some ARM devices.

# contact

Please send bug reports to "bugs@rcn-ee.com".

# dependencies:

1. [GCC/ARM cross toolchain](http://elinux.org/Toolchains)
2. [Linaro](http://www.linaro.org/downloads/)

The kernel source will be downloaded when you run any of the build scripts. By
default this script will clone the
[linux-stable](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git)
tree to `./ignore/linux-src` with full history.

If you've already cloned torvalds tree and would like to save some hard drive
space, just modify the `LINUX_GIT` variable in `system.sh` to point to your
current git clone directory.

# requirements

For users building the
[linux-stable](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git)
tree with full history, at least 1GB of memory should be available for `git(1)`
to clone the repository. If this is a problem for your build system, you can
use a swap file to add more memory to your system.

To create a swap file on disk, you can run the following commands as a
privileged user.

```bash
dd if=/dev/zero of=/swapfile bs=1024 count=1024k
mkswap /swapfile
swapon /swapfile
```

# building

To build the kernel image use the following command.

```bash
./build_kernel.sh
```

Optionally, to build a Debian package one can use the following command.

```bash
./build_deb.sh
```

# installation

To install the kernel image to an SD card (requires `MMC` variable set in
`./system.sh`) use the following.

```bash
./tools/install_kernel.sh
```

To install the kernel image to the local system use the following. Note, the
kernel must've been built on the ARM board for this command to work.

```bash
./tools/local_install.sh
```

# development

For development, one must first run `./build_kernel.sh`, then use the files
inside of the `KERNEL` directory for your local kernel development. To rebuild
the kernel with local modifications, use the `./tools/rebuild.sh` script.
