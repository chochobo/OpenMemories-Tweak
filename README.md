# OpenMemories: Tweak
An app to unlock settings on your Sony camera.
* Remove the 30min video recording limit
* Unlock the language menu

## Installation
Install it here: [sony-pmca.appspot.com](https://sony-pmca.appspot.com/apps) (Only Internet Explorer and Safari are supported)

## Compatibility
This app should be compatible with all Sony cameras supporting PlayMemories Camera Apps (PMCA). See [here](https://github.com/ma1co/OpenMemories-Framework/blob/master/docs/Cameras.md) for a full list.

## A word of caution
This is not an official Sony application. All information has been found through reverse engineering. Even though everything worked fine for our developers, it could cause harm to your hardware. If you break your camera, you get to keep both pieces. **We won't take any responsibility.**

## Usage
After installation, you should find the app in the "Application List" on your camera.

* Use the menu button to exit the app
* The app writes a log to the SD card (*TWEAKLOG.TXT*)

There are several different tabs:

### Video
Remove the 30 minute recording limit and enjoy (almost) unlimited video recording.

### Region
Is your camera locked to Japanese? Is it set to the wrong region? Unlock all 30+ languages.

Is your camera locked to NTSC? Enable the PAL / NTSC selector.

Does your camera show you the NTSC nag screen on every startup? Disable the PAL / NTSC selector to get rid of the nag screen.

### Protection
Use this option only if you're asked to do so. Some of the above settings may fail because your settings file is locked. Disable the protection here. In practice, it should only matter to this app if your settings are protected or not. Otherwise, this won't change anything. We still recommend re-enabling protection after you're done tweaking your settings.

### Developer
Run a telnet daemon and connect to it via wifi.

#### Run an Android shell
    android_console.sh

#### Dump firmware to sdcard
On Android 2:

    dd if=/dev/nflasha of=/android/mnt/sdcard/DUMP.DAT bs=1M

On Android 4:

    dd if=/dev/nflasha of=/android/storage/sdcard0/DUMP.DAT bs=1M

This operation will take some time (it copies about 500MB). Use [fwtool.py](https://github.com/ma1co/fwtool.py) to unpack the dump file.

## FAQ
### How does it all work?
[nex-hack](http://www.personal-view.com/faqs/sony-hack/hack-development) managed to decrypt firmware updates (see [fwtool.py](https://github.com/ma1co/fwtool.py) for a more recent unpacker). The [PMCA-RE](https://github.com/ma1co/Sony-PMCA-RE) project reverse engineered how apps are installed. This allows us to run custom code. With the knowledge from the firmware, we found out how settings are stored on the camera (hint: in a file called *Backup.bin*). We can now change these settings directly, also the ones locked by Sony.

### It doesn't work for me!
First, thanks for testing. If you encounter a bug, please open an issue!

### I don't have Internet Explorer
Well, lucky you :) You can try the experimental [installer](https://github.com/ma1co/Sony-PMCA-RE#local-installer) (releases for Windows and OS X are provided).

### How can I remove the app?
You can uninstall it normally with the "Application Management" app. The modified settings are preserved even if you remove the app.

### What happens if i do a factory reset?
Some settings might be removed, others will be permanent. We still have to investigate a bit more to find out which features are reset and how. In the worst case, you can reinstall the app (all apps are removed in a factory reset) and apply the settings again.

### What happens if i do a firmware update?
See above.

### I have an old camera that doesn't support apps
For now, you're out of luck. We can only run code on our cameras through the Android subsystem. For older cameras, you'd have to patch a firmware image with your settings. There is also a USB service mode (senser / adjust mode) which sadly we haven't managed to trigger (yet).

### Can you add feature X?
Keep in mind that this app can only change settings that are already there and just hidden by Sony. However, there are still about 15 000 entries in the settings file. So finding out what a particular setting does is quite an effort. But if you have ideas, feel free to open an issue!
