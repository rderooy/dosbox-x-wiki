<img src="images/Demoscene:CNCD-vs-Orange-by-CNCD-and-Orange-(1997).gif" width="640" height="400"><br>
[[1997|Guide:MS-DOS:demoscene:1997]] demoscene entry.

# Demo description

(todo)

# Recommended DOSBox-X configuration

    [dosbox]
    memsize=16
    machine=svga_s3
    
    [cpu]
    cycles=max    # set to 250000 if you want to capture instead
    core=dynamic
    cputype=pentium
    
    [sblaster]
    sbtype=sb16
    
    [gus]
    gus=true

GUS emulation should be enabled so the demo can automatically choose it for best music audio quality. The high cycles count is needed for the 3D objects and effects used in the demo. If you only want to watch the demo instead, you should consider cycles=max instead.

The demo will not start immediately. It needs to load some data first and process it, which can take 30-60 seconds in DOSBox-X on a quad core Intel i5 laptop.

# More information

[More information (Pouet)](http://www.pouet.net/prod.php?which=1326)