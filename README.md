# File_browser_setup_VPS
File browser setup VPS

---

1. Download and Install
- Connect to your VPS via SSH and run the official install script:
  ```bash
  curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash
  ```

2. Create a Systemd Service
- To keep File Browser running in the background and start it automatically on boot, create a service file:
  ```bash
  sudo nano /etc/systemd/system/filebrowser.service
  ```
- Paste the following configuration into the file. Make sure to adjust the paths and port to your preference:
```ini
[Unit]
Description=File Browser
After=network.target

[Service]
ExecStart=/usr/local/bin/filebrowser -r /srv -p 8080 --address 0.0.0.0 --database /etc/filebrowser/filebrowser.db
Restart=on-failure
User=root
Group=root

[Install]
WantedBy=multi-user.target
```
---

```bash
# Create New File and Permisions
touch filebrowser.db
chmod 666 filebrowser.db

# Start container
docker run -d \
  --name=filebrowser \
  --user root \
  -v /var/www:/srv \
  -v $(pwd)/config/settings.json:/.filebrowser.json \
  -v $(pwd)/filebrowser.db:/database/filebrowser.db \
  -p 8085:80 \
  filebrowser/filebrowser:latest

# Check if it works you will see the username and password.
sleep 3
docker logs filebrowser
docker ps | grep filebrowser
```
