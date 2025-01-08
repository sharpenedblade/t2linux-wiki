# Installing alongside Windows

If you already have Bootcamp installed, you might notice that the boot option for Bootcamp instead boots you into Fedora. This is because GRUB automatically shares with a Windows installation. Follow [this guide on triple booting](https://wiki.t2linux.org/guides/windows/#if-windows-is-installed-first) to get Windows working again.

# My boot hangs before getting to the installer

This may be due to differences between USB-C to USB-A adapters. Try a different one if it is not working.

# I get an error about the bootloader when installing

Download the latest ISO, then try again. If this does not help, install [rEFInd](https://wiki.t2linux.org/guides/refind/)

# My Wi-Fi stops working after suspending

Add this to `/etc/systemd/system-sleep/unload-wifi.sh`:

```bash
#!/usr/bin/env bash
if [ "${1}" = "pre" ]; then
    systemctl stop NetworkManager
    modprobe -r brcmfmac_wcc
    modprobe -r brcmfmac
elif [ "${1}" = "post" ]; then
    modprobe brcmfmac
    systemctl start NetworkManager
fi
```
