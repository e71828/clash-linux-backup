# clash-linux-backup

Clash Webui: [`lab:9080/ui`](http://192.168.31.163:9080/ui)

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


## geoipupdate

### upadte for windows

```bash
e71828@VITASOY MINGW64 ~/3D Objects/geoipupdate_7.0.1_windows_amd64
$ ./geoipupdate.exe -d ~/.config/clash -v
geoipupdate version 7.0.1 (0df16c46-modified, 2024-04-08T21:30:02Z, windows-amd64)
Using config file C:\ProgramData\MaxMind\GeoIPUpdate\GeoIP.conf
Using database directory C:\Users\admin\.config\clash
Initializing file lock at C:\Users\admin\.config\clash\.geoipupdate.lock
Acquired lock file at C:\Users\admin\.config\clash\.geoipupdate.lock
Calculated MD5 sum for C:\Users\admin\.config\clash\GeoLite2-ASN.mmdb: d9d7d0e9c12396dcbe0fd5a560d3a200
No new updates available for GeoLite2-ASN
Database GeoLite2-ASN up to date
Database does not exist, returning zeroed hash
Updates available for GeoLite2-City
Database GeoLite2-City successfully updated: 3306f902a744b5517626d876ab4ef19a
Calculated MD5 sum for C:\Users\admin\.config\clash\GeoLite2-Country.mmdb: d721c71dded9c86a1fd80c93b4ec73c9
No new updates available for GeoLite2-Country
Database GeoLite2-Country up to date
Lock file C:\Users\admin\.config\clash\.geoipupdate.lock successfully released
```

### rename the `mmdb`

```bash
e71828@VITASOY MINGW64 ~/.config/clash
$ mv GeoLite2-Country.mmdb Country.mmdb
```

## Credits
- [Elegycloud/clash-for-linux-backup](https://github.com/Elegycloud/clash-for-linux-backup.git)
- [Dreamacro/maxmind-geoip](https://github.com/Dreamacro/maxmind-geoip.git)
- [haishanh/yacd](https://github.com/haishanh/yacd.git)
- [Dreamacro/clash](https://github.com/Dreamacro/clash.git)
- [maxmind/geoipupdate](https://github.com/maxmind/geoipupdate)
