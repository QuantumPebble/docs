# Getting started with Non-Acrcade/Software Emulation in Libretro MAME/MESS cores

In this chapter, the terms 'software' and 'software lists' are used to define non-arcade machines that are emulated by MAME/MESS. This kind of emulation requires a different planning approach than arcade machine emulation - it is more complicated to set up.

## Understand the core variants

The libretro core ecosystem currently includes many multi software emulators that support software emulation. Three families exist: MAME, MESS and UME. These emulators are in turn available in multiple versions to allow users to best match a core to their preference.

#### MAME
Arcade (MAME) & Arcade (MAME 2016) are currently the only MAME cores that support the emulation of both software & arcade systems. The Arcade (MAME) core is updated regularly and most inline with the official MAME project release. Arcade (MAME 2016) is an archived snapshot of MAME from the 0.174 release.

#### MESS
Multi (MESS 2015) is a snapshot of the MESS project from v0.160. The MESS project later merged with the MAME project in MAME v0.162, i.e. in May 2015.

#### UME
Multi (UME 2015) is a snapshot of the Universal Machine Emulator. This was a precursor to the MAME/MESS merger, released by David Haywood (haze). The MAME and MESS project codebases co-existed in the MESS SVN development tree before they officially merged. This allowed haze to build and release the emulator with unmodified code from both projects under the name UME.

## Use the correct version of romset for the desired emulator
  
Arcade (MAME), Arcade (MAME 2016) will be the main focus of this guide but also the MULTI (MESS 2015) and MULTI (UME 2015) cores have this ability. As in MAME arcade emulation, each core requires its own distinct version of software list "romsets", which the emulator supports.

| Emulator | Required ROM Version |
| :---: | :---: |
| MAME 2016 | MAME 0.174 |
| MAME (latest version) | MAME (latest version) |
| MESS 2015 | - |
| UME 2015 | - |

!!! tip
    For best results, start with a full software list ROM collection with a version that matches the emulator you are using. Individual romset zip files may not include BIOS ROMs, "Parent" romsets, necessary audio sample files, etc.
    Matching emulator and game versions is advised for maximum compatibility, but you may find mis-matched combinations also work.
    
---

## Running software list machines
There are two ways of configuring Retroarch to launch software list machines and games with MAME cores.

  1. **Method 1 - MAME Frontend direct launch:** uses the inbuilt MAME logic and hash files to launch your games
  2. **Method - RetroArch fontend friendly via Libretro CMD file launch:** uses an extra libretro feature to pass command line functions to the core 

### Method 1: MAME Frontend direct launch

For using the internal software list functions of MAME, you will need the right supporting files from the mainline MAME standalone emulator, i.e. the **hash files**. E.g. for the MAME (current) core, download the newest version of the Windows MAME emulator [here](https://www.mamedev.org/release.html). For earlier versions, make sure to get the correct version you require: The version of the hash files must match with the Libretro Core version.

!!! tip
    In RetroArch, launch the desired core standalone, and on the bottom left, you find the correct MAME version that you want to download.

Extract the contents and take the “hash” folder. Move this folder into the RetroArch folder structure. If your device has limited storage, just copy the hash files relating to the system you want to emulate.

**RetroArch MAME system folder structure:**
Folder structure/naming is very important here. The naming will depend on the machine you are trying to emulate but the folder structure will be the same. The example below is for the Atari 7800 system in MAME current.

“YourPath” is the location of your Retroarch system folders. It varies depending on your operating system.
!!! tip
    In RetroArch, head for Settings/Directory - the System/BIOS entry identifies the correct "system" folder.

If not already existent, create the following folder in your RetroArch “system” folder:
"YourPath"/Retroarch/System/mame

Copy the hash folder acquired earlier into the RetroArch system folder:
"YourPath"/Retroarch/system/mame/hash

So for Atari 7800 you would have the following hash file:
YourPath/Retroarch/system/mame/hash/a7800.xml

(To do: check about .hsi file or use another example)

**RetroArch MAME games folder structure:**
Create the following folders in your games directory of your choice (these will be mame naming dependent)
"YourPath"/Games/Atari 7800/a7800
(The last folder MUST be named as MAME requires, in this case “a7800”)

Place any .zip games and .zip bios files required here:
"YourPath"/Games/Atari 7800/a7800.zip
"YourPath"/Games/Atari 7800/a7800/asteroid.zip

!!! note
    To place the bios file above a7800 is the way that official MAME stores the data and thus also recommended here. You could also put the bios into the a7800 folder, but that's not how official MAME does it. 

You may also put or even extract the bios file to their own folder within the games directory
"YourPath"/Games/Atari 7800/a7800/a7800/7800.rom

Now launch the game: In RetroArch, choose "Load Content" and browse to asteroid.zip and launch with MAME current.

(To Do: Add note about SoftList xml specifying the game names and crc and only supporting only those specific file names.)

### Method 2: RetroArch frontend friendly via Libretro CMD file launching  

This method follows the same folder structure as above, but you can use custom naming outside of the hash file included with MAME. It utilises some custom additions to the Libretro MAME Cores. Specifically the use of text files (.cmd) to replicate sending command line actions as you can with mainline MAME.

**Creating a .cmd file**
Let's follow the above example and create a dedicated asteroid.cmd file for the Atari 7800 game. It needs this line:

a7800 -cart asteroid -rp "/"YourPath"/mame/roms/a7800"

To do: Other path definitions, e.g. under Windows?

Now launch the game: In RetroArch, choose "Load Content" and browse to asteroid.cmd, and it should launch with MAME current.

To do: Cmd file example

