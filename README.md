# Linux Setup
Some essential commands for Manjaro and Ubutnu

## GPT Partition Table

Mountpoint -- Flag -- Filesystem

```/boot/efi -- boot -- FAT32```

```Swap -- swap -- linuxswap```

```/ -- root -- brfs```

```/home -- 0 -- btrfs```


## Replace CapsLock with Backspace

```setxkbmap -option caps:backspace -option shift:both_capslock```


## Activate 'Hand Break'

Force end of session with (Ctrl + Alt + Backspace)

```kate /etc/default/keyboard```

```XKBOPTIONS="terminate:ctrl_alt_bksp"```


## Enable the Firewall

```sudo ufw enable```

```pamac install gufw```  // ```sudo apt install gufw```


## Install Printer Driver for Brother MFC295CN

```pamac build brother-mfc-290c```

```sudo pacman -S cups manjaro-printer```

```sudo systemctl enable org.cups.cupsd.service```


## Reduce Swappiness

```sudo echo "vm.swappiness=10" > /etc/sysctl.d/100-manjaro.conf```


## Essential Programs

```pamac install tvtime testdisk vivaldi brave-browser nextcloud-client thunar smplayer qmmp mixxx gimp inkscape steam evince scrcpy pavucontrol clamtk audacity plasma-vault gocryptfs telegram-desktop tuxedo-control-center mediathekview libappindicator-gtk3 gnome-shell-extension-appindicator converseen base-devel```

```pamac build qimgv protonvpn puddletag avidemux-qt ffmpegthumbnailer rainlendar-pro peazip-qt-bin linux-wifi-hotspot```


## Initiate E-Card-Reader

```sudo systemctl start pcscd.service```

```sudo systemctl enable pcscd.service```


## Tesseract Fraktur

```tesseract page1.tif page1 -l deu_frak```

## Convert PDF to Images

```pdftoppm -jpeg -r 300 Document.pdf page```


## Nikon as Webcam

```pamac install v4l2loopback-dkms gphoto2```

```sudo apt install entangle linux-generic v4l2loopback-dkms gphoto2```

```sudo modprobe v4l2loopback```

```gphoto2 --stdout --capture-movie | gst-launch-1.0 fdsrc fd=0 ! decodebin name=dec ! queue ! videoconvert ! tee ! v4l2sink device=/dev/video0```


## Inject Spatial Metadata for 360° Videos

```pamac install perl-image-exiftool```

```exiftool -XMP-GSpherical:Spherical="true" video.mp4```


## Plasma-Vaults

Path:

```/home/$USER/.config/plasmavaultrc```

plasmavaultrc:

```[/home/$USER/.vaults/Data.enc]```

```activities=```

```backend=gocryptfs```

```mountPoint=/home/$USER/Vaults/Data```

```name=Data```

```offlineOnly=false```

```[EncryptedDevices]```

```/home/$USER/.vaults/Data.enc=true```

```[UI-notice]```

```SkipNotice-gocryptfs-message=false```


## Wipe Filesystem with Zeros

HDD only!

```dd if=/dev/zero of=zero.small.file bs=1024 count=102400```

```cat /dev/zero > zero.file```

```sync```

```rm zero.small.file```

```rm zero.file```


## Write Image on Disk with dd

```sudo dd if=image.iso of=/dev/sd* bs=1024k status=progress```

