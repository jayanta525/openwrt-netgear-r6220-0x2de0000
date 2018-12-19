# Netgear R6220 AC1200 OpenWrt Firmware
**Factory partition: <0x2de0000>**

This is a modified ramips build for the netgear R6220.

**Factory partition adjusted to <0x2de0000>**, verify WAN interface MAC address with that printed on packaging.

**If your R6220 is still unable to read the correct MAC address, try this [build](https://github.com/jayanta525/openwrt-netgear-r6220-100ins).**

**If the issue persists, try original builds from [OpenWrt](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/).**

The package selection and configuration was intended for personal/home use and is overall lighter. This build includes LuCi interface with some useful luci-applications such as adblock, printer-server, samba, mwan3, sqm, etc.
**Change branch for base builds.**

**[Please note that, once you're using a modified OpenWrt build, packages with kernel dependencies can't be installed using opkg. Request for new builds or ipk files for manual installation]**

## Install Instructions:
  1. Enable debug mode: ```http://<router_ip>/setup.cgi?todo=debug   [usually 192.168.1.1]```
  2. Copy squashfs-rootfs.bin and squashfs-kernel.bin to a USB drive
  3. Telnet <router_ip> and login as root
  4. Connect the USB drive
  5. Check whether USB drive is recognised ``` ls /mnt/shares```
  6. Enter the USB drive ``` cd /mnt/shares/<usb drive>```
  7. Install the binaries and reboot
  ``` 
  mtd_write write <***squashfs-rootfs.bin> Rootfs
  mtd_write write <***squashfs-kernel.bin> Kernel
  reboot
  ```
  
## Update Instructions:
1. Through OpenWrt web interface ```Luci > System > Upgrade > ***-sysupgrade.tar```
2. Through OpenWrt CLI
```
scp ***-sysupgrade.tar root@<router_ip>:/tmp/
ssh root@<router_ip>
sysupgrade -v /tmp/***-sysupgrade.tar
```

## Brick Recovery:
1. If Luci fails to connect and no SSH connection, try [OpenWrt Failsafe](https://wiki.openwrt.org/doc/howto/generic.failsafe) to upgrade to a different build.

    - Power the router holding the WPS button until the power led starts blinking at a faster pace.
    - Assign static IP to PC `192.168.1.XXX/24`
    - Telnet or SSH to `192.168.1.1`
    - SCP a sysupgrade.tar firmware file to `/tmp`
    - On terminal
     ```
      mount_root
      sysupgrade -n -v /tmp/sysupgrade.tar
      ```
  
1. If something goes south, use [nmrpflash](https://github.com/jclehner/nmrpflash) for brick recovery.
2. Obtain router default firmware from [Netgear Support](https://www.netgear.com/support/product/R6220#download).





> *The builds will be updated every month/on-request. Request support for customised builds. If you're having trouble, create an issue on GitHub, or request for support [here](mailto:jayanta.gogoi525@gmail.com)*
