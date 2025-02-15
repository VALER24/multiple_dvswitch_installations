# multiple_dvswitch_installations

```
cp /opt/MMDVM_Bridge/ /opt/MMDVM_Bridge2/ -r
cp /opt/Analog_Bridge/ /opt/Analog_Bridge2/ -r
cp /opt/md380-emu/ /opt/md380-emu2/ -r

mkdir /var/log/mmdvm2
mkdir /var/log/dvswitch2

cp /lib/systemd/system/mmdvm_bridge.service /lib/systemd/system/mmdvm_bridge2.service

cp /lib/systemd/system/analog_bridge.service /lib/systemd/system/analog_bridge2.service

cp /lib/systemd/system/md380-emu.service /lib/systemd/system/md380-emu2.service
```
nano /lib/systemd/system/mmdvm_bridge2.service

Look for the following lines and edit:

WorkingDirectory=/opt/MMDVM_Bridge2

Environment=DVSwitch=/opt/MMDVM_Bridge2/DVSwitch.ini

ExecStart=/opt/MMDVM_Bridge2/MMDVM_Bridge /opt/MMDVM_Bridge2/MMDVM_Bridge.ini

Remember to save your file (in Nano, it’s Ctrl-X, then Y, then enter). If you are not root or superuser, sudo to edit the item as root.

--

# nano /lib/systemd/system/analog_bridge2.service

Look for these lines and edit accordingly.

WorkingDirectory=/opt/Analog_Bridge2

Environment=AnalogBridgeLogDir=/var/log/dvswitch2

ExecStart=/opt/Analog_Bridge2/Analog_Bridge /opt/Analog_Bridge2/Analog_Bridge.ini

# nano /lib/systemd/system/md380-emu2.service

WorkingDirectory=/opt/md380-emu2

ExecStart=/opt/md380-emu2/md380-emu -S 2472

The “2472” above is the port of the MD380 emulator we will use on Analog_Bridge. Take note of it.
