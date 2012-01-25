Configuration files and documentation for creating usb stick
containing multiple Lnux Live images selectable from Grub2 menu.

## Usage

mkfs.vfat -n LinuxBoot /dev/sdd1
grub2-install --no-floppy --root-directory=/media/LinuxBoot /dev/sdd

Copy boot/grub2/grub.cfg and disks directory.
