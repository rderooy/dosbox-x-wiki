**Welcome to the DOSBox-X Wiki!**

### Introduction

DOSBox-X is a cross-platform DOS emulator based on [[DOSBox|http://www.dosbox.com]]. Like DOSBox, it emulates a PC necessary for running many MS-DOS games and applications that simply cannot be run on modern PCs and operating systems. However, while the main focus of DOSBox is for running DOS games, DOSBox-X goes much further than this. As a fork of DOSBox, it retains compatibility with the wide base of DOS games and DOS gaming DOSBox was designed for. But it is also a platform for emulating DOS applications, including emulating the environments to run Windows 3.x, 95, 98 and ME and software written for those versions of Windows. DOSBox-X supports multiple operating systems such as Windows, Linux and macOS (MacOS X). Windows binaries (both 32-bit and 64-bit) are released periodically for testing. You can download them from the [[Releases|https://github.com/joncampbell123/dosbox-x/releases]] page.

### DOSBox-X's main focus

Apart from DOSBox's original focus on DOS games, DOSBox-X gives more focus on accurate emulation of the hardware and many more ways to tweak and configure the DOS virtual machine. We believe that a better way to emulate the legacy PC platform is to give the user all the options they need to emulate everything from original IBM PC hardware with 64KB of RAM all the way up to late 90's hardware, whatever it takes to get that game or software package to run. Our goal is to eventually make DOSBox-X a complete emulation package that covers all pre-2000 DOS and Windows 9x based hardware scenarios, including peripherals, motherboards, CPUs, and all manner of hardware that was made for PC hardware of that time.

### DOSBox-X's feature highlights

### What DOSBox-X can do

### Running and configuring DOSBox-X

### Functions of DOSBox-X's GUI menus

DOSBox-X features a GUI menu bar that does not exist in DOSBox. In DOSBox-X, there are 7 menus shown in the menu bar, namely "Main", "CPU", "Video", "Sound", "DOS", "Capture" and "Drive".

**1. The "Main" menu**

* Mapper editor

* Configuration GUI

* Send Key

* Wait on error

* Show details

* Show console

* Capture mouse

* Autolock mouse

* Pause

* Pause with interrupts enabled

* Reset guest system

* Quit

**2. The "CPU" menu**

* Turbo (Fast Forward)

* Normal speed

* Speed up

* Speed down

* Increment cycles

* Decrement cycles

* Edit cycles

* CPU core

* CPU type

**3. The "Video" menu**

* Fit to aspect ratio

* Toggle fullscreen

* Hide/show menu bar

* Reset window size

* Frameskip

* Force scaler

* Scaler

* Output

* Overscan

* Compability

* PC-98

* Debug

**4. The "Sound" menu**

* Increase volume

* Decrease volume

* Mute

* Swap stereo

**5. The "DOS" menu**

* Mouse

* PC-98 PIT master clock

* Swap floppy

* Swap CD

* Rescan all drives

**6. The "Capture" menu**

* Take screenshot

* Capture format

* Record video to AVI

* Record audio to WAV

* Record audio to multi-track AVI

* Record FM (OPL) output

* Record MIDI output

**7. The "Drive" menu**

* A-Z: For each drive, re-scans (refreshes the cache) or un-mounts this drive.

### DOSBox-X's supported commands

Many internal or external MS-DOS commands are supported by DOSBox-X. Also, DOSBox-X offers additional commands such as MOUNT and CAPMOUSE, which are not found in MS-DOS or compatibles. 

* **25/28/50**                              
Changes the DOSBox-X screen to 25/28/50 line mode.
* **A20GATE**                               
Turns on/off or changes the A20 gate mode.
* **APPEND**                              
Enables programs to open data files in specified directories as if the files were in the current directory.
* **BOOT**                              
Starts floppy hard disk images independent of the operating system emulation offered by DOSBox-X.
* **BUFFERS**                              
Displays or changes the CONFIG.SYS's BUFFERS setting.
* **CAPMOUSE**                              
Captures or releases the mouse inside DOSBox-X.
* **CD/CHDIR**                              
Displays or changes the current directory.
* **CHOICE**                              
Waits for a key press and sets ERRORLEVEL. Displays the given prompt followed by [Y,N]? for yes or no response.
* **CLS**                              
Clears the screen of all input and returns just the current prompt in the upper left hand corner.
* **COMMAND**                              
Restarts DOSBox-X's command shell.
* **CONFIG**                              
Starts DOSBox-X's config tool to change it settings.
* **COPY**                              
Copies one or more files.
* **CWSDPMI**                              
Starts CWSDPMI - a 32-bit DPMI server used by various DOS games/applications.
* **DEBUG**                              
The DOS DEBUG tool.
* **DEL/ERASE**                              
Removes one or more files.
* **DEVICE**                              
Load device drivers as CONFIG.SYS's DEVICE command.
* **DIR**                              
Lists available files and sub-directories inside the current directory.
* **DOS32A**                              
Starts DOS32A - a 32-bit DOS extender used by various DOS games/applications.
* **DOS4GW**                              
Starts DOS4GW - a 32-bit DOS extender used by various DOS games/applications.
* **DOSIDLE**                              
Puts the DOS emulator into idle mode for lower CPU usages.
* **DSXMENU**                              
Runs DOSLIB's DSXMENU tool.
* **EDIT**                              
Starts the full-screen file editor.
* **EXIT**                              
Exits from the batch file or DOSBox-X.
* **FCBS**                              
Displays or changes the CONFIG.SYS's FCBS setting.
* **FIND**                              
Prints lines of a file that contains the specified string.
* **HEXMEM16/HEXMEM32**                              
Starts DOSLIB's HEXMEM tool - a memory viewer/dumper.
* **IMGMAKE**                              
Makes floppy drive or hard-disk images.
* **IMGMOUNT**                              
Mount drives from floppy drive, hard-disk, or CD images.
* **INTRO**                              
A full-screen DOSBox introduction.
* **KEYB**                              
Changes the layout of the keyboard used for different countries.
* **LABEL**                              
Changes the label of a drive.
* **LASTDRIV**                              
Displays or changes the CONFIG.SYS's LASTDRIVE setting.
* **LOADFIX**                              
Loads a program above the first 64K of memory.
* **LOADROM**                              
Loads the specified ROM file.
* **LH/LOADHIGH**                              
Loads a program into upper memory (if UMB is available).
* **MD/MKDIR**                              
Makes a directory.
* **MEM**                              
Displays the status of the DOS memory, such as the amount of free memory.
* **MIXER**                              
Displays current sound levels.
* **MODE**                              
Configures DOS system devices.
* **MOUNT**                              
Mounts folders or CD drives.
* **MOUSE**                              
Turns on/off mouse support.
* **MOVE**                              
Moves a file or directory to another location.
* **NMITEST**                              
Runs the NMI testing tool.
* **RD/RMDIR**                              
Removes a directory.
* **RE-DOS**                              
Re-enters to DOSBox-X.
* **REN**                              
Renames one or more files.
* **RESCAN**                              
Refreshes mounted drives by clearing their caches. 
* **SET**                              
Displays and sets environment variables.
* **SHOWGUI**                              
Starts DOSBox-X's configuration GUI dialog, where you can review or change its settings.
* **TREE**                              
Graphically displays the directory structure of a drive or path.
* **TYPE**                              
Displays the contents of a text-file.
* **VER**                              
Views and sets the reported DOS version. Also displays the running DOSBox-X version.
* **VESAMOED**                              
Runs the VESA BIOS mode editor utility.
* **VFRCRATE**                              
Runs the Video refresh rate tool.
* **XCOPY**                              
Copies files and directory trees.

### DOSBox-X's command-line options

DOSBox-X supports command-line options. You can start DOSBox-X without any option, or with any of the following options.

* **-h** or **-help**                              
Shows DOSBox-X's help message.
* **-editconf [program]**                             
Calls program with as first parameter the configuration file. You can specify this command more than once. In this case it will move to second program if the first one fails to start.
* **-opencaptures [program]**                              
Calls program with as first parameter the location of the captures folder.                        
* **-opensaves [program]**                              
Calls program with as first parameter the location of the saves folder.
* **-eraseconf**                              
Erases DOSBox-X's default config file.
* **-resetconf**                              
Erases DOSBox-X's default config file.
* **-printconf**                              
Generates DOSBox-X's config file in the user directory and prints its location.
* **-erasemapper**                            
Erases the mapper file used by the default clean configuration file.
* **-resetmapper**                            
Erases the mapper file used by the default clean configuration file.
* **-console**                                
Starts DOSBox-X with the console window (win32 only).
* **-noconsole**                              
Starts DOSBox-X without showing the console window (debug+win32 only).
* **-nogui**                                  
Starts DOSBox-X without showing its GUI menu (win32 only).
* **-nomenu**                                 
Starts DOSBox-X without showing its GUI menu (win32 only).
* **-userconf**                               
Loads the configuration from the user's profile or home directory.
* **-conf [file]**                           
Uses the specified file as DOSBox-X's config file.
* **-startui** or **-startgui**                      
Starts DOSBox-X with its configuration GUI dialog, where you can review or change its settings.
* **-startmapper**                            
Starts DOSBox-X and enters to the mapper directly.
* **-showcycles**                             
Show cycles count (FPS) on the DOSBox-X title bar.
* **-showrt**                                 
Show emulation speed relative to realtime on the DOSBox-X title bar.
* **-fullscreen**                             
Start DOSBox-X in full-screen mode.
* **-savedir [path]**                         
Uses the specified path as DOSBox-X's save path.
* **-disable-numlock-check**                  
Disables numlock check (win32 only).
* **-date-host-forced**                       
Forces synchronization of date with the host system.
* **-debug**                                  
Sets all logging levels to debug.
* **-early-debug**                            
Logs early initialization messages in DOSBox (this option implies -console).
* **-keydbg**                                 
Logs all SDL key events (debugging).
* **-lang [message file]**                    
Uses specific message file instead of language= setting.
* **-nodpiaware**                             
Ignores (don't signal) Windows DPI awareness.
* **-securemode**                             
Enables DOSBox-X's secure mode. The [autoexec] section of the loaded configuration file will be skipped, and commands such as MOUNT and IMGMOUNT are disabled.
* **-noautoexec**                             
Skips the [autoexec] section of the loaded configuration file.
* **-exit**                                   
Exit after executing the [autoexec] section of the loaded configuration file.
* **-c [command string]**                              
Execute this command in addition to the [autoexec] section of the loaded configuration file. Make sure to surround the command in quotes to cover spaces.
* **-break-start**                              
Starts DOSBox-X and breaks into its debugger directly.
* **-time-limit [n]**                              
Starts and terminates DOSBox-X after 'n' seconds.
* **-fastbioslogo**                              
Skips the 1-second BIOS pause with Fast BIOS logo.
* **-log-con**                              
Logs CON output to a log file.

### Frequently asked questions (FAQ)
