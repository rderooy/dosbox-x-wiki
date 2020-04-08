## Overview
This applies to
- MS-DOS 6.0
  - Adds F5 and F8 clean boot and selective boot options
  - Adds Startup Menu support
  - Adds MEMMAKER memory optimizer with better HIMEM/EMM386
  - Adds Disk defrag (based on Norton SpeedDisk)
  - Adds DBLSPACE disk compression
  - Adds MSCDEX
  - SmartDrive upgraded with write caching and double buffering
  - New MS Backup software for DOS and Windows (based on Norton Backup)
  - Adds MS AntiVirus for DOS and Windows (based on Centrap Point AV)
  - Adds a Windows version of UNDELETE
  - Adds APM Power Management (POWER.EXE)
  - Adds InterLink file transfer tool (using Serial or Parallel port)
  - Adds DELTREE and MOVE commands
  - Removed EDLIN, MIRROR, RECOVER and BACKUP
- MS-DOS 6.20
  - CHKDSK replaced by SCANDISK
  - Improved DBLSPACE stability
- MS-DOS 6.21
  - DBLSPACE removed (due to Stacker lawsuit)
- MS-DOS 6.22
  - New DRVSPACE disk compression added

From this point, Microsoft MS-DOS and IBM PC-DOS have diverged. MS-DOS 6.x was available to both OEM's and end-users. However the version available to end-users was the "Upgrade" release, which requires that you already have DOS installed. It will refuse to install on a clean system. The workaround to this is fairly simple. You boot from the first disk, at the welcome screen press F3 twice and your at the command prompt. You can now, if necessary, partition and format the HDD and transfer the system files (``SYS C:``). After your done, just run SETUP.EXE or simply reboot from Disk 1 and the installer, because there are now system files on the HDD, will allow you to install MS-DOS 6.x Upgrade edition.

## Creating a MS-DOS 6.x HDD image
Starting with DOS 5.00, installing DOS in DOSBox-X is much more straight forward, as you can have ``IMGMAKE`` create a HDD image that is already partitioned and formatted.

Maximum HDD size has increased to 7.84GB, but the maximum partition size is basically still 2GB, which is a FAT16 limitation.

```
 IMGMAKE hdd.img -t hd -size 2048
 IMGMOUNT C hdd.img
 BOOT DISK1.IMG DISK2.IMG DISK3.IMG
```

When prompted to change disk, on the DOSBox-X menu bar select "DOS" followed by "Swap disk". After the installation is finished, from the DOSBox-X menu bar select "Main" followed by "Reset guest system" and you will be back at the DOSBox-Z ``Z:\>`` prompt.

You can now boot these DOS versions directly from the HDD image as follows:
```
IMGMOUNT C hdd.img
BOOT -L C
```