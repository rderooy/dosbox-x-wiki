Back to the [[PC-DOS and MS-DOS Installation Guide|Guide:DOS Installation Guide]]

## Overview
DOS version 4.00 was the first release where IBM had the development lead. It returned to Microsoft for version 5.00.

Key new features of DOS 4.00:
- First version to allow HDDs up to 4,095MB
- First version to allow a DOS partition up to 2,047MB
- First version to include a guided installation program
- Added MEM and SWITCHES commands
- Added XMA2EMS.SYS and XMAEM.SYS supporting LIM EMS 4.0
- New DOS SHELL
- National Language Support (NLS) enhancements
- GRAPHICS utility upgraded with EGA/VGA support

This applies to
- Microsoft MS-DOS 4.00
  - First version to include HIMEM.SYS XMS 2.x driver with support for up to 16MB RAM
  - Added EMM386.SYS with support for LIM EMS 4.0
  - First version to include SMARTDRV.SYS
- Microsoft MS-DOS 4.01
- IBM PC-DOS 4.00
- IBM PC-DOS 4.01

Note: Unlike with MS-DOS, there is no obvious way to know if you have PC-DOS 4.00 or 4.01. The ``VER`` command will claim Version 4.00 for either, as will the box, manuals and installer. The ways to check are either to look at the disk labels, which will say 4.00 or 4.01, or check if some OS files like IBMBIO.COM and IBMDOS.COM are dated 08-03-1988 (MM-DD-YYYY), in which case you have the 4.01 release. IBM released a corrective service (CSD UR22624) to upgrade a 4.00 installation to 4.01, you can view the README here: http://www.retroarchive.org/garbo/pc/doc-soft/dos400.bug

External links:
- http://www.os2museum.com/wp/dos/dos-4-0/

First of all, consider if you really, really want to use DOS 4.x as it was considered a very buggy release. If you decide to continue with a full install, and you have the choice, do yourself a favour and use the 3.5" version as it will minimize the amount of disk swapping required. Also the IBM PC-DOS release is easier to install then the MS-DOS release as it uses fewer disks, but lacks HIMEM.SYS, EMM386.SYS and SMARTDRV.SYS.

MS-DOS 4.0x on 5.25" 360KB media consists of the following six diskettes
- Install, Select, Operating 1, Operating 2, Operating 3, Shell

MS-DOS 4.0x on 3.5" 720KB media consists of the following three diskettes
- Setup, Operating, Shell

PC-DOS 4.0x on 5.25" 360KB media consists of the following five diskettes
- Install , Select, Operating 1, Operating 2, Operating 3

PC-DOS 4.0x on 3.5" 720KB media consists of the following two diskettes
- Install, Operating

OEM versions could have additional disks such as a Diagnostic disk.

In addition the installation process will require BLANK diskettes "Select Copy"

- Like DOS 3.3 before it, DOS 4.0x supports primary, extended and logical partitions. However, DOSBox-X has only limited support for extended and logical partitions. You can create them, and when you boot your DOS image, you can access them. But when you ``IMGMOUNT`` the image in DOSBox-X, the integrated DOS will only be able to access the primary partition. As such it is recommended to only create a single DOS partition per disk image, and if you need more space to create more disk images.

- DOS 4.0x supports HDDs up to 4,095MB. It is also supposed to support a primary partition up to 2,047MB and a logical partition of 2,048MB. But creating partitions that large will result in numerous problems, typically in ``FORMAT`` giving a "Divide overflow" error. The solution, assuming your only going to have a single primary partition, is to create a HDD image no larger then 2014MB.

- DOS 4.0x supports the "type 6" FAT16 partition which DOSBox-X's ``IMGMAKE`` creates, but is incompatible with the way the partition is formatted. The DOS 4.0x installer will not offer the option to install to the HDD. And if you manually SYS the drive, it will not boot from it. The solution is to exit to the command line and manually format the C: drive.

## Creating a MS-DOS 4.0x HDD image

In these examples we still use a 32MB HDD.

### Bare-bones install
If you decide to do just an absolute minimal install, and effectively skip the MS-DOS 4.0x install program, you don't need to worry about the buggy MS-DOS 4.0x installer.

```
 IMGMAKE hdd.img -t hd -size 32
 IMGMOUNT 2 hdd.img
```
Now you need to boot from the first MS-DOS 4.0x disk, which is called either Setup or Install depending on the media type.
```
 BOOT SETUP.IMG
```
<img src="images/MS-DOS:MS-DOS_4.01_BOOT_FDD.png" width="640" height="400" alt="Boot MS-DOS 4.01 from Disk"><br>

When at the Welcome screen (3.5" media) or prompted to insert the SELECT disk (5.25" media), simply press ESC instead followed by F3 to drop to the MS-DOS prompt

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER.png" width="640" height="400" alt="MS-DOS 4.01 Installer welcome screen"><br>

<img src="images/MS-DOS:MS-DOS_4.01_INSTALLER_EXIT.png" width="640" height="400" alt="MS-DOS 4.01 Installer exit screen"><br>

and run the following command to format the C: drive and transfer system files:
```
 FORMAT C: /S
```

<img src="images/MS-DOS:MS-DOS_4.01_FORMAT.png" width="640" height="400" alt="MS-DOS 4.01 FORMAT"><br>

The HDD image is now bootable and you can optionally copy some of the DOS utilities from the diskette to the HDD and create your ``CONFIG.SYS`` and ``AUTOEXEC.BAT``. Alternatively if you want to do a full install, you can type ``SELECT MENU`` to return to the installer.

<img src="images/MS-DOS:MS-DOS_4.01_BOOT_HDD.png" width="640" height="400" alt="MS-DOS 4.01 HDD Boot"><br>

### Full install from 3.5" media
Notes
- The MS-DOS 4.0x installer can corrupt its own installation diskettes, as such you should change the permission of the disk images in the host OS such that the image files are READ-ONLY. In turn DOSBox-X will treat them as if the disks have the write-protect set.

- It is required that you first follow the [#bare-bones-install](Bare-bones) install above, up to the point where the DOS partition has been formatted. The alternative is to use the -NOFS flag with ``IMGMAKE`` to create a HDD image that is not partitioned and formatted, and to let MS-DOS 4.0x installer create the partition for you, but this requires that you go through the first phase of the installation process twice, including creating the "SELECT COPY" backup diskette twice.

For this process, it is assumed that you have followed the Bare-bones install process such that your HDD image file is created, partitioned and formatted with MS-DOS 4.0x.

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
You will now be asked between 3 install options. "program workspace" in this context means the amount of RAM available for programs. Based on your decision FASTOPEN will be enabled, and various DOS buffers will be adjusted.

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
Installing PC-DOS 4.0x is easier then MS-DOS 4.0x as it comes on only two 3.5" disks (Install and Operating), or five 5.25" disks.

The same limits on disk and partition sizes seem to apply as MS-DOS 4.0x.

First start by creating a HDD image file, mount it and boot from disk.

```
 IMGMAKE hdd.img -t hd -size 1024 -nofs
 IMGMOUNT 2 hdd.img -size 512,63,2,520 -fs none
 BOOT INSTALL.IMG OPERATING.IMG
```

You can now largely follow the instructions for MS-DOS 4.0x. There will be fewer questions, for instance you will not get the question if you want to install the DOS Shell. After the install is finished and you boot from the HDD image, it will go directly to the DOS Shell program.
