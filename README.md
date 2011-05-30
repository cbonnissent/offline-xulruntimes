This package is a wrapper to download and install the third-party
tarball containing the XUL runtimes for the supported OS/platforms.

The runtimes tarball is constructed by hand and has the following
structure:

    linux/i686/xulrunner/*
    linux/x86_64/xulrunner/*
    mac/universal/XUL.framework/*
    win/32/xulrunner/*

# Fetch and extract the runtimes files

## Linux

Download the official runtimes from the releases.mozilla.org site,
and unpack the `xulrunner' subdir.

    $ mkdir -p linux/i686
    $ ( cd linux/i686 && wget -q -O- http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/2.0/runtimes/xulrunner-2.0.en-US.linux-i686.tar.bz2 | tar jxf - )

    $ mkdir -p linux/x86_64
    $ ( cd linux/x86_64 && wget -q -O- http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/2.0/runtimes/xulrunner-2.0.en-US.linux-x86_64.tar.bz2 | tar jxf - )

## Windows

Idem.

    $ mkdir -p win/32
    $ wget http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/2.0/runtimes/xulrunner-2.0.en-US.win32.zip
    $ ( cd win/32 && unzip ../../xulrunner-2.0.en-US.win32.zip )
    $ rm xulrunner-2.0.en-US.win32.zip

## Mac

Download the official runtime and extract the `XUL.framework' dir from
the Archive.pax.gz file:

    $ mkdir -p mac/universal
    $ wget http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/2.0/runtimes/xulrunner-2.0.en-US.mac-pkg.dmg
    $ mkdir mnt_xul
    $ hdiutil -attach xulrunner-2.0.en-US.mac-pkg.dmg -mountpoint mnt_xul
    $ gzip -dc mnt_xul/xulrunner-2.0.en-US.mac.pkg/Contents/Archive.pax.gz | ( cd mac/universal && cpio -id )
    $ umount mnt_xul
    $ rmdir mnt_xul
    $ rm xulrunner-2.0.en-US.mac-pkg.dmg

# Re-pack the runtimes

    $ GZIP=-9 tar zcf dynacase-offline-xulruntimes-2.0.tar.gz linux mac win

