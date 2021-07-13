The XenServer Windows Installer Packages
==========================================

The XenServer windows installer packages consists of

6 MSIs for installing 32 bit and 64 bit versions of

*    The XenServer Windows Guest Agent
*    The XenServer Windows Paravirtualized Drivers
*    The XenServer Windows Volume Shadow Copy Service Provider

An installwizard service for handling automated updates and installations of the tools 
(which internally used the correct MSIs from the list above)

A 32 bit MSI for installing and starting the installwizard service

Quick Start
===========

Prerequisites to build
----------------------

*   Visual Studio 2012 or later 
*   Python 3 or later 
*   WIX (Windows Installer XML) Version 3.5

Environment variables used in building the installer
----------------------------------------------------

BUILD\_NUMBER Build number

WIX location of the WIX binaries

VS location of visual studio

Commands to build
-----------------

To build the installer, first construct a package output directory containing a 
subdirectory for each of the other windows tools projects.  The subdirectories should be 
named

*  xenbus
*  xenguestagent
*  xeniface
*  xenvif
*  xennet
*  xenvbd
*  xenvss

Each subdirectory should have the relevent build output of it's associated component
copied inside.  The expected tree looks like:

        directory\xenvif\{x86,x64}\xenvif.sys
        directory\xenvbd\{x86,x64}\xenvbd.sys
        directory\xenvbd\{x86,x64}\xencrsh.sys
        directory\xenvbd\{x86,x64}\xendisk.sys
        directory\xennet\{x86,x64}\xennet.sys
        directory\xeniface\{x86,x64}\xeniface.sys
        directory\xeniface\{x86,x64}\xenagent.exe
        directory\xeniface\{x86,x64}\liteagent.exe
        directory\xenbus\{x86,x64}\xenbus.sys
        directory\xenbus\{x86,x64}\xen.sys
        directory\xenbus\{x86,x64}\xenfilt.sys
        directory\xenbus\{x86,x64}\xenbus_monitor.exe

Then use the following commands

    git clone http://github.com/xenserver/win-installer
    cd win-installer
    .\build.py --local <build output directory>

To sign the drivers with a certificate installed on the build machine, the 
following additional arguments can be placed after the build output directory 
in the .\build.py command

    --sign <certificate name> 
        Sign with the best certificate matching <certificate name>
    
    --addcert <certificate file> 
        Add an aditional <certificate file> to the signature block

Alternatively a user specified commandline (to which the name of the file
to be signed is appended) can be specifed as follows

    --signcmd <full command line for signing tool>

