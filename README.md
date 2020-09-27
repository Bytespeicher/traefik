Install:

```bash
wget https://github.com/traefik/traefik/releases/download/v2.3.0/traefik_v2.3.0_linux_amd64.tar.gz

tar xfz traefik_v2.3.0_linux_amd64.tar.gz
rm traefik_v2.3.0_linux_amd64.tar.gz
sudo cp traefik /usr/local/bin
sudo chown root:root /usr/local/bin/traefik
sudo chmod 755 /usr/local/bin/traefik
sudo setcap 'cap_net_bind_service=+ep' /usr/local/bin/traefik

sudo groupadd -g 321 traefik
sudo useradd   -g traefik --no-user-group --home-dir /var/www --no-create-home   --shell /usr/sbin/nologin   --system --uid 321 traefik

sudo mkdir /etc/traefik /var/lib/traefik /var/log/traefik
sudo mkdir /etc/traefik/acme
sudo chown -R root:root /etc/traefik
sudo chown -R traefik:traefik /etc/traefik/acme

sudo touch /var/log/traefik/traefik.log
sudo chown traefik:traefik /var/log/traefik/traefik.log


git clone https://github.com/Bytespeicher/traefik

cd traefik
sudo mv *.toml /etc/traefik/
sudo chown root:root /etc/traefik/*.toml
sudo chmod 644 /etc/traefik/*.toml

sudo mv traefik.service /etc/systemd/system/
sudo chown root:root /etc/systemd/system/traefik.service
sudo chmod 644 /etc/systemd/system/traefik.service

sudo systemctl daemon-reload
sudo systemctl start traefik.service
sudo systemctl enable traefik.service
```
