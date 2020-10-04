Install:

```bash
wget https://github.com/traefik/traefik/releases/download/v2.3.1/traefik_v2.3.1_linux_amd64.tar.gz

sudo mkdir /opt/traefik
sudo mkdir -p /etc/traefik/{acme,conf}
sudo mkdir /var/log/traefik

sudo tar -xvzf traefik_v2.3.1_linux_amd64.tar.gz --directory=/opt/traefik
rm traefik_v2.3.1_linux_amd64.tar.gz

sudo groupadd --gid 321 traefik
sudo useradd --gid traefik --no-user-group --home-dir /opt/traefik --no-create-home --shell /usr/sbin/nologin --system --uid 321 traefik

git clone https://github.com/Bytespeicher/traefik
sudo cp -R traefik/etc/traefik /etc/traefik
sudp cp traefik/etc/systemd/system/traefik.service /etc/systemd/system/
sudo cp traefik/etc/logrotate.d/traefik /etc/logrotate.d/

sudo chown -R traefik:traefik /{opt,etc,var/log}/traefik
sudo chmod 750 /opt/traefik/traefik
sudo chmod 644 /etc/systemd/system/traefik.service
sudo chown root:root /etc/systemd/system/traefik.service
sudo chmod 644 /etc/logrotate.d/traefik
sudo chown root:root /etc/logrotate.d/traefik

sudo systemctl daemon-reload
sudo systemctl enable --now traefik.service
```
