# PC-DOS and MS-DOS Installation Guide

This guide explains how to boot regular IBM PC-DOS or Microsoft MS-DOS in DOSBox-X, including creating hard disk images.

Before going through this guide, consider if you really need this as the integrated DOS functionality in DOSBox-X is more convenient for typical use-cases. Booting regular DOS is normally not necessary to run DOS applications such as games, or even Windows version up to 3.11 in DOSBox-X. And even if you have a application that requires a specific DOS version, you can change the reported version of the integrated DOS in DOSBox-X. There are two ways to change the DOS version:
1. There is a setting "ver" under the [dos] section in dosbox.conf (or from the DOSBox-X Configuration GUI). For example, setting "ver = 7.10" will cause DOSBox-X to set the initial DOS version as 7.10, instead of the default 5.00. Note that LFN (long filename) support will be enabled when the initial version is set to 7.0 or higher.
2. You can also set the reported DOS version with the ``VER`` command in the DOSBox-X command line. For example, ``VER SET 6 22`` will cause DOSBox-X to claim to be version 6.22. Note that this method will only change the reported DOS version, but will not effect LFN support.

Some disadvantages of booting regular DOS in DOSBox-X includes:
- Inability to use the ``MOUNT`` command to access directories on the host filesystem. All storage will have to be in the form of images, and they need to be mounted using ``IMGMOUNT`` <b>before</b> using the ``BOOT`` command to boot regular DOS.
- If you need to access a CD or DVD drive you need to load a IDE/PATA CD/DVD driver and MSCDEX
- If you need a mouse, you need to load a mouse driver
- Less free memory in the lower 640KB range, and having to tune available memory by selectively loading drivers high.
- If you need XMS memory you need to load a driver (typically HIMEM.SYS)
- If you need EMS memory you need to load a driver (typically EMM386.EXE)

