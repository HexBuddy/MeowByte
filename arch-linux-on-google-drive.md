# Arch Linux on Google Drive

Here's a detailed guide to boot Arch Linux from Google Drive using FUSE and `google-drive-ocamlfuse`.

#### Prerequisites

1. An existing Arch Linux installation (or a live USB/CD for initial setup).
2. Internet connection.
3. Basic knowledge of Linux command line and file systems.

#### Step-by-Step Guide

**1. Install Necessary Packages**

First, you'll need to install `dracut`, `docker`, and other necessary packages:

```bash
sudo pacman -Syu dracut docker git
```

**2. Clone Dracut Repository**

```bash
git clone https://github.com/dracutdevs/dracut
cd dracut
```

**3. Set Up Docker Container**

```bash
sudo docker run -it --name arch -v $(pwd):/dracut docker.io/archlinux:latest bash
```

Inside the Docker container, install necessary packages:

```bash
pacman -Syu base-devel linux
```

**4. Write Dracut Module Script**

Create a script for the FUSE module:

```bash
mkdir -p /dracut/modules.d/90fuse
cat <<EOF > /dracut/modules.d/90fuse/module-setup.sh
#!/bin/bash
check() {
    require_binaries fusermount fuseiso mkisofs || return 1
    return 0
}

depends() {
    return 0
}

install() {
    inst_multiple fusermount fuseiso mkisofs
    return 0
}
EOF

chmod +x /dracut/modules.d/90fuse/module-setup.sh
```

**5. Build the Custom Initramfs**

```bash
dracut --kver 6.9.6-arch1-1 --uefi efi_firmware/EFI/BOOT/BOOTX64.efi --force -l -N --no-hostonly-cmdline --modules "base bash fuse shutdown network" --add-drivers "target_core_mod target_core_file r8169" --kernel-cmdline "ip=dhcp rd.shell=1 console=ttyS0"
```

**6. Configure Network and Mount Google Drive in Initramfs**

Add the following to `/dracut/modules.d/99base/init.sh` after the udev rules are loaded:

```bash
modprobe fuse
modprobe r8169
ip link set lo up
ip link set eth0 up
dhclient eth0
ip route add default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15
s3fs -o url=http://192.168.2.209:9000 -o use_path_request_style fuse /sysroot
mount --rbind /sys /sysroot/sys
mount --rbind /dev /sysroot/dev
mount -t proc /proc /sysroot/proc
exec chroot /sysroot /sbin/init
```

**7. Install Google Drive FUSE in Arch Linux**

Exit the Docker container and install `google-drive-ocamlfuse` on your Arch Linux system:

```bash
sudo pacman -Syu google-drive-ocamlfuse
```

Authenticate with Google Drive:

```bash
google-drive-ocamlfuse
```

Mount Google Drive:

```bash
mkdir ~/gdrive
google-drive-ocamlfuse ~/gdrive
```

**8. Copy Root Filesystem to Google Drive**

Copy the Arch Linux root filesystem to Google Drive:

```bash
sudo rsync -avxHAX --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} / ~/gdrive/arch-root/
```

**9. Update Initramfs with Google Drive Configuration**

Add the following to your initramfs script:

```bash
inst ./gdfuse-config /.gdfuse/default/config
inst ./gdfuse-state /.gdfuse/default/state
find /etc/ssl -type f -or -type l | while read file; do inst "$file"; done
find /etc/ca-certificates -type f -or -type l | while read file; do inst "$file"; done
```

Rebuild the EFI image:

```bash
dracut --kver 6.9.6-arch1-1 --uefi efi_firmware/EFI/BOOT/BOOTX64.efi --force -l -N --no-hostonly-cmdline --modules "base bash fuse shutdown network" --add-drivers "target_core_mod target_core_file r8169" --kernel-cmdline "ip=dhcp rd.shell=1 console=ttyS0"
```

**10. Boot from USB**

Create a bootable USB drive with the EFI image:

```bash
sudo dd if=efi_firmware/EFI/BOOT/BOOTX64.efi of=/dev/sdX bs=4M
```

Replace `/dev/sdX` with your USB device.

**11. Boot Your System**

Insert the USB drive into your target system and boot from it. Ensure the network settings are correct, and use an external keyboard if necessary to set up networking.

#### Final Adjustments

1. **Update Timeouts**:
   * Increase timeouts for devices and login settings if needed.
2. **Debugging**:
   * If you encounter issues, check `/run/initramfs/rdsosreport.txt` for detailed error logs.
3. **Optimize Performance**:
   * Experiment with different network settings or hardware configurations to optimize boot time and performance.

This guide should help you boot Arch Linux from Google Drive.
