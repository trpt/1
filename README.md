# 1
cryptsetup wrapper in bash

# Description
This wrapper is mostly for those who uses `cryptsetup` with non-default parameters often in shell and do not want to type long commands. Also it has some advanced features like encrypted keyfiles, which is highly experimental and does not exist in `cryptsetup` in form as in e.g. Truecrypt. Also with the help of custom `encryptk` hook you can easly decrypt your system partition at boot with encrypted keyfile.

# Config
You *should* change config options in source to match your needs. It is good idea to put script in PATH and into your rescue flash drive.

# Usage
`1 action`

where `action` is:  
`o` - open block device with passphrase  
`ok` - open block device with encrypted keyfile  
`of` - open file with passphrase  
`ofk` - open file with encrypted keyfile  
`n` - encrypt block device with passphrase  
`nk` - encrypt block device with encrypted keyfile  
`nf` - create file container encrypted with passphrase  
`nfk` - create file container with encrypted keyfile  
`gf` - generate new file of specifeid size with random data  
`gkf` - generate new keyfile with /dev/random  
`c` - unmount and close container  
`1` - force unmount and close all containers  
`wipe` - securely wipe block device with cryptsetup  

# System encryption (advanced skillz needed)
You can encrypt the whole system partition with this script in the stage of installing. To decrypt it at boot you should use `encryptk` hook to generate initial ramdisk (initramfs). In Arch you should put `encryptk` files in appropriate folders in `/etc/initcpio`, configure hook (check it source for comments) and add `encryptk` hook at the end of HOOKS array in `/etc/mkinitcpio.conf`.

# Notes
Encrypted keyfiles are not supported by cryptsetup, and my implementation of it could be harmful to your data, could kill your cat, destroy your house and start 3rd World War.

# Dependencies
`bash`  
`cryptsetup`  
optional `ddrescue`  

Used daily in Arch Linux and tested in many others.
