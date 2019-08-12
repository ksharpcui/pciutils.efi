pciutils.efi
===
**pciutils.efi/PciUtilsPkg** is a UDK/EDK2 porting of the GNU's [pciutils](https://github.com/pciutils/pciutils) for the handy PCI tools: `lspci` and `setpci`<br>
As a full UDK package, **PciUtilsPkg** can be built using either [the stander EDK II build process](https://edk2-docs.gitbooks.io/edk-ii-build-specification/) or [iPug](https://github.com/timotheuslin/ipug).


## Prerequisites:
1. Python 2.7.10+ or Python 3.7.0+
2. git 2.19.0+
3. UDK/EDK2 code tree in following tags: edk2-stable{201811, 201903, 201905}


## Generic prerequisites for the UDK porting:
1. nasm (2.0 or above)
2. iasl (version 2018xxxx or later, maybe optional)
3. MSVC(Windows) or Xcode(Mac) or GCC(Open-source Posix)
4. build-essential uuid-dev (Posix)
5. pip2 install future (Python 2.7.x)
6. motc (Xcode)
0. Reference:
    - [Getting Started with EDK II](https://github.com/tianocore/tianocore.github.io/wiki/Getting%20Started%20with%20EDK%20II) 
    - [Xcode](https://github.com/tianocore/tianocore.github.io/wiki/Xcode)


## Tools installation for any Debian-Based Linux:
- `$ sudo apt update; sudo apt install nasm iasl build-essential uuid-dev`
- optional when using iPug
    - `pip install ipug --user`


## Known issues:
1. Only Linux (Debian & Arch) and Windows build are tested. Xcode is not covered yet.
2. "pci.ids" database is not working yet.
3. The double/triple/quadruple command with {'x', 'm', 'v' ...} may not work correctly.
4. UDK with Python3 has build-dependency issue which causes slow re-building. Python2 is still recommended anyway.


## Build using iPug (Optional) :
0. Change-directory to folder **pciutils.efi** .
1. (Optional) Edit `CODETREE` in `project.py` to specify where to place the downloaded source files of the UDK git repo or any other additional respos.
2. To build the code, run `python project.py`. (iPug will then handle all the rest of the tedious works with the UDK code tree steup and the build process.)
3. Browse to folder **Build/PciUtilsPkg** for the build results.
4. Browse to folder **Build/Pug/Conf** for CONF_PATH setting files.
5. Run `python project.py {clean, cleanall}` to clean (all) the intermediate files.
6. For the 1st time setup, following code trees are automatically git-cloned:
    - [the UDK code tree](https://github.com/tianocore/edk2)
    - the openssl repo (and some other CryptoPkg's submodules maybe)
    - [the edk2-libc code tree](https://github.com/tianocore/edk2-libc) -- UDK newer than edk2-stable201905 needs this for StdLib package.
    - [the GNU pciutils source](https://github.com/pciutils/pciutils)


## Tech notes with iPug (Optional) :
1. The full [UDK code tree](https://github.com/tianocore/edk2) is git-cloned-checked-out to:
    - Windows: %USERPROFILE%/.cache/pug/edk2
    - Linux:  $HOME/.cache/pug/edk2
2. On Windows, the default MSVC tool chain tag is vs2012x86. The following command should be run first in the command console:
    - "C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x86
3. **pciutils.efi**, as the current working directory, is assigned as the "WORKSPACE" directory. **PACKAGES_PATH a.k.a. MULTIPLE-WORKSPACE** is used here to implicitly reference other standard packages outside the current working directory tree.


## Have Fun!
