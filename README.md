# Linux Setup
My personal modifications for Manjaro and Ubuntu

## Replace CapsLock with Backspace

```setxkbmap -option caps:backspace -option shift:both_capslock```

## Activate 'Hand Break'

Force end of session with (Ctrl + Alt + Backspace)

```kate /etc/default/keyboard```

```XKBOPTIONS="terminate:ctrl_alt_bksp"```

## Enable the Firewall

```sudo ufw enable```

```pamac install gufw```  // ```sudo apt install gufw```

## Nikon as Webcam

```pamac install v4l2loopback-dkms gphoto2```

```sudo apt install entangle linux-generic v4l2loopback-dkms gphoto2```

```sudo modprobe v4l2loopback```

```gphoto2 --stdout --capture-movie | gst-launch-1.0 fdsrc fd=0 ! decodebin name=dec ! queue ! videoconvert ! tee ! v4l2sink device=/dev/video0```

## Install Printer Driver for Brother MFC295CN

```pamac build brother-mfc-290c```

```sudo pacman -S cups manjaro-printer```

```sudo systemctl enable org.cups.cupsd.service```


## Essential Programs

```pamac install vivaldi brave-browser nextcloud-client thunar bitwarden libreoffice-fresh smplayer qmmp mixxx gimp inkscape steam evince scrcpy pavucontrol clamtk audacity plasma-vault gocryptfs telegram-desktop tuxedo-control-center mediathekview libappindicator-gtk3 gnome-shell-extension-appindicator```

```pamac build protonvpn authy freetube puddletag avidemux-qt ffmpegthumbnailer rainlendar-pro```