# File_browser_setup_VPS
File browser setup VPS

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
