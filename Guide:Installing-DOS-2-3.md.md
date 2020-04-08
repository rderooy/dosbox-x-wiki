## Overview
- Key new features of DOS 2.00:
  - First version to support HDDs (still using FAT12)
  - First version to support directories
  - First version to support redirection (pipes)
  - First version to support TSRs
  - First version to support installable device drivers
  - First version to introduce CONFIG.SYS
  - First to support 5.25" 9-sector 180KB (SSDD) and 360KB disks (DSDD)
- Key new features of DOS 3.00:
  - Maximum partition size of 32MB (using the new FAT16)
  - First version to support 5.25" 1.2MB disks (HD)
  - First version to support the AT internal clock
- Key new features of DOS 3.10:
  - ???
- Key new features of DOS 3.20:
  - First version to support 3.5" 720kB disks (2DD)
- Key new features of DOS 3.30:
  - First version to support the MBR partitioning scheme with primary, extended and logical partitions
  - First version to support HDDs up to 504MB (partitions still limited to 32MB)
  - First version to support 3.5" 1.44MB disks (HD)

This applies to
- Microsoft MS-DOS 3.21
- Microsoft MS-DOS 3.30
- IBM PC-DOS 2.00
- IBM PC-DOS 2.10
- IBM PC-DOS 3.00
- IBM PC-DOS 3.10
- IBM PC-DOS 3.20
- IBM PC-DOS 3.30

External links
- http://www.os2museum.com/wp/dos/dos-2-0-and-2-1/
- http://www.os2museum.com/wp/dos/dos-3-0-3-2/
- http://www.os2museum.com/wp/dos/dos-3-3/

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
## Creating a DOS 2.0-3.21 HDD image

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
- DOS 3.3 introduced the MBR partitioning scheme with primary, extended and logical partitions, that was used for all later DOS versions. However, DOSBox-X has only limited support for extended and logical partitions. You can create them, and when you boot your DOS image, you can access them. But when you ``IMGMOUNT`` the image in DOSBox-X, the integrated DOS will only be able to access the primary partition.
- The maximum HDD size is now 504MB, but the maximum partition size is still only 32MB. Since DOSBox-X has only limited support for extended and logical partitions, it is recommended that you only create a single primary partition up to 32MB per HDD image. If you need multiple drives, you can create multiple images.
- After you have created your image, due to the newer style partition layout, which DOSBox-X can autodetect, you do not have to specify the geometry to mount the image. So your can boot from the HDD image with the following commands instead.
- Partitioned and formatted images created with IMGMAKE are not recognised by DOS 3.3. Presumably this is because IMGMAKE sets the partition type to type 6 (FAT 16), while DOS 3.3 expects type 4 (FAT 16 < 32M). As such you need to use the -NOFS switch like with earlier DOS versions and manually create the partitions and format them.

```
IMGMOUNT C hdd.img
BOOT -L C
```

<img src="images/MS-DOS:MS-DOS_3.3_BOOT_HDD.png" width="640" height="400" alt="Boot MS-DOS 3.3 from HDD"><br>