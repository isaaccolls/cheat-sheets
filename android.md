- [abd](#abd)
- [avd](#avd)

# abd

- add path: `export PATH=${PATH}:$HOME/Android/Sdk/platform-tools/`
- check version: `adb --version`
- install an APK: `adb install path_to_apk`
- copy files:
  - copy from the device: `adb pull remote local`
  - copy to the device: `adb push local remote` (`adb push foo.txt /sdcard/foo.txt`)
- stop the adb server: `adb kill-server` `restart the server by issuing any other adb command`

# avd

- add path: `export PATH=${PATH}:$HOME/Android/Sdk/emulator/`
- location: `~/Android/Sdk/emulator`
- list of AVD names: `emulator -list-avds`
- starting the emulator: `emulator -avd Pixel420 -netdelay none -netspeed full`
