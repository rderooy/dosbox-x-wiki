## Creating a DOS 5.00-6.30 HDD image
This applies to
- MS-DOS 5.00
- MS-DOS 5.00a
  - Fixes a data corruption bug (CHKDSK and UNDELETE can in some cases cause corruption, alternatively use the "PD0646" patch).
- PC-DOS 5.00
- PC-DOS 5.02
  - Adds ISO screen fonts
  - Adds Eject utility for lockable media
  - Adds APM Power management
  - Adds file transfer utility

DOS 5 is the last version that Microsoft and IBM shared code for, and later PC-DOS and MS-DOS versions diverge from here on. Both IBM and Microsoft started selling their respective DOS versions directly to the general public. IBM marketed it "For IBM and IBM Compatibles", while Microsoft simply said "for DOS systems". There are also no other OEM versions of DOS 5 or later, as all PCs at this point where fully IBM Compatible. Microsoft and IBM also started to leapfrog each other with version numbers, so that it would appear their respective version was newer. This would continue until Windows 95 was released, and Microsoft lost interest in launching new stand-alone DOS versions.

Starting with DOS 5.00, installing DOS in DOSBox-X is much more straight forward, as you can have ``IMGMAKE`` create a HDD image that is already partitioned and formatted.

Maximum HDD size has increased to 7.84GB, but the maximum partition size is basically still 2GB, which is a FAT16 limitation.

Note: these instructions assume the "Full" version and not the "Upgrade" release.

```
 IMGMAKE hdd.img -t hd -size 2048
 IMGMOUNT 2 hdd.img
 BOOT DISK1.IMG DISK2.IMG DISK3.IMG
```

When prompted to change disk, on the DOSBox-X menu bar select "DOS" followed by "Swap disk". After the installation is finished, from the DOSBox-X menu bar select "Main" followed by "Reset guest system" and you will be back at the DOSBox-Z ``Z:\>`` prompt.

You can now boot these DOS versions directly from the HDD image as follows:
```
IMGMOUNT C hdd.img
BOOT -L C
```
