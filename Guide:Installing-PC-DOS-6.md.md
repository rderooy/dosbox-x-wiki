This applies to
- PC-DOS 6.10
  - E replaces EDIT
  - Includes disk utilities from Central Point Software
  - Includes IBM Antivirus
- PC-DOS 6.30
  - Includes Addstor SuperStor disk compression software

## Creating a PC-DOS 6.x HDD image

```
 IMGMAKE hdd.img -t hd -size 2048
 IMGMOUNT C hdd.img
 BOOT DISK1.IMG DISK2.IMG DISK3.IMG
```

When prompted to change disk, on the DOSBox-X menu bar select "DOS" followed by "Swap disk". After the installation is finished, from the DOSBox-X menu bar select "Main" followed by "Reset guest system" and you will be back at the DOSBox-X ``Z:\>`` prompt.

You can now boot these DOS versions directly from the HDD image as follows:
```
IMGMOUNT C hdd.img
BOOT -L C
```
