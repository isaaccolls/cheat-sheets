- [locations](#locations)
- [commands / shortcuts / apps](#commands--shortcuts--apps)
  - [linux kernel version](#linux-kernel-version)
  - [terminator](#terminator)
  - [youtube-dl](#youtube-dl)
  - [spotdl](#spotdl)
  - [compress](#compress)
- [permissions](#permissions)
- [install custom apps](#install-custom-apps)
- [hibernate](#hibernate)
- [backup](#backup)
  - [configs](#configs)
  - [pictures](#pictures)
  - [documents](#documents)
  - [music](#music)
  - [projects](#projects)
  - [dark bookmarks](#dark-bookmarks)
- [after install](#after-install)
  - [install](#install)
  - [configs](#configs-1)
  - [run script when logging](#run-script-when-logging)
  - [run script when usb plugged in](#run-script-when-usb-plugged-in)

# locations

- desktop entry location `.local/share/applications`
- polychromatic profiles located: `/home/isaac/.config/polychromatic/profiles`
- wallpapers `/usr/share/backgrounds`
- change gnome screenhots default save directory: ~~`gsettings set org.gnome.gnome-screenshot auto-save-directory "${HOME}/Pictures/Screenshots"`~~

# commands / shortcuts / apps

- find and delete files `find . -name '._*' -exec rm -f {} \;`
- symbolic link `ln -s /Applications/Sublime Text 3.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl3`
- watch `watch -n 3 sudo date`
- hardware detail `lshw`
- random rename `for f in *.jpg; do mv -n "$f" "${f/*/$(shuf -i 1111-9999 -n1).jpg}"; done`
- check port `sudo lsof -i:22`
- recover `ddrescue -R -r9 /dev/sdc5 /media/clientes/87/datos.img /media/clientes/87/logfile.log`
- compare folders `find /dir1/ -type f -exec md5sum {} + | sort -k 2 > dir1.txt` `find /dir2/ -type f -exec md5sum {} + | sort -k 2 > dir2.txt` `diff -u dir1.txt dir2.txt`
- is valid date? `date -d "02/01/2000" 2>: 1>:; echo $?` (0:good date, 1:bad date)
- show environment variable: `cat /etc/environment`
- shows the application menu `super+a`
- set user password: `passwd`
- download website `wget --recursive --page-requisites --adjust-extension --span-hosts --convert-links --restrict-file-names=windows --domains yoursite.com --no-parent yoursite.com`
- change owner group recursively user `sudo chown -R mary ./archive/`
- change owner group `chgrp -hR www-data /var/www`
- Change permissions recursively only to directories `find . -type d -exec chmod -R 0755 {} \;`
- Change permissions recursively only to files `find . -type f -exec chmod -R 0644 {} \;`
- check actual shell `echo $0`
- kill: `pkill -fl Postman`
- merge pdfs: `pdfunite 1.pdf 2.pdf pdfunite.pdf` (`apt install poppler-utils`)
- list packages: `dpkg --list | grep <package-name>`
- uninstalling packages with apt:
  - remove: `sudo apt remove <package-name>`
  - purge: `sudo apt purge <package-name>`
- cleanup: `sudo apt-get clean && sudo apt-get autoremove && sudo apt-get autoclean`
- clear logs: `truncate -s 0 /var/log/syslog`

## linux kernel version

- Find Linux kernel version `uname -r`
- Show Linux kernel version with help of a special file `cat /proc/version`
- display hostname and running Linux kernel version `hostnamectl`

## terminator

- terminator config location `/home/isaac/.config/terminator/config`
- split the view vertically `Ctrl-Shift-E`
- split the view horizontally `Ctrl-Shift-O`
- close the view where the focus is on `Ctrl-Shift-W`
- will exit terminator `Ctrl-Shift-Q`
- Toggle fullscreen `F11`
- Move to the terminal above the current one. `Alt+Up`
- Toggle between showing all terminals and only showing the current one (maximise). `Ctrl+Shift+X`
- Reset terminal state and clear window `Ctrl+Shift+G`
- Move to next Tab / Move to previous Tab `Ctrl+PageDown` `Ctrl+PageUp`
- Group all terminals in the current tab so input sent to one of them, goes to all terminals in the current tab `Super+t`
- Remove grouping from all terminals in the current tab `Super+Shift+T`
- New group `Shift+click`
- Broadcast group `Alt+G`
- Broadcast off `Alt+O`
- fix twice command error:
  - `sudo mv /usr/local/bin/ibus-daemon /usr/local/bin/ibus-daemon.bak`
  - `env --unset=GTK_IM_MODULE terminator`

### custom config

```
[global_config]
inactive_color_offset = 0.61
suppress_multiple_term_dialog = True
title_hide_sizetext = True
[keybindings]
[layouts]
[[default]]
  [[[child1]]]
    parent = window0
    type = Terminal
  [[[window0]]]
    parent = ""
    size = 1800, 800
    type = Window
[plugins]
[profiles]
[[default]]
  cursor_color = "#aaaaaa"
  font = MesloLGS NF 15
  use_system_font = False
  background_color = "#282a36"
  background_image = None
  background_darkness = 0.95
  background_type = transparent
  foreground_color = "#f8f8f2"
  palette = "#262626:#e356a7:#42e66c:#e4f34a:#9b6bdf:#e64747:#75d7ec:#efa554:#7a7a7a:#ff79c6:#50fa7b:#f1fa8c:#bd93f9:#ff5555:#8be9fd:#ffb86c"
  scrollback_infinite = True
```

### set as default

```bash
gsettings set org.gnome.desktop.default-applications.terminal exec /usr/bin/terminator
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "-x"
```

## youtube-dl

- playlist `youtube-dl -i -f best PL_8z4vyyerkMa3Fi6VTw0eXe5ki4R8lc7`
- music playlist with metadata `youtube-dl -i --write-thumbnail --format 'bestaudio/best' --output '%(title)s.%(ext)s' --embed-thumbnail --add-metadata --extract-audio --audio-format 'mp3' PL_8z4vyyerkPtXYwSg6PRo-uUbkAwVcUY`
- not found python fix: `sudo ln -s /usr/bin/python3 /usr/bin/python`
- download mp3: `youtube-dl --extract-audio --audio-format mp3 -f best https://www.youtube.com/watch?v=j-_Amo943XE`
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) sudo apt-get install yt-dlp

## spotdl

- install spotdl: `pip3 install spotdl`
- donwload playlist: `spotdl [playlistUrl]`

## compress

### tar

- Extract a tar.gz archive `tar -xvzf bigfile.tar.gz`
- Extract files to a specific directory or path `tar -xvzf bigfile.tar.gz -C /folder/subfolder/`
- Extract a single file `tar -xz -f Music.tar.gz "./new/one.mp3"`
- List and search contents of the tar archive `tar -tvz -f Music.tar.gz | grep two.mp3`
- Create a tar/tar.gz archive `tar -cvf Videos.tar ./Latest/`
- For the compression we could use the "z" or "j" option for gzip or bzip respectively `tar -cvzf Videos.tar.gz ./Latest/`
- Add files to existing archives `tar -rv -f Book.tar pageone.txt`

### zip

- zip `zip file.zip /dir/file`
- unzip `unzip file.zip`

# permissions

| 0   | --- |
| --- | --- |
| 1   | --x |
| 2   | -w- |
| 3   | -wx |
| 4   | r-- |
| 5   | r-x |
| 6   | rw- |
| 7   | rwx |

# install custom apps

1. put it on `/opt`
2. create launcher `/usr/share/applications/yourapp.desktop`:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Type=Application
Terminal=false
Exec=/path/to/yourapp
Name=YourApp
Comment=Description of YourApp
Icon=/path/to/yourapp.png
Categories=Development;
```

# hibernate

1. install pm-utils: `sudo apt-get install pm-utils`
2. `cat /sys/power/state` should see `freeze mem disk`
3. `grep swap /etc/fstab`
4. add `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=UUID=YOUR_VALUE"` on grub `/etc/default/grub`
5. update grub `sudo update-grub`
   1. in case of problems `sudo grub-install`
6. test it `sudo systemctl hibernate` or `pm-hibernate`

# backup

## configs

- terminator config `cp -fv .config/terminator/config /media/isaac/Backup/configs/terminator`
- ssh keys `cp -rfv .ssh /media/isaac/Backup/configs/ssh`
- zsh config `cp -fv .zshrc /media/isaac/Backup/configs/zshrc`
- aws `cp -rfv .aws /media/isaac/Backup/configs/aws`
- kube `cp -rfv .kube /media/isaac/Backup/configs/kube`
- grub `cp -v /etc/default/grub /media/isaac/Backup/configs/grub`

## pictures

## documents

- credentials `rm -rfv /media/isaac/Backup/xxx` `cp -rfv ~/xxx /media/isaac/Backup/xxx`
- signature.html `rm -rfv /media/isaac/Backup/Documents/signature.html` `cp -rfv ~/Documents/signature.html /media/isaac/Backup/Documents`

## music

`rm -rfv /media/isaac/Backup/Music/sheets` `cp -rfv ~/Music/sheets /media/isaac/Backup/Music`

## projects

`rm -rf /media/isaac/Backup/Projects` `mkdir /media/isaac/Backup/Projects` `rsync -av --exclude 'node_modules' ~/Projects/ /media/isaac/Backup/Projects`

## dark bookmarks

`cp /opt/tor-browser_en-US/Browser/Desktop/bookmarks.json /media/isaac/Backup/configs/`

# after install

## install

- git: `sudo apt-get git`
- chrome
- slack
- postman
- robomongo
- dbeaver
- gparted: `sudo apt-get install gparted`
- torrent client: `sudo apt-get install transmission`
- operator mono _font_
- vscode
- spotify and musixmatch
- multimedia codecs: `sudo apt install ubuntu-restricted-extras libavcodec-extra libdvd-pkg`
- vlc `sudo apt install vlc`
- steam
- nvm `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash` and terminal restart (nvm plugin 😉)
- terminator: `sudo apt-get install terminator`

### improve Laptop battery life

```bash
sudo apt-get install tlp tlp-rdw
sudo systemctl enable tlp
sudo tlp-stat -s
```

### zsh

```bash
sudo apt install zsh
zsh --version
chsh -s $(which zsh)
```

#### oh my zsh

install: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

#### power level

1. Install the [recommended](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k) font.
2. set _MesloLGS NF Regular_ on **Profiles**
3. clone power level `git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k`
4. enable theme `echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc`
5. restart Zsh
6. type `p10k configure` if the configuration wizard doesn't start automatically

##### plugins

- zsh-syntax-highlighting: `git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`
- zsh-autosuggestions: `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`
- update: in `~/.zshrc` file replace update plugins `plugins=(git virtualenv nvm zsh-syntax-highlighting zsh-autosuggestions)`

### tweaks

```bash
sudo apt install software-properties-common
sudo add-apt-repository ppa:philip.scott/pantheon-tweaks
sudo apt update
sudo apt install pantheon-tweaks
```

### nvidia

- check nvidia `nvidia-smi`
- ubuntu-drivers devices (look for _recommended_)
- if good recommendation `sudo ubuntu-drivers autoinstall`
  - else `sudo apt install nvidia-driver-460`
- To check which card is being used right now: `prime-select query`
- remove all 💩: `sudo apt-get --purge -y remove 'nvidia*'`

### open razer

```bash
sudo apt install software-properties-gtk
sudo add-apt-repository ppa:openrazer/stable
sudo apt update
sudo apt install openrazer-meta
# don't forget below command
sudo gpasswd -a $USER plugdev
```

### libre office

- calc: `sudo apt-get install libreoffice-calc`
- writer: `sudo apt-get install libreoffice-writer`
- draw: `sudo apt-get install libreoffice-draw`

### tuxguitar

1. `sudo apt-get install tuxguitar tuxguitar-alsa tuxguitar-jsa tuxguitar-oss`
2. go to Tools -> Settings -> Sound and select _Gervill_ as Midi Port.

## configs

- workspace should contain all monitors: `gsettings set org.gnome.mutter workspaces-only-on-primary false`
- theme, cursor and icons: check for something cool on [pling](https://www.pling.com/p/1403328/)
  - extract themes to `~/.themes/`
  - extract cursor and icons to `~/.icons/` or `~/usr/share/icons/` for system side installation

### tweaks

- disable single-click (on settings -> tweaks -> files)
- disable natural copy-paste in terminal (Tweaks and in the Terminal tab)
- add minimize button (os x)

### dock

1. `hold`ctrl + right-click` over _the dock_
2. then `click` preferences (transparent)

### grub

1. copy grub razer theme `sudo cp -rf /media/isaac/Backup/configs/grub-theme /boot/grub/themes/razer`
2. edit `/etc/default/grub`

```
GRUB_CMDLINE_LINUX_DEFAULT="button.lid_init_state=open intel_idle.max_cstate=4"
# gfx mode for RBS 4k
GRUB_GFXMODE="3840x2160-32"
GRUB_GFXPAYLOAD_LINUX="3840x2160-32"
GRUB_THEME="/boot/grub/themes/razer/theme.txt"
```

3. set it up: `sudo update-grub`

### sport camera as webcam

- reconfigure the uvcvideo `sudo rmmod uvcvideo` `sudo modprobe uvcvideo quirks=2` (Note you can add this parameter to /etc/modules or /etc/modprobe.d/)
- debug `sudo apt-get install v4l-utils` `v4l2-ctl --list-devices`

### fix i915 firmware

```bash
cd /tmp
git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cd linux-firmware/
cp i915/* /lib/firmware/i915/
update-initramfs -u
```

## run script when logging

- specific user `~/.config/autostart/my_script.desktop`
- all users `/etc/xdg/autostart/my_script.desktop`

```
[Desktop Entry]
Type=Application
Name=openrazer start
Exec=python3 /home/isaac/Projects/openrazer/set.py 50
Icon=system-run
X-GNOME-Autostart-enabled=true
```

## run script when usb plugged in

- add a new rule on `/etc/udev/rules.d/`
  - name: `openrazer.rules`
  - content: `ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="1532", RUN+="/etc/udev/rules.d/test.sh"`
