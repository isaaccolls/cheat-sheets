- [config](#config)
  - [get hardware revision](#get-hardware-revision)
- [wifi](#wifi)

# config

- show config menu: `sudo raspi-config`
- enable ssh: `sudo systemctl enable ssh`
  - create file: `/boot/ssh/`
- working without hdmi: Uncomment the below line `hdmi_force_hotplug=1` in the file `/boot/config.txt`

## get hardware revision

- pinout utility: `pinout`
- cpuinfo File: `cat /proc/cpuinfo`
- Raspberry Pi Model Information: `cat /proc/device-tree/model`

# wifi

- scan `sudo iwlist wlan0 scan`
- edit /etc/wpa_supplicant/wpa_supplicant.conf as:

  ```conf
  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1
  country=CL
  network={
      ssid="hakunaMatata"
      psk="k-Z0aACNLvXVsuMa9su@"
      priority=1
  }
  network={
      ssid="Starbucks"
      key_mgmt=NONE
      wep_key0=1b9dda483d
      priority=2
  }
  ```
