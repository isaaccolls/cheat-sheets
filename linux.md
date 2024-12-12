- [locations](#locations)
- [commands / shortcuts / apps](#commands--shortcuts--apps)
  - [samba](#samba)
  - [linux kernel version](#linux-kernel-version)
  - [terminator](#terminator)
  - [youtube-dl](#youtube-dl)
  - [compress](#compress)
  - [flatpak](#flatpak)
- [permissions](#permissions)
- [install custom apps](#install-custom-apps)
- [backup](#backup)
  - [configs](#configs)
  - [documents](#documents)
  - [projects](#projects)
  - [dark bookmarks](#dark-bookmarks)
- [after install](#after-install)
  - [install](#install)
- [dbeaver](#dbeaver)
  - [themes](#themes)
  - [sport camera as webcam](#sport-camera-as-webcam)
  - [fix opera bug](#fix-opera-bug)
  - [run script when logging](#run-script-when-logging)
  - [run script when usb plugged in](#run-script-when-usb-plugged-in)

# locations

- desktop entry location `.local/share/applications`
- polychromatic profiles located: `/home/isaac/.config/polychromatic/profiles`
- wallpapers `/usr/share/backgrounds`

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
- paquetes:
  - actualizar: `sudo apt-get update`
  - actualizar: `sudo apt-get full-upgrade`
- scan for Wi-Fi networks signal strength
  1. Install Necessary Tools: `sudo apt install iw`
  2. Scan for Wi-Fi Networks `sudo iwlist wlan0 scan | grep -E 'SSID|Signal level'`

## samba

- mount: `sudo mount.cifs //192.168.6.211/backup /home/isaac/Downloads/montaje -o username=isaaccolls,password=cenco`
- unmount: `sudo umount /home/isaac/Downloads/montaje`

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
  1. find terminator location: `which terminator`
  2. edit terminator: `vim /usr/bin/terminator`
  3. after the "import" lines at top, insert: `os.environ['DBUS_SESSION_BUS_ADDRESS'] = ''`

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

run `sudo update-alternatives --config x-terminal-emulator`

## youtube-dl

- playlist `youtube-dl -i -f best PL_8z4vyyerkMa3Fi6VTw0eXe5ki4R8lc7`
- music playlist with metadata `youtube-dl -i --write-thumbnail --format 'bestaudio/best' --output '%(title)s.%(ext)s' --embed-thumbnail --add-metadata --extract-audio --audio-format 'mp3' PL_8z4vyyerkPtXYwSg6PRo-uUbkAwVcUY`
- not found python fix: `sudo ln -s /usr/bin/python3 /usr/bin/python`
- download mp3: `youtube-dl --extract-audio --audio-format mp3 -f best https://www.youtube.com/watch?v=j-_Amo943XE`
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) sudo apt-get install yt-dlp

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

- zip `zip -r file.zip /dir/file`
- unzip `unzip file.zip`

## flatpak

- list installed apps: `flatpak list`
- show app info: `flatpak info [app_name]`
  - show app location: `flatpak info --show-location [app_name]`

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

# backup

## configs

- terminator config `cp -fv .config/terminator/config /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/configs/terminator`
- ssh keys `cp -rfv .ssh /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/configs/ssh`
- zsh config `cp -fv .zshrc /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/configs/zshrc`

## documents

- credentials `rm -rfv /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/xxx` `cp -rfv ~/xxx /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/xxx`

## projects

`rm -rf /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/Projects` `mkdir /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/Projects` `rsync -av --exclude 'node_modules' ~/Projects/ /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/Projects`

## dark bookmarks

`cp /opt/tor-browser_en-US/Browser/Desktop/bookmarks.json /media/isaac/7493cdfd-c3b3-4bfb-aa03-6bb3af4e4069/isaac/configs/`

# after install

## install

- git: `sudo apt-get git`
- opera
- postman
- torrent client: `sudo apt-get install transmission`
- operator mono _font_
- vscode
- vlc `sudo apt install vlc`
- steam
- nvm `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash` and terminal restart (nvm plugin 😉)
- terminator: `sudo apt-get install terminator`
- tweaks: `sudo apt install gnome-tweaks`
- heic support: `sudo apt install heif-gdk-pixbuf` and `sudo apt-get install heif-thumbnailer`

# dbeaver

[website](https://dbeaver.io/download/)

Ubuntu PPA:

```bash
sudo add-apt-repository ppa:serge-rider/dbeaver-ce
sudo apt-get update
sudo apt-get install dbeaver-ce
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

### Music edition

#### tuxguitar

1. `sudo apt-get install tuxguitar tuxguitar-alsa tuxguitar-jsa tuxguitar-oss`
2. go to Tools -> Settings -> Sound and select _Gervill_ as Midi Port.

#### MuseScore

- install with `sudo apt install musescore`

### nvidia

monitor: `sudo apt install nvtop`

### sensors

- install: `sudo apt install lm-sensors`
- run `sensors`

## themes

- theme, cursor and icons: check for something cool on [pling](https://www.pling.com/p/1403328/)
  - extract themes to `~/.themes/`
  - extract cursor and icons to `~/.icons/` or `~/usr/share/icons/` for system side installation

## sport camera as webcam

- reconfigure the uvcvideo `sudo rmmod uvcvideo` `sudo modprobe uvcvideo quirks=2` (Note you can add this parameter to /etc/modules or /etc/modprobe.d/)
- debug `sudo apt-get install v4l-utils` `v4l2-ctl --list-devices`

## fix opera bug

1.  Find the chromium version your browser is based on
    1.  Goto `opera://about`
    1.  then `Ctrl+F` to find `'Chrome'` in the user-agent
    1.  version number is Chrome/`XX`.other_numbers
1.  Download libffmpeg.so
    - [option 1](https://onedrive.live.com/?authkey=%21AC7ddalBsUiWsUE&id=75D48EF8D3750510%21234&cid=75D48EF8D3750510) and get your file based on your chromium version
    - [option 2](http://security.ubuntu.com/ubuntu/pool/universe/c/chromium-browser/) and download the `chromium-codecs-ffmpeg-extra_XX` where `XX` is your chromium version
    - [resource 1](https://www.reddit.com/r/operabrowser/wiki/opera/linux_libffmpeg_config)
    - [resource 2](https://gist.github.com/hauke96/5d808ff06e695c752783f4054232a4a9)
1.  Copy libffmpeg.so in the browser folder: `cp ~/Downloads/libffmpeg.so /home/isaac/.local/share/flatpak/app/com.opera.Opera/x86_64/stable/022db8a5595c2fff27f44a7a28f2611598632c277d3f72e1731399d1c9cbbb25/files/opera`

## run script when logging

- specific user `~/.config/autostart/my_script.desktop`
- all users `/etc/xdg/autostart/my_script.desktop`

```

[Desktop Entry]
Type=Application
Name=openrazer start
Exec=python3 /home/isaac/Projects/openrazer/set.py m
Icon=system-run
X-GNOME-Autostart-enabled=true

```

## run script when usb plugged in

- add a new rule on `/etc/udev/rules.d/`
  - name: `openrazer.rules`
  - content: `ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="1532", RUN+="/etc/udev/rules.d/test.sh"`
