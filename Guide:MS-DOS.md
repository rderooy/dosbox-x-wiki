independently# PC-DOS and MS-DOS Installation Guide

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
- https://en.wikipedia.org/wiki/MS-DOS
- https://en.wikipedia.org/wiki/IBM_PC_DOS
- https://en.wikipedia.org/wiki/Timeline_of_DOS_operating_systems
- The MS-DOS Encyclopedia (DOS 1.0-3.3) [[https://pcjs.org/documents/books/mspl13/msdos/encyclopedia/]]
- DOS memory management - [[https://www.vogonswiki.com/index.php/DOS_memory_management]]
- CD-ROM driver help - [[https://www.computerhope.com/cdromd.htm]]
- How to get a mouse to work in MS-DOS - [[https://www.computerhope.com/issues/ch000007.htm]]

## General guidelines
These pages assume that you have PC-DOS or MS-DOS diskette images. Getting these image files is outside the scope of this document.

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
  - First version to allow HDDs up to 4,095MB and larger partitions
  - First version to included HIMEM.SYS XMS 2.x driver with support for up to 16MB RAM
- DOS version 5.0
  - First version to support 3.5" 2.88MB disks (ED)
  - First version to support HDDs up to 7.84GB with 2GB partitions

#### DOS versions - divergence
DOS 5 is the last version for which Microsoft and IBM shared code. From this point, Microsoft MS-DOS and IBM PC-DOS are developed independantly and start to diverge.

##### Microsoft MS-DOS 6+
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

##### IBM PC-DOS 6+
- PC-DOS version 6.1
- PC-DOS version 6.3
- PC-DOS version 7.0 / 2000
  - Introduces XDF diskettes
- PC-DOS version 7.1
  - Adds support for LBA and FAT32

### DOS editions
MS-DOS was licensed by many clone manufacturers and in the early days these OEM editions were 'personalized' to the manufacturer, and therefore many of these early OEM specific editions don't work, or only work partially in DOSBox-X. Because of this, up to DOS version 3.2, it is typically easier to use the IBM PC-DOS versions in DOSBox-X.

## Booting DOS from diskettes
Booting DOS from a diskette image is pretty straight forward. Start DOSBox-X and you should find yourself at the DOSBox-X ``Z:\>`` prompt. This is not a real DOS, but a 'simulated' DOS that is compatible with most DOS games and applications. Now type something equivalent to
```
 BOOT dos.img
```
Assuming that dos.img is an uncompressed DOS disk image in IBM-MFM format (typically with an file extension of .IMG or .IMA), in your current working directory, it should start it. This even works for IBM PC-DOS 1.00.

<img src="images/MS-DOS:PC-DOS_1.0.png" width="640" height="400" alt="Booting a PC-DOS 1.00 diskette image"><br>

* [[Guide: Installing DOS 2.00-3.x in DOSBox-X|Guide:Installing-DOS-2-3.md]]
* [[Guide: Installing DOS 4.0x in DOSBox-X|Guide:Installing-DOS-4.md]]
* [[Guide: Installing DOS 5.0x in DOSBox-X|Guide:Installing-DOS-5.md]]
