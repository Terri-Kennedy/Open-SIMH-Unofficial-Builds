# Open SIMH Unofficial Builds
These are unofficial builds of the Open-SIMH emulator package.

Open-SIMH does not appear to publish official builds of their emulators on their GitHub repo, so I've built a few different versions here.

The incentive for this was an offhand comment of mine that Open-SIMH was a kind of "trial by fire" as you had to build the emulators yourself before you could use them to emulate classic computers, or risk downloading possibly questionable files from possibly questionable sites. Someone suggested "So, why don't you make and publish your own builds?" Here they are. Binary packages with all emulators are available for:
- Windows 10 32-bit (x86)
- Windows 10 64-bit (amd64)
- Windows XP 32-bit (x86)
- FreeBSD 13 64-bit (amd64)
- Debian 12/Bookworm (amd64)
- Raspberry Pi OS Bookworm 32-bit (armhf)
- Raspberry Pi OS Bookworm 64-bit (aarch64)

These are currently based on Open-SIMH GitHub commit 6e9324e09f4f364346310de34849077c986c29f2

# Notes
- The only emulators that have been thoroughy tested on all platforms are the microvax3900 and pdp11 binaries. If you run into any problems with any of these binaries, please open an issue here and I'll look into it.
- The emulators are provided as dynamically-linked executables, so you may need to install additional libraries on yout target system. As above, open an issue here if anything is unclear.
- All emulators for a given platform are bundled together, in a .zip file for Windows and a .tgz file for all other platforms.

# Information about making your own builds for specific platforms
Most platforms were built simply by installing the prerequisite libraries and typing "make". Additional information for FreeBSD and Windows follow below:

# FreeBSD
The "Makefile" and "distinfo" files here are copied to the /usr/ports/emulators/open-simh directory on FreeBSD. This upgrades the existing FreeBSD port to use the latest version from the Open-SIMH development tree. Then just use "make; make install; make clean" as usual for a FreeBSD port.

# Windows
Building on Windows is substantially more complex. The following are the steps I used to build on Windows. Note that the build environment I used was 64-bit, regardless of whether I was building 32-bit or 64-bit Windows binaries:
- Install Visual Studio Community 2019 from https://download.visualstudio.microsoft.com/download/pr/e84651e1-d13a-4bd2-a658-f47a1011ffd1/e17f0d85d70dc9f1e437a78a90dcfc527befe3dc11644e02435bdfe8fd51da27/vs_Community.exe using the provided .vsconfig file.
- Install Git 2.51.0(2) from https://github.com/git-for-windows/git/releases/download/v2.51.0.windows.2/Git-2.51.0.2-64-bit.exe
- Install 7Zip 25.01 from https://www.7-zip.org/a/7z2501-x64.msi
- Install CMake 3.31.9 from https://github.com/Kitware/CMake/releases/download/v3.31.9/cmake-3.31.9-windows-x86_64.msi
- Run Developer PowerShell for VS 2019 as Administrator from the Start Menu
- Type "Set-ExecutionPolicy UnRestricted" and answer "A" 
- Type "mkdir C:\Temp"
- Type "cd C:\Temp"
- Type "git clone https://github.com/open-simh/simh.git"
- Type "xcopy cmake-builder.ps1 C:\temp\simh\cmake" (fixes broken 64-bit build under VS 2019)
- Type "cd simh"
- Type "Start-Transcript -Path C:\Temp\simh-build-log.txt"
- Type "cmake\cmake-builder.ps1 -flavor vs2019 -config Release" (for Windows 10 32-bit)
- Type "cmake\cmake-builder.ps1 -flavor vs2019-x64 -config Release" (for Windows 10 64-bit)
- Type "cmake\cmake-builder.ps1 -flavor vs2019-xp -config Release" (for Windows XP compatibility)
- [sit and wait]
- Type "Stop-Transcript"

# Code Authenticity
There is an "About.exe" in this repo which is a Windows executable signed with my Windows Code Signing Certificate. That proves that this repository is owned by the same person (me) that holds the Windows Code Signing Certificate, which should reduce any worries about downloading any of the emulators from here. This will only run on Windows, and when you run it, it will provide instructions on how to view the certificate the "About.exe" was signed with. There is no equivalent function for non-Windows platforms, but hopefully it will help alleviate any worries you have about the authenticity of any of the builds here.

# Credit
The official Open-SIMH repository can be found at https://github.com/open-simh/simh

All I did was provide pre-compiled binaries for various platforms.