Some external links with useful information:
- DOS memory management - [[https://www.vogonswiki.com/index.php/DOS_memory_management]]
- CD-ROM driver help - [[https://www.computerhope.com/cdromd.htm]]
- How to get a mouse to work in MS-DOS - [[https://www.computerhope.com/issues/ch000007.htm]]

## General guidelines
This document assumes that you have PC-DOS or MS-DOS diskette images. Getting these image files is outside the scope of this document.

### DOS versions
Unless noted otherwise, the PC-DOS and MS-DOS versions are equivalent for this document. There are various limitations that DOS imposes that are dependant on the version. A few milestones:

- PC-DOS version 1.0, supports only 5.25" 8-sector 160KB (SSDD) diskettes
- PC-DOS version 1.1, adds support for 5.25" 8-sector 320KB (DSDD) diskettes
- MS-DOS version 1.25
  - First version available to other OEMs
  - Equivalent to PC-DOS 1.1 (but missing DISKCOPY, DISKCOMP, COMP and MODE utilities)
- DOS version 2.0
  - First to support HDDs up to 16 or 32MB (depending on OEM)
  - First to support 5.25" 9-sector 180KB (SSDD) and 360KB disks (DSDD)
- DOS version 3.0
  - First version to support FAT16 partitions up to 32MB
  - First version to support 5.25" 1.2MB disks (HD)
  - First version to support the AT internal clock
- DOS version 3.2, adds support for 3.5" 720kB disks (2DD)
- DOS version 3.3
  - First version to support extended and logical partitions
  - First version to support HDDs up to 504MB
  - First version to support 3.5" 1.44MB disks (HD)
- DOS version 4.0
  - First version to allow HDDs up to 4,095MB with up to two partitions (primary of up to 2,047MB and a logical of up to 2,039MB)
  - First version to included HIMEM.SYS XMS 2.x driver with support for up to 16MB RAM
- MS-DOS version 5.0
  - First version to support 3.5" 2.88MB disks (ED)
  - First version to support HDDs up to 7.84GB
- MS-DOS version 6.0 included an updated HIMEM.SYS XMS 3.x driver with support for up to 64MB RAM
- MS-DOS version 7.0 (included in Windows 95 and 95A)
  - First version to support VFAT
  - First version to allow up to 4GB RAM
  - First version to support HDDs up to 32GB (CHS type only)
- MS-DOS version 7.1 (included in Windows 95 OSR2, 98 and 98SE)
  - First version to support FAT32
  - First version to support LBA for HDDs up to 2TB, although FDISK requires patch to support HDD size greater than 64GB
  - Considered the best MS-DOS version to be used in modern systems. While unofficial, there is also standalone MS-DOS 7.1 installation package available
- MS-DOS version 8.0 (included in Windows ME)
  - Removed some features such as real-mode support, although there are patches to re-enable some of these features

### DOS editions
MS-DOS was licensed by many clone manufacturers and in the early days these OEM editions were 'personalized' to the manufacturer, and therefore many of these early OEM specific editions don't work, or only work partially in DOSBox-X. Because of this, up to DOS version 3.2, it is typically easier to use the IBM PC-DOS versions in DOSBox-X.

## Booting DOS from disks
Booting DOS from a disk image is pretty straight forward. Start DOSBox-X and you should find yourself at the DOSBox-X ``Z:\>`` prompt. This is not real DOS, but a 'simulated' DOS that is compatible with most DOS games and applications. Now type something equivalent to
```
 BOOT dos.img
```
Assuming that dos.img is an uncompressed DOS disk image in IBM-MFM format, typically with an file extension of .IMG or .IMA, in your current working directory, it should start it. This even works for IBM PC-DOS 1.00.

<img src="images/MS-DOS:PC-DOS_1.0.png" width="640" height="400" alt="Booting a PC-DOS 1.00 diskette image"><br>

## Creating a DOS 2.0-3.21 HDD image
Notes:
- For DOS 2.x
  - The maximum partition size depends on the OEM version, and should be 16 or 32MB using a FAT12 filesystem.
- For DOS 3.00-3.21
  - The maximum partition size is supposed to be 32MB, using a FAT16 filesystem, but in reality this only appears to be the case for PC-DOS 3.0 and 3.1. Other DOS versions are in practice limited to either 31MB, or their ``FDISK`` (or equivalent) tool is simply incompatible with DOSBox-X. For this reason the below examples will use 31MB for maximum compatibility between DOS versions.
- While it is possible to use a HDD size larger then the maximum partition size, this is not recommended as these DOS versions only support a maximum of one DOS partition per HDD. In effect, you will not be able to access the additional capacity from DOS, and it is therefore waisted space. In addition the ``FDISK`` option to use the entire fixed disk for DOS gets confused if the drive is larger then 32MB, and depending on the DOS version will either overflow such that a 40MB HDD image becomes a 40-32=8MB partition, or it will create a drive that cannot be formatted.

|DOS|OEM|Maximum partition size|Note|
|---|---|----------------------|----|
|MS-DOS 2.11|Zenith|-|Incompatible disk preparation software|
|MS-DOS 3.10|Compaq|-|Incompatible FDISK|
|MS-DOS 3.10|HP|31MB|Fails to boot from diskette, this can be circumvented by renaming CONFIG.SYS. FDISK hangs with 32MB|
|MS-DOS 3.20|-|31MB|Will fail to boot with 32MB|
|MS-DOS 3.20|Tandy|31MB|Format error, and will fail to boot with 32MB|
|MS-DOS 3.21|-|31MB|Format error, and will fail to boot with 32MB|
|PC-DOS 2.00|IBM|32MB||
|PC-DOS 2.10|IBM|32MB||
|PC-DOS 3.0|IBM|32MB||
|PC-DOS 3.1|IBM|32MB||
|PC-DOS 3.2|IBM|31MB|Will fail to boot with 32MB|

<i>Note 2:</i> If you specify a different size then 31MB for the ``IMGMAKE`` command, pay close attention to the output of ``IMGMAKE`` as you will need to adjust the ``IMGMOUNT`` size parameter values accordingly.

The ``IMGMOUNT`` size parameter should have the format of: ``512,<sectors>,<heads>,<cylinders>``.

First you need to start DOSBox-X, and create an empty HDD image file.

```
 IMGMAKE hdd.img -t hd -size 31 -nofs
 IMGMOUNT 2 hdd.img -t hdd -size 512,32,2,992 -fs none
```
<img src="images/MS-DOS:PC-DOS_3.2_IMGMAKE.png" width="640" height="400" alt="Running IMGMAKE and IMGMOUNT commands"><br>

You are now ready to boot the DOS diskette image:
```
 BOOT dos.img
```
Assuming that your uncompressed DOS 3.0-3.2 image is named dos.img and in your current working directory, it should boot DOS from the diskette image.

<img src="images/MS-DOS:PC-DOS_3.2_BOOT.png" width="640" height="400"><br>
These early DOS versions did not have an installer, so the preparation and installation is a manual process. You need to start with creating a DOS partition.

Run ``FDISK`` and select option 1 to create a new DOS partition, and confirm you want to use the entire fixed disk for DOS.

<img src="images/MS-DOS:PC-DOS_3.2_FDISK.png" width="640" height="400" alt="Running PC-DOS 3.2 FDISK"><br>

<img src="images/MS-DOS:PC-DOS_3.2_FDISK_Restart.png" width="640" height="400" alt="PC-DOS 3.2 FDISK restart confirmation"><br>

After it is finished, press any key and DOS will reboot DOSBox-X and your again at the DOSBox-X ``Z:\>`` prompt. At this point the HDD image is partitioned, but not yet formatted or made bootable, so that is what you need to do next.
```
 IMGMOUNT 2 hdd.img -t hdd -size 512,32,2,992 -fs none
 BOOT dos.img
```
You have now again booted from the disk image, and are ready to format the C: and transfer the system files.
```
 FORMAT C: /S
```
<img src="images/MS-DOS:PC-DOS_3.2_FORMAT.png" width="640" height="400" alt="Running PC-DOS 3.2 FORMAT command"><br>

You can optionally copy over the rest of the diskette contents at this point
```
 MKDIR C:\DOS
 COPY A:\*.* C:\DOS
```
You can also create a ``AUTOEXEC.BAT`` and ``CONFIG.SYS`` on the HDD with the included ``EDLIN`` editor.

From the DOSBox-X menu bar select Main and then select Reset guest system. You are again at the DOSBox-X ``Z:\>`` prompt.

Our setup is now complete and all that is left is how to boot the image normally. From the DOSBox-X ``Z:\>`` prompt this can be accomplished with
```
IMGMOUNT C hdd.img -size 512,32,2,992
BOOT -L C
```
You probably don't want to memorize those last two commands, so do yourself a favour and create yourself a DOSBox-X .conf file and place those commands in the [autoexec] section of that config file.

<i>Note:</i> You may notice that instead of using "2", we are now using "C". This is because the image is now partitioned and formatted and DOSBox is able to find the partition within it. The advantage of being able to address it as "C" is that you can access the files inside the HDD image from the DOSBox-X integrated DOS, making it easier to transfer files.

<i>Note 2:</i> Unfortunately we do still need to specify the drive geometry as DOSBox-X cannot autodetect it for DOS versions prior to 3.3.

<img src="images/MS-DOS:PC-DOS_3.2_BOOT_HDD.png" width="640" height="400" alt="Boot PC-DOS 3.2 from HDD"><br>

## Creating a DOS 3.3 HDD image
Creating a DOS 3.3 HDD image is nearly identical to that of DOS 3.0-3.2 above with a few small notes
- DOS 3.3 introduced the partitioning scheme with primary, extended and logical partitions. However, DOSBox-X has only limited support for extended and logical partitions. You can create them, and when you boot your DOS image, you can access them. But when you ``IMGMOUNT`` the image in DOSBox-X, the integrated DOS will only be able to access the primary partition.
- The maximum HDD size is now 504MB, but the maximum partition size is still only 32MB. Since DOSBox-X has only limited support for extended and logical partitions, it is recommended that you only create a single primary partition up to 32MB per HDD image. If you need multiple drives, you can create multiple images.
- After you have created your image, due to the newer style partition layout, which DOSBox-X can autodetect, you do not have to specify the geometry to mount the image. So your can boot from the HDD image with the following commands instead.

```
IMGMOUNT C hdd.img
BOOT -L C
```

<img src="images/MS-DOS:MS-DOS_3.3_BOOT_HDD.png" width="640" height="400" alt="Boot MS-DOS 3.3 from HDD"><br>

## Creating a MS-DOS 4.0x HDD image
First of all, consider if you really, really want to use MS-DOS 4.x as it was considered a very buggy release. If you decide to continue with a full install, and you have the choice, do yourself a favour and use the 3.5" version as it will minimize the amount of disk swapping required.

MS-DOS 4.0x on 5.25" media consists of the following six disks
 - Install
 - Select
 - Operating 1
 - Operating 2
 - Operating 3
 - Shell

MS-DOS 4.0x on 3.5" media consists of the following three disks
 - Setup
 - Operating
 - Shell

OEM versions could have additional disks such as a Diagnostic disk.

- Like DOS 3.3 before it, MS-DOS 4.0x supports primary, extended and logical partitions. However, DOSBox-X has only limited support for extended and logical partitions. You can create them, and when you boot your DOS image, you can access them. But when you ``IMGMOUNT`` the image in DOSBox-X, the integrated DOS will only be able to access the primary partition.

- Be sure to use the -NOFS flag when creating an image with DOSBos's ``IMGMAKE``. If you don't, it will create a partitioned and formatted HDD image, which is incompatible with MS-DOS 4.0x. The MS-DOS 4.0x installer will not offer the option to install to the HDD. And if you manually SYS the drive, it will not boot from it.

- MS-DOS 4.0x supports HDDs up to 4,095MB. It is also supposed to support a primary partition up to 2,047MB and a logical partition of 2,048MB. But creating partitions that large will result in numerous problems, typically in ``FORMAT`` giving a "Divide overflow" error. The solution, assuming your only going to have a single primary partition, is to create a HDD image no larger then 2014MB.

In these examples we still use a 32MB HDD.

### Bare-bones install
If you decide to do just an absolute minimal install, and effectively skip the MS-DOS 4.0x install program, you don't need to worry about the buggy MS-DOS 4.0x installer.

```
 IMGMAKE hdd.img -t hd -size 32 -nofs
 IMGMOUNT 2 hdd.img -fs none
```
Now you need to boot from the first MS-DOS 4.0x disk, which is called either Setup or Install depending on the media type.
```
 BOOT SETUP.IMG
```
<img src="images/MS-DOS:MS-DOS_4.01_BOOT_FDD.png" width="640" height="400" alt="Boot MS-DOS 4.01 from Disk"><br>

When at the Welcome screen (3.5" media) or prompted to insert the SELECT disk (5.25" media), simply press ESC instead followed by F3 to drop to the MS-DOS prompt

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER.png" width="640" height="400" alt="MS-DOS 4.01 Installer welcome screen"><br>

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER_EXIT.png" width="640" height="400" alt="MS-DOS 4.01 Installer exit screen"><br>

and run the following command:
```
 FDISK
```
<img src="images/MS-DOS:MS-DOS_4.01_FDISK.png" width="640" height="400" alt="MS-DOS 4.01 FDISK"><br>

Now select option 1 to create a DOS partition

<img src="images/MS-DOS:MS-DOS_4.01_FDISK2.png" width="640" height="400" alt="MS-DOS 4.01 FDISK"><br>

Followed by option 1 to create a Primary DOS Partition

<img src="images/MS-DOS:MS-DOS_4.01_FDISK3.png" width="640" height="400" alt="MS-DOS 4.01 FDISK"><br>

Confirm you want to use the maximum available size

<img src="images/MS-DOS:MS-DOS_4.01_FDISK4.png" width="640" height="400" alt="MS-DOS 4.01 FDISK"><br>

And finally press any key to restart, to go back to the DOSBox-X ``Z:\>`` prompt.

At this point your image file is partitioned, but still needs to be formatted and made bootable. We first need to execute the exact same ``IMGMOUNT`` and ``BOOT`` commands from before.

```
IMGMOUNT 2 hdd.img -fs none
BOOT SETUP.IMG
```
You can now FORMAT the C: drive with the /S switch to transfer the system files.

<img src="images/MS-DOS:MS-DOS_4.01_FORMAT.png" width="640" height="400" alt="MS-DOS 4.01 FORMAT"><br>

The HDD image is now bootable and you can optionally copy some of the DOS utilities from the diskette to the HDD and create your ``CONFIG.SYS`` and ``AUTOEXEC.BAT``.

<img src="images/MS-DOS:MS-DOS_4.01_BOOT_HDD.png" width="640" height="400" alt="MS-DOS 4.01 HDD Boot"><br>

### Full install from 3.5" media
Notes
- The MS-DOS 4.0x installer can corrupt its own installation diskettes, as such you should change the permission of the disk images in the host OS such that the image files are READ-ONLY. In turn DOSBox-X will treat them as if the disks have the write-protect set.

- It is recommended that you first follow the [#bare-bones-install](Bare-bones) install above, at least up to the point where the DOS partition has been formatted. The alternative is to let MS-DOS 4.0x installer create the partition for you, but this requires that you go through the first phase of the installation process twice, including creating the "SELECT COPY" backup diskette twice.

- If you skip the ``FORMAT`` step during the Bare-bones install, the MS-DOS 4.0x installer will error out after it does the format itself, and the DOSBox log will contain the message "ERROR BIOS:INT13: Function 18 called on drive 80 (dos drive 2)", and you cannot continue the install.

For this process, it is assumed that you already have your image file created, partitioned and formatted with MS-DOS 4.0x.

During install, the installer will insist on a blank disk to be labelled "SELECT COPY", to make a copy of the INSTALL (Setup) disk. Unfortunately while it seems the installer should allow to use the B: drive for this purpose this does not seem to work in practice (it seems this only works if there is no disk in drive B: when the installer starts, which you cannot do with DOSBox-X).
```
 IMGMAKE SELECT_COPY.IMG -t fd_720
 IMGMOUNT 2 hdd.img -size 512,63,2,520 -fs none
 BOOT SETUP.IMG SELECT_COPY.IMG SETUP.IMG SELECT_COPY.IMG OPERATING.IMG MSSHELL.IMG
```

Notes
- You may notice in the above BOOT command, that SETUP.IMG and SELECT_COPY.IMG appear twice. This is not an error, and is done to simplify the installation process due to the fact that the install process will ask for you to swap between those disks.

- It is important that you keep track of the order of the disks that you specify on the BOOT line, as you will need to switch between them using either a keyboard shortcut or the "Swap floppy" option on the DOSBox-X menu bar located under the DOS heading. Unfortunately at this point there is no visual indication in DOSBox-X itself, as to which diskette is the current one inserted, you can however look at the DOSBox-X messages logged to the console if you have it open to see a message as to which disk is currently inserted. When you cycle through them one by one, once you reach the end, you will simply go back to the first.

- While the first MS-DOS 4.0x 3.5" disk is labelled "Setup" the installer will actually refer to it as "INSTALL".

<b>Welcome</b><br>
When booted to the Welcome screen, simply press Enter as prompted.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER.png" width="640" height="400" alt="MS-DOS 4.01 Installer welcome screen"><br>

<b>Introduction</b><br>
Press again Enter to bypass the Introduction screen.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER2.png" width="640" height="400" alt="MS-DOS 4.01 Introduction screen"><br>

<b>Specify Function and Workspace</b><br>
You will now be asked between 3 install options. "program workspace" in this context means the amount of disk space available for <i>other</i> programs. Your effectively being asked if you want to do a Small, Medium or Full installation of MS-DOS 4.0x.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER3.png" width="640" height="400" alt="MS-DOS 4.01 Specify Function and Workspace"><br>

<b>Select Country and Keyboard</b><br>
You can now change the country and keyboard settings if necessary. Select option 1 when ready to continue.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER4.png" width="640" height="400" alt="MS-DOS 4.01 Select Country and Keyboard"><br>

<b>Select Installation Drive</b><br>
It will now ask where you want to install MS-DOS 4.0x. Select to install on the C: (option 1).

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER5.png" width="640" height="400" alt="MS-DOS 4.01 Select Installation Drive"><br>

<b>Specify DOS Location</b><br>
If you want you can change the directory into which DOS will be installed, but you probably want to stick to the default, so press Enter to accept option 1.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER6.png" width="640" height="400" alt="MS-DOS 4.01 Specify DOS Location"><br>

<b>Number of Printers</b><br>
You should probably just leave this at 0. Press Enter to continue.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER7.png" width="640" height="400" alt="MS-DOS 4.01 Number of Printers"><br>

<b>MS-DOS Shell Option</b><br>
Here you can elect to install the MS-DOS Shell, which will automatically start on boot if selected.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER8.png" width="640" height="400" alt="MS-DOS 4.01 MS-DOS Shell Option"><br>

<b>Installation Options</b><br>
Here you can review the options. Select option 1 to accept and continue with installation.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER9.png" width="640" height="400" alt="MS-DOS 4.01 Installation Options"><br>

<b>Continuing Installation</b><br>
This screen is to notify you that you need to have a blank disk ready. Just press Enter to continue.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER10.png" width="640" height="400" alt="MS-DOS 4.01 Installation Complete"><br>

<b>Continuing Installation</b><br>
This is an important point, you now need to do a disk swap. This can be accomplished with a hot-key combination, or possibly easier from the DOSBox-X menu bar, select the "DOS" menu, followed by "Swap floppy". It is important that you use the "Swap floppy" option each time it asks you to insert a different disk. The disks have been "stacked" with the BOOT command in such a way that they are in the correct order. This is important, as other then looking at the DOSBox-X logging you have no visual indicator as to which diskette is the active one.

You will be asked in turn to insert the "INSTALL" disk (Setup), the "SELECT COPY" disk, again the "INSTALL DISK" and again the "SELECT COPY" disk. You will then be asked for the OPERATING disk, and finally (if selected to install), the MS-DOS SHELL disk.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER11.png" width="640" height="400" alt="MS-DOS 4.01 Continuing Installation"><br>

<b>Installation Complete</b><br>
The installation is complete, and we can reset DOSBox-X from the "Main" menu with "Reset guest system", and we should be back at the DOSBox-X ``Z:\>`` prompt.

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER_FINISHED.png" width="640" height="400" alt="MS-DOS 4.01 Installation Complete"><br>

You can now boot the MS-DOS 4.0x HDD image using
```
IMGMOUNT C hdd.img
BOOT -L C
```

Depending if we installed DOS Shell or not, we will either get a DOS prompt or a DOS Shell menu.

<img src="images/MS-DOS:MS-DOS_4.01_BOOT_HDD2.png" width="640" height="400" alt="MS-DOS 4.01 Installation Complete"><br>

<img src="images/MS-DOS:MS-DOS_4.01_DOSSHELL.png" width="640" height="400" alt="MS-DOS 4.01 Installation Complete"><br>


### Full install from 5.25" media
This process is basically the same as for the 3.5" media, but you have more disks and they are labelled differently. You will also need two blank disks.

### Booting MS-DOS 4.0x from HDD
Now that you have created a bootable HDD image you can boot it from the DOSBox-X ``Z:\>`` prompt with the following commands:
```
IMGMOUNT C hdd.img
BOOT -L C
```

## Creating a PC-DOS 4.0x HDD image
Installing PC-DOS 4.0x is easier then MS-DOS 4.0x because it does not require the creation of backup disks, and comes on only two 3.5" disks (Install and Operating).

The same limits on disk and partition sizes seem to apply as MS-DOS 4.0x.

First start by creating a HDD image file, mount it and boot from disk.

```
 IMGMAKE hdd.img -t hd -size 1024 -nofs
 IMGMOUNT 2 hdd.img -size 512,63,2,520 -fs none
 BOOT INSTALL.IMG OPERATING.IMG
```

You can now largely follow the instructions for MS-DOS 4.0x. There will be fewer questions, for instance you will not get the question if you want to install the DOS Shell. After the install is finished and you boot from the HDD image, it will go directly to the DOS Shell program.

## Creating a MS-DOS 5.0+ HDD image
TBD...
