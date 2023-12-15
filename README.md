# clash-linux-backup

## clash
```bash
e71828@lab:~/Downloads$ cat /etc/systemd/system/clash.service
[Unit]
Description=A rule-based tunnel in go
After=network-online.target
[Service]
Type=simple
User=e71828
Group=LSP
UMask=007
ExecStart=/home/e71828/Downloads/clash-linux-amd64
Terminal=false
Restart=on-failure
# Configures the time to wait before service is stopped forcefully.
TimeoutStopSec=3000
[Install]
WantedBy=multi-user.target

e71828@lab:/etc$ ls /usr/share/applications/Clash.desktop
/usr/share/applications/Clash.desktop
e71828@lab:/etc$ cat  /usr/share/applications/Clash.desktop
[Desktop Entry]
Type=Application
Name=Clash
Comment=A rule-based tunnel in go
Exec=/home/e71828/Documents/go/clash
Icon=/usr/share/icons/clash.png
Terminal=false
Categories=Development;

e71828@lab:~/.config/clash$ sudo systemctl disable clash
e71828@lab:~/.config/clash$ tar -xvf yacd.tar.xz
e71828@lab:~/.config/clash$ ln -s public/ ui/
e71828@lab:~/.config/clash$ grep external config.yaml
external-controller: 0.0.0.0:9080
external-ui: ui
```

## clash subscribe
```bash
e71828@lab:~/.config/clash$ cat Scheduled.sh
#! /bin/bash
echo "yes"
cd /home/e71828/.config/clash
wget -O config.yaml https://yoyu.cc/subscribe/8171/**********/clash
sed -i '/^\s*external-controller/ c\external-controller: 0.0.0.0:9080' config.yaml
sed -i '/^\s*external-controller/ a\external-ui: ui' config.yaml
```
`crontab -l` display
`0 21 * * * /home/e71828/.config/clash/Scheduled.sh`


## Credits
- [Elegycloud/clash-for-linux-backup](https://github.com/Elegycloud/clash-for-linux-backup.git)
- [Dreamacro/maxmind-geoip](https://github.com/Dreamacro/maxmind-geoip.git)
- [haishanh/yacd](https://github.com/haishanh/yacd.git)
- [Dreamacro/clash](https://github.com/Dreamacro/clash.git)
