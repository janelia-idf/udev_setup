#udev_setup

Authors:

    Peter Polidoro <peterpolidoro@gmail.com>

License:

    BSD

Information about USB devices:

```shell
lsusb
```

Information about last USB device connected:

```shell
tail /var/log/syslog
```

Find idVendor, idProduct, and serial of USB device:

```shell
udevadm info -a -n /dev/ttyUSB0 | grep '{idVendor}' | head -n1
udevadm info -a -n /dev/ttyUSB0 | grep '{idProduct}' | head -n1
udevadm info -a -n /dev/ttyUSB0 | grep '{serial}' | head -n1
```

Example USB serial rules file:

```shell
sudo touch /etc/udev/rules.d/99-usb-serial.rules
sudo echo 'SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A6008isP", SYMLINK+="arduino"' >> /etc/udev/rules.d/99-usb-serial.rules
sudo echo 'SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A7004IXj", SYMLINK+="buspirate"' >> /etc/udev/rules.d/99-usb-serial.rules
sudo echo 'SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="FTDIF46B", SYMLINK+="ttyUSB.ARM"' >> /etc/udev/rules.d/99-usb-serial.rules
```
