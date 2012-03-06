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

### Special notes about SeaTools DOS image

I had to do following to be able to boot SeaTools hard drive
diagnostics utilities boot image. General idea should probably work
with other DOS cdrom or floppy images.

1. Copy syslinux's memdisk to the stick. Syslinux can be installed
with Yum in Fedora.

        yum install syslinux
        cp /usr/share/syslinux/memdisk /media/Bootstick/disks

2. Download [SeaTools iso image][seatools] from Seagate's site:
http://www.seagate.com/www/en-us/support/downloads/seatools

3. Extract SeaTools.ima from ISO and copy it to the stick as SeaTools.img

        mount -o loop SeaToolsDOS223ALL.ISO some-directory
        cp some-directory/SeaTools.ima /media/Bootstick/disks/SeaTools.img

4. Following menuentry _(already_ _in_ _grub.cfg)_ handles the
SeaTools, modify initrd16 line for other DOS images.


        menuentry "SeaTools" {
            linux16 /disks/memdisk bigraw
            initrd16 /disks/SeaTools.img
        }

## Known issues & TODO

Couldn't boot Fedora images from iso loopback. Probably related to bug [650672][rh650672]

[rh650672]: https://bugzilla.redhat.com/show_bug.cgi?id=650672
[seatools]: "http://www.seagate.com/www/en-us/support/downloads/seatools"
