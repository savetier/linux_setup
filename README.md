# Linux Setup
Some essential commands for Manjaro and EndeavourOS


## Replace CapsLock with Backspace

```setxkbmap -option caps:backspace -option shift:both_capslock```

Can be done in Plasma in System Settings > Keyboard > Advanced

## Activate 'Hand Break'

Force end of session with (Ctrl + Alt + Backspace)

```kate /etc/default/keyboard```

```XKBOPTIONS="terminate:ctrl_alt_bksp"```

Can be done in Plasma in System Settings > Keyboard > Advanced

## Enable the Firewall

```sudo ufw enable```

```pamac install gufw```

## Allow Wifi-Hotspot through Firewall (ufw)

```sudo ufw allow to any port 53```

```sudo ufw allow to any port 67 proto udp```

```sudo ufw allow to any port 68 proto udp```

```sudo ufw allow udp 5353```

```sudo ufw allow bootps```

## Install Printer Driver for Brother MFC295CN

```pamac build brother-mfc-290c brscan3```

```sudo pacman -S cups```

```sudo systemctl enable --now cups```

```sudo usermod -aG lp username```

```sudo pacman -S system-config-printer```


## Reduce Swappiness

```sudo echo "vm.swappiness=10" > /etc/sysctl.d/100-manjaro.conf```


## Activate apparmor

```pamac install apparmor```

```systemctl enable apparmor.service```

```systemctl status apparmor```

Boot with apparmor activated:

```kate /etc/default/grub```

-> add ```apparmor=1 security=apparmor``` to ```GRUB_CMDLINE_LINUX_DEFAULT```

```sudo update-grub```

```aa-enabled```

## Essential Programs

```pamac install base-devel btrfs-progs btrfsmaintenance tvtime testdisk tesseract thunar xfce4-taskmanager mkvtoolnix-gui vym vivaldi brave-browser nextcloud-client smplayer qmmp gimp inkscape steam evince scrcpy pavucontrol audacity plasma-firewall gufw plasma-vault gocryptfs telegram-desktop tuxedo-control-center libappindicator-gtk3 gnome-shell-extension-appindicator converseen pdfarranger gnome-disk-utility gparted clamtk mediathekview avidemux-qt ffmpegthumbnailer bleachbit vulkan-radeon lib32-vulkan-radeon libreoffice-fresh zotero wine-staging zpaq scummvm```

```pamac build joplin-appimage freetube qimgv puddletag rainlendar-pro linux-wifi-hotspot cover-thumbnailer protonvpn-cli-community proton-mail-bin espanso qmplay2```

```sudo pacman -S --needed mesa-demos vulkan-tools```


## If proton-vpn-gtk-app doesn't work on Manjaro - rebuild it

```pamac remove proton-vpn-gtk-app python-proton-core python-proton-keyring-linux python-proton-keyring-linux-secretservice python-proton-vpn-api-core python-proton-vpn-killswitch-network-manager python-proton-vpn-killswitch-network-manager-wireguard python-proton-vpn-logger python-proton-vpn-network-manager python-proton-vpn-network-manager-openvpn python-proton-vpn-network-manager-wireguard```

```pamac build proton-vpn-gtk-app```


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

## Restart Plasma-Shell

```plasmashell --replace & ```

## Re-Initialise Font-Cache

```sudo fc-cache -f -v```

## Cleaning

Clean Cache

```sudo pacman -Sc```

```sudo pacman -Qdt```

```sudo pacman -Rns $(pacman -Qtdq)```

Vacuum Journals

```journalctl --disk-usage```

```sudo journalctl --vacuum-size=50M```

Remove orphaned libraries

```pamac remove --orphans```

Clean cache

```pamac clean --build-files```

## Merge Textfiles

```cat *.txt > all.txt```

## Remove Title from MKV-File

```mkvpropedit "Film.mkv" --tags all: ```

## Set up Jellyfin-Server

```pamac install jellyfin-server```

```pamac install jellyfin-web```

```sudo systemctl start jellyfin.service```

```sudo systemctl enable jellyfin.service```

```sudo find /jellyfin -type d -exec chmod 2755 {} \;```

```sudo find /jellyfin -type f -exec chmod 0644 {} \;```

```http://localhost:8096```

```sudo chown -R jellyfin: /etc/jellyfin /var/lib/jellyfin /var/log/jellyfin /var/cache/jellyfin /usr/share/jellyfin```

## Switching to zsh shell


```sudo pacman -Sy zsh```

```sudo pacman -S zsh-autosuggestions zsh-syntax-highlighting zsh-completions zsh-theme-powerlevel10k```

```chsh -s /usr/bin/zsh```

Add to .zshrc

```autoload -U compinit promptinit```

```promptinit```
```prompt pure```

```compinit```

```source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh```

```source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh```

```source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme```

```# History file for zsh```

```HISTFILE=~/.zsh_history```

Start zsh and edit theme

Restart System

```rehash```

Or:

Get .zshrc from Grml:

```wget -O ~/.zshrc https://raw.githubusercontent.com/grml/grml-etc-core/master/etc/zsh/zshrc``` 

## Stop Nextcloud-Client from Popping up Randomly

```mkdir -p .local/share/dbus-1/services/```

```touch .local/share/dbus-1/services/com.nextcloudgmbh.Nextcloud.service```

Add the follwing to the file:

```[D-BUS Service]```

```Name=com.nextcloudgmbh.Nextcloud```

```Exec=/bin/false```
