# Clove Tree

Makes a Raspberry Pi emulate a bluetooth keyboard. This is based on
[Emulating a Bluetooth Keyboard with Raspberry Pi and
Python](http://yetanotherpointlesstechblog.blogspot.com/2016/04/emulating-bluetooth-keyboard-with.html).

## Prerequisites

```sh
$ sudo cp btkeyboard/dbus/org.yaptb.btkkbservice.conf /etc/dbus-1/system.d
$ sudo apt-get install python3-pip python3-bluez python3-pyqt4 python3-dbus.mainloop.qt
$ pip3 install evdev
```

Set up Bluetooth:

```sh
$ sudo hciconfig hci0 up
```

Copy the Bluetooth MAC address and edit the MY_ADDRESS binding in
`btkeyboard/server/btk_server.py`.

Pairing:

```sh
$ sudo /usr/bin/bluetoothctl
> agent on
> default-agent
> scan on
> discoverable on
```

Pair from the host computer; type `yes` to accept the pairing request
on the pi.

## Running

Run the bluetooth daemon attached to a console with only the "time"
plugin:

```sh
$ sudo /etc/init.d/bluetooth stop
$ sudo /usr/sbin/bluetoothd --nodetach --debug -p time
```

## TODO

- OS X not responding to keystrokes
- Default plugins interfere with the port in the SDP; choose a different one.
- Automatic connections, see
[here](https://www.raspberrypi.org/forums/viewtopic.php?t=170353) or
[here](https://www.linuxquestions.org/questions/linux-wireless-networking-41/setting-up-bluez-with-a-passkey-pin-to-be-used-as-headset-for-iphone-816003/).