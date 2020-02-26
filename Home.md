Welcome to the DOSBox-X wiki!

DOSBox-X is a cross-platform DOS emulator based on [[DOSBox|http://www.dosbox.com]]. Like DOSBox, it emulates a PC necessary for running many MS-DOS games and applications that simply cannot be run on modern PCs and operating systems. However, while the main focus of DOSBox is for running DOS games, DOSBox-X goes much further than this. As a fork of DOSBox, it retains compatibility with the wide base of DOS games and DOS gaming DOSBox was designed for. But it is also a platform for emulating DOS applications, including emulating the environments to run Windows 3.x, 95, 98 and ME and software written for those versions of Windows. DOSBox-X supports multiple operating systems such as Windows, Linux and macOS (MacOS X). Windows binaries (both 32-bit and 64-bit) are released periodically for testing. You can download them from the [[Releases|https://github.com/joncampbell123/dosbox-x/releases]] page.

== DOSBox-X's main focus ==

Apart from DOSBox's original focus on DOS games, DOSBox-X gives more focus on accurate emulation of the hardware and many more ways to tweak and configure the DOS virtual machine. We believe that a better way to emulate the legacy PC platform is to give the user all the options they need to emulate everything from original IBM PC hardware with 64KB of RAM all the way up to late 90's hardware, whatever it takes to get that game or software package to run. Our goal is to eventually make DOSBox-X a complete emulation package that covers all pre-2000 DOS and Windows 9x based hardware scenarios, including peripherals, motherboards, CPUs, and all manner of hardware that was made for PC hardware of that time.

== DOSBox-X's feature highlights ==

== What DOSBox-X can do ==

== Running and configuring DOSBox-X ==

== Functions of DOSBox-X's GUI menu ==

== DOSBox-X's supported commands ==

* 25/28/50
* A20GATE
* APPEND
* BOOT
* BUFFERS
* CAPMOUSE
* CD/CHDIR
* CHOICE
* CLS
* COMMAND
* CONFIG
* COPY
* CWSDPMI
* DEBUG
* DEL/ERASE
* DEVICE
* DIR
* DOS32A
* DOS4GW
* DOSIDLE
* DSXMENU
* EDIT
* EXIT
* FCBS
* FIND
* HEXMEM16/HEXMEM32
* IMGMAKE
* IMGMOUNT
* INTRO
* KEYB
* LABEL
* LASTDRIV
* LOADFIX
* LOADROM
* LH/LOADHIGH
* MD/MKDIR
* MEM
* MIXER
* MODE
* MOUNT
* MOUSE
* MOVE
* NMITEST
* RD/RMDIR
* RE-DOS
* REN
* RESCAN
* TREE
* TYPE
* SET
* SHOWGUI
* VER
* VESAMOED
* VFRCRATE
* XCOPY

== DOSBox-X's command line options ==

* -h or -help                              
Show help message
* -editconf                              
Launch editor
* -opencaptures <param>                              
Launch captures                              
* -opensaves <param>                              
Launch saves
* -eraseconf                              
Erase config file
* -resetconf                              
Erase config file
* -printconf                              
Print config file location
* -erasemapper                            
Erase mapper file
* -resetmapper                            
Erase mapper file
* -console                                
Show console (win32)
* -noconsole                              
Don't show console (debug+win32 only)
* -nogui                                  
Don't show gui (win32 only)
* -nomenu                                 
Don't show menu (win32 only)
* -userconf                               
Create user level config file
* -conf <param>                           
Use config file <param>
* -startui -startgui                      
Start DOSBox-X with UI
* -startmapper                            
Start DOSBox-X with mapper
* -showcycles                             
Show cycles count
* -showrt                                 
Show emulation speed relative to realtime
* -fullscreen                             
Start in fullscreen
* -savedir <path>                         
Save path
* -disable-numlock-check                  
Disable numlock check (win32 only)
* -date-host-forced                       
Force synchronization of date with host
* -debug                                  
Set all logging levels to debug
* -early-debug                            
Log early initialization messages in DOSBox (implies -console)
* -keydbg                                 
Log all SDL key events (debugging)
* -lang <message file>                    
Use specific message file instead of language= setting
* -nodpiaware                             
Ignore (don't signal) Windows DPI awareness
* -securemode                             
Enable secure mode
* -noautoexec                             
Don't execute AUTOEXEC.BAT config section
* -exit                                   
Exit after executing AUTOEXEC.BAT
* -c <command string>                              
Execute this command in addition to AUTOEXEC.BAT. Make sure to surround the command in quotes to cover spaces.
* -break-start                              
Break into debugger at startup
* -time-limit <n>                              
Kill the emulator after 'n' seconds
* -fastbioslogo                              
Fast BIOS logo (skip 1-second pause)
* -log-con                              
Log CON output to a log file

== Usage tips and remarks ==

== Frequently asked questions (FAQ) ==
