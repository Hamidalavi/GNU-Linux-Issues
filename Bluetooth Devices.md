# Bluetooth Devices

## Full upgrade (run as `sudo`):

- `pacman -Sy`
- `pacman-key --refresh-keys`
- `pacman -Syu`

or

- `pacman -Syyu`

## Minimal upgrade:

- `pacman -Sy`
- `pacman-key --refresh-keys`

## Installing necessary packages:

- `pacman -Syu pulseaudio-bluetooth`
- `pacman -Syu pulseaudio-alsa`
- `pacman -Syu pavucontrol`
- `pacman -Syu bluez`
- `pacman -Syu bluez-utils`

Make sure bluetooth is running and automatically starts after booting:

- `systemctl enable bluetooth`
- `systemctl start bluetooth`

Configure PulseAudio and Bluetooth. Add the following to the bottom of the main bluetooth configuration file (use nano or vscode or emacs editor):

- `emacs -nw /etc/bluetooth/main.cf` => **AutoEnable=true**

or

- `code -nw /etc/bluetooth/main.cf` => **AutoEnable=true**

To make sure that your headsets is automatically connected to your bluetooth device we need to enable the `switch-on-connect module`. We also copy the configurations to our user directory because we don't want to change the system wide settings. If you want you can also change `/etc/pulse/*` though, the choice is whatever you prefer. (use editor like `emacs` or `code` and etc.)

- `mkdir -p ~/.config/pulse`
- `cp /etc/pulse/* ~/.config/pulse/`

**code -nw ~/.config/pulse/default.pa** => `load-module module-switch-on-connect` -- add this at the bottom

After making these changes restart your bluetooth: `systemctl restart bluetooth`

Pairing your headset. Ok we've finally done all the ground work to pair our device. Open a terminal and start `bluetoothctl`. We use `bluetoothctl` to pair, trust and connect to the headset. But before we start we check if the device was already paired and maybe incorrectly configured. To make sure we start off with the same settings check if the device was paired, then remove it and start from scratch:

```js
`bluetoothctl`

[bluetooth]# `paired-devices`

Device 00:1D:43:6D:03:26 PXC 550

[bluetooth]# `remove 00:1D:43:6D:03:26`
```

Ok, now we can start with a clean configuration. Execute the following commands. After you've given the `scan` on command (see below), you need to put your PXC headset (or other devices) into pairing more. To set your device (headset) into pairing mode `hold down the sound effect button` (on the right cap) for 4 seconds. The headset will tell you something like "Pairing...". You can use the `TAB` key to autocomplete the device IDs. You don't have to type them yourself, simply type the first characters and hit `TAB`.

```js
bluetoothctl

[bluetooth]# `power on`
[bluetooth]# `agent on`
[bluetooth]# `default-agent`
[bluetooth]# `scan on`

[NEW] Device 00:1D:43:6D:03:26 PXC 550

[bluetooth]# `pair 00:1D:43:6D:03:26`     -- pair with the device
[bluetooth]# `connect 00:1D:43:6D:03:26`  -- connect with the device
[bluetooth]# `trust 00:1D:43:6D:03:26`    -- trust the device

[bluetooth]# `scan off`
[bluetooth]# `exit`
```

Verify if your headset is working -- congratz!
