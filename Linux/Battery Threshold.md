## Config Battery Threshold

1. Detect if the battery is detected by de operative system
```bash
ls /sys/class/power_supply
```
The result of this command must to be the list of power supplies devices AC0 or BAT0

2. Create a systemd service to set the battery charge stop threshold on boot
```bash
ls /sys/class/power_supply/BAT0/charge_control_end_threshold
```
If the command return the file, the the laptop supports limiting battery charging

 Create a file in systemd
```bash
sudo nano /etc/systemd/system/battery-charge-threshold.service
```
with the next conten:
```bash
[Unit]
Description=Set the battery charge threshold
After=multi-user.target
StartLimitBurst=0

[Service]
Type=oneshot
Restart=on-failure
ExecStart=/bin/bash -c 'echo 80 > /sys/class/power_supply/BAT0/charge_control_end_threshold'

[Install]
WantedBy=multi-user.target
```

3. Enable and start the battery-charge-threshold systemd service
```bash
sudo systemctl enable battery-charge-threshold.service
sudo systemctl start battery-charge-threshold.service
```

If you want to change the battery charge stop threshold level , you'll need to edit the `/etc/systemd/system/battery-charge-threshold.service` file, and change the number from the `ExecStart` line (after `echo`) to the new value you want to use, then reload systemd (because the file contents have changed) and restart the systemd service using the following commands:

```bash
sudo systemctl daemon-reload
sudo systemctl restart battery-charge-threshold.service
```