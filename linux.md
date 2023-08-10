# Linux things

## Kernel Debugging

https://www.linuxtopia.org/online_books/linux_kernel/kernel_configuration/ch09s07.html

## Linux Kernel Configuration

```
export ARCH=<arch>
export CROSS_COMPILE=<cross_compiler>
make <board_basic_configuration>
make menuconfig
	add needed features
make savedefconfig
	=> defconfig with current configuration
mv ./defconfig ./arch/<arch_name>/configs/<specific_name_defconfig>
```

And to use the new configuration:
```
make <specific_name_defconfig>
```

## Linux Loadable Modules

To create an image and modules:
Linux 5.10

```
	prepare configuration where needed modules <- <m>
make <kernel_configuration>

make -j8 UIMAGE_LOADADDR=0x8000 uImage
sudo make INSTALL_MOD_PATH=./modules modules_install
sudo mv ./modules/lib/modules/<linux_version_name> /media/dariana/rootfs/usr/lib/modules/
```

## Embedded Linux Booting Process

https://www.youtube.com/watch?v=DV5S_ZSdK0s&t

First stage = bootloaders

	5. Root Filesystem Init Process
	^
	4. Linux Kernel Device Tree File
	^
	3. Second Stage Bootloader
	^
	2. First Stage Bootloader
	^
	1. SoC ROM Bootloader

SoC is powered and begins execution at the reset vector (something the
manufacturer already programmed into the board).

ROM bootloader starts executing.

ROM bootloader sets up some hardware then locates the First Stage Bootloader and
loads it into SoC internal memory and then passes control to it.

First Stage Bootloader copies Second Stage Bootloader into RAM and passes control
to it.

Second Stage Bootloader loads the Kernel and the Device Tree Binary into RAM.

Look at its own settings and using that start the Kernel, pass the Kernel the
Boot Arguments and Kernel takes over.

The Kernel initializes hardware components, look at the root filesystem, mount
root filesystem.

Search for init process (PID 0) and invokes it.

Spawns other processes based on configuration files.