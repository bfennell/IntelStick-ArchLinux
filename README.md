# IntelStick-ArchLinux

# Get Install Image & write to USB stick
```sh
wget http://artfiles.org/archlinux.org/iso/2019.11.01/archlinux-2019.11.01-x86_64.iso
dd bs=4M if=archlinux-2019.11.01-x86_64.iso of=/dev/sdX status=progress oflag=sync
```

# Enter BIOS
```sh
Press F7 while booting
```

# Fix Network Driver
```sh
cp /lib/firmware/brcm/brcmfmac43455-sdio.raspberrypi,3-model-b-plus.txt /lib/firmware/brcm/brcmfmac43455-sdio.txt
modprobe -r brcmfmac
modprobe brcmfmac
```

# Connect to Wifi
```sh
wifi-menu
```

# Follow Arch Linux install....
```sh
... First delete all windows partitions (including the EFI partition)
...
pacstrap /mnt base linux linux-firmware
...
Install GRUB (UEFI)....
...
```

# Chroot...

# Fix GRUB config (to allow boot without monitor connected)
```sh
edit /etc/default/grub
-> GRUB_CMDLINE_LINUX_DEFAULT="nomodeset text"
-> GRUB_TERMINAL_OUTPUT=console
grub-mkconfig -o /boot/grub/grub.cfg
```

# Auto WLAN connect at boot
```sh
netctl enable profile
# Note: profile is created by wifi-menu
 --> e.g. /etc/netctl/my-fifi-network
```

