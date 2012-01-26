Configuration files and documentation for creating usb stick
containing multiple Linux Live images selectable from Grub2 menu.

## Usage

Download disk images to disks directory.

Partition, format and install boot loader to usb stick as root.

    mkfs.vfat -n Bootstick /dev/sdd1
    mount /dev/sdd1 /media/Bootstick
    grub2-install --no-floppy --boot-directory=/media/Bootstick /dev/sdd

Copy grub2/grub.cfg and disks directory to stick.

Directory tree on the stick should look like this:

    .
    |-- disks
    |   |-- Fedora-16-x86_64-Live-Desktop.iso
    |   |-- kubuntu-11.10-desktop-amd64.iso
    |   |-- kubuntu-11.10-desktop-i386.iso
    |   |-- ubuntu-11.10-desktop-amd64.iso
    |   `-- ubuntu-11.10-desktop-i386.iso
    `-- grub2
        |-- number of files installed by grub2-install...
        `-- grub.cfg
