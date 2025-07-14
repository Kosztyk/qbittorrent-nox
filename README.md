![qbittorent](https://github.com/user-attachments/assets/5da8904d-1ea6-495e-a246-737d23272f4f)

# How to install qbittorent-nox linux native

# 1.Installing dependencies
```
sudo apt install dirmngr ca-certificates software-properties-common apt-transport-https
```

# 2. Install the repo

```
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable -y
sudo apt update
```

# 3. Install qbittorrent

```
sudo apt install -y qbittorrent-nox
```

# 4. Make sure the home exists
```
sudo mkdir -p /home/qbittorrent
```

# 5. Create the config path
```
sudo mkdir -p /home/qbittorrent/.config/qBittorrent
sudo mkdir -p /home/qbittorrent/.local/share/data/qBittorrent/BT_backup
```

# 6. Give ownership to the qbittorrent user
```
sudo chown -R qbittorrent:qbittorrent /home/qbittorrent
```
# 7. Create the service file 
```
nano /etc/systemd/system/qbittorrent.service
```
# 7a.Paste the bellow code:
```
[Unit]
Description=qBittorrent Command Line Client
After=network.target

[Service]
User=qbittorrent
Group=qbittorrent
Environment=HOME=/home/qbittorrent
Type=simple
ExecStart=/usr/bin/qbittorrent-nox --webui-port=8080
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
# 8. Start the service
```
sudo systemctl daemon-reload
sudo systemctl restart qbittorrent
```
# 9. Access the server
```
http://<server-IP>:8080/
```

# If needed find the admin password:
```
    journalctl -u qbittorrent.service | grep "temporary password"
```
