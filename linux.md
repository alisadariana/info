# Linux things

## Linux VS Code Configuration

```
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "${workspaceFolder}/include",
                "${workspaceFolder}/arch/arm/include",
                "${workspaceFolder}/arch/arm/include/generated"
            ],
            "defines": [
                "__KERNEL__",
                "MODULE",
                "MODULE_AUTHOR(x)=x",
                "MODULE_DESCRIPTION(x)=x",
                "MODULE_LICENSE(x)=x"
            ],
            "cStandard": "c11",
            "intelliSenseMode": "linux-gcc-arm",
            "configurationProvider": "ms-vscode.makefile-tools"
        }
    ],
    "version": 4
}
```

## Prepare SD Card with Linux image

1. download ADI Kuiper Linux
2. unzip
3. format SD card
4. $ sudo umount /dev/<sd_name>
5. $ time sudo dd if=<path_to_kuiper_image> of=/dev/<sd_name>
	- ex: time sudo dd if=/home/dariana/base/adi_kuiper_linux/image_2022-08-04-ADI-Kuiper-full/2022-08-04-ADI-Kuiper-full.img of=/dev/sda

## Kernel Debugging

https://www.linuxtopia.org/online_books/linux_kernel/kernel_configuration/ch09s07.html

## Linux Kernel Configuration

```
export ARCH=<arch>
export CROSS_COMPILE=<cross_compiler>
    export CROSS_COMPILE=<path_to_compiler>/gcc-arm-10.3-2021.07-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-
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