1. Your Droid must be rooted, if it isn't follow these directions.

> http://forum.xda-developers.com/showthread.php?t=597175

2. You need to have busybox installed and the busybox links generated.
If you don't, try this:

> i)  Download busybox from
http://code.google.com/p/get-a-robot-vpnc/downloads and tranfer it to
your sdcard
> ii)  Go to the command line on your Droid, either using 'adb
shell' from your computer or from a terminal program like ConnectBot
> iii)  issue the su command to get root access
> iv)  change your system partition from read only to writable
    1. mount -o remount,rw /dev/block/mtdblock4 /system
> v)  check if the directory /system/xbin exists.  If it does not create it
    1. mkdir /system/xbin
    1. hmod 755 /system/xbin
> vi) change the the xbin directory
    1. cd /system/xbin
> vii) copy the busybox program to this location and make it executable
    1. dd if=/sdcard/busybox of=./busybox
    1. chmod 755 ./busybox
> viii)  install the busybox links
    1. ./busybox -install .
> > If you get a series of error messages that say "Invalid
cross-device link" you are probably using an older version of busybox.

> Use 1.15.2 or greater.

3. Install the kernel module tun.ko to enable network tunneling.  The
"tun.ko" module and instructions were contributed by Jon Tomaszewski

> i)  Download tun.ko from
http://code.google.com/p/get-a-robot-vpnc/downloads and tranfer it to
your sdcard
> ii)  If you are doing this directly after installing busybox, then
you already have root access and have remounted the system partition.
If not, do steps ii, iii, and iv above.
> iii)  cp /sdcard/tun.ko /system/lib/modules/
> iv)  set the system partition back to read only
    1. mount -o remount,ro /dev/block/mtdblock4 /system

4. Install VPN\_Connections\_v096.apk or newer.  It can be installed
from the market or downloaded from
http://code.google.com/p/get-a-robot-vpnc/downloads and installed
manually.

5.  Load the tun.ko module from the command line or a terminal
session.  You will need to do this after a reboot as well.
> $ su
  1. insmod /system/lib/modules/tun.ko

The VPN Connections app should be ready to use.

Notes:

In at least one working example, connecting to servers via vpn
required the fully qualified name of the server.  Connecting to 'mail'
would not work via Droid even though it works via Windows and MacOS,
but connecting to 'mail.mycompany.com' would work on the Droid just
fine.

After shutting down a vpn tunnel, there may be times when
VPN\_Connections does not properly reset the dns servers.  If you have trouble
connecting to the internet, you can go to the command line and use the
commands # getprop net.dns1 or # getprop net.dns2 to see the current
settings.  You can reset these settings by using the commands #
setprop net.dns1 8.8.8.8 and # setprop net.dns2 8.8.4.4 to set your
dns servers to the ones operated by Google.

-- The "tun.ko" module and initial instructions were contributed by Jon Tomaszewski

-- These updated and detailed instructions here were contributed by Mike DeAngelo


