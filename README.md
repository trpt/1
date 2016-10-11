# 1
cryptsetup wrapper in bash

# Description
This wrapper is mostly for those who use `cryptsetup` with non-default parameters often in shell and do not want to type long commands. Also it has some advanced features like encrypted keyfiles, which is highly experimental and does not exist in `cryptsetup` in form as in e.g. Truecrypt. Also with the help of custom `encryptk` hook you can easily decrypt your system partition at boot with encrypted keyfile.

# Config
You *should* change config options in source to match your needs. It is good idea to put script in PATH and into your rescue flash drive.

# Usage
`1 action`

where `action` is:  
`o` `open` - decrypt something and mount it in $mountpath  
`n`, `new` - encrypt block device or create encrypted file container  
`f`, `file` - generate new file of specifeid size with random data  
`k`, `key` - generate new keyfile with /dev/random  
`c`, `close` - unmount and close container  
`1`, `panic` - force unmount and close all containers  
`w`, `wipe` - securely wipe block device with cryptsetup  

# System encryption (advanced skillz needed)
You can encrypt the whole system partition with this script in the stage of installing. To decrypt it at boot you should use `encryptk` hook to generate initial ramdisk (initramfs). In Arch you should put `encryptk` files in appropriate folders in `/etc/initcpio`, configure hook (check it source for comments) and add `encryptk` hook at the end of HOOKS array in `/etc/mkinitcpio.conf`. Then generate image with `mkinitcpio` command. Finally, you should put something like `root=/dev/mapper/root` to your kernel parameters in `grub.cfg`.

# Notes
Encrypted keyfiles are not supported by cryptsetup, and my implementation of it could be harmful to your data, could kill your cat, destroy your house and start 3rd World War.

# Dependencies
`bash` >= v.4  
`cryptsetup`  
optional `ddrescue` and `fallocate`  

Used daily in Arch Linux and tested in many others.
