# Reliactyl 2.0

![Reliactyl](https://images-ext-1.discordapp.net/external/L4tPYgGXJv5POQ_PZ8hx3brzFYCRS6hH267cIaLQrvQ/https/repository-images.githubusercontent.com/467312432/1d1ed9e4-b8f4-4fdc-a5c1-933ca523b4c3?width=814&height=457)<br>

<h1>Features</h1>
- Allows users to split resources throughout multiple servers on the Pterodactyl Panel, and uses a Discord OAuth2 as a login system(updated).<br>
- Coins (AFK Page earning)<br>
- Coupons (Gives resources & coins to a user)<br>
- Servers (create, view, edit servers)<br>
- Store (buy resources with coins)<br>
- User System (auth, regen password, profile)<br>
- Join for Resources (join discord servers for resources)<br>
- API (for bots & other things)<br>
- Anti-ADBlock (BlockADBlock)<br>
- Multi-Lang Support(Soon)<br>

# Installination-Setup

<h2>Installing Dependencies</h2>

`sudo apt update && sudo apt upgrade`<br>
`sudo apt install git`<br>
`curl -fsSL https://deb.nodesource.com/setup_14.x | sudo bash -`<br>
`sudo apt install nodejs`<br>
`sudo apt install mariadb-server`<br>
`sudo mysql_secure_installation`<br>
`npm -v`<br>
`git clone https://github.com/reliactyldev/Reliactyl-2.0.git`<br>
`cd Reliactyl`<br>
`cp settings-template.yml settings.yml` <br>
`sudo nano settings.yml` and type all require settings<br>
`sudo npm install`<br>
`sudo apt install nginx`<br>
`sudo apt install certbot`<br>
`sudo apt install -y python3-certbot-nginx`

<h2>Database Setup</h2>

```Bash
mysql -u root -p

# After you've got that setup, let's go into the next step. Remember to change 'YourPasswordHere' with a secure password.

CREATE USER 'dashboard'@'%' IDENTIFIED BY 'YourPasswordHere';
CREATE DATABASE reliactyl;
GRANT ALL PRIVILEGES ON dashactyl.* TO 'dashboard'@'%' WITH GRANT OPTION;
quit;

```

<h2>Webserver Config</h2>

`systemctl start nginx`<br>
`certbot certonly --nginx -d your.domain`<br>
`sudo nano /etc/nginx/sites-enabled/reliactyl.conf`<br>
`# In reliactyl, paste this config and change the varible `

```Nginx
server {
  listen 80;
  server_name <domain_name>;
  return 301 https://$server_name$request_uri;
}
server {
  listen 443 ssl http2;

  server_name <domain_name>;
  ssl_certificate /etc/letsencrypt/live/<domain_name>/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/<domain_name>/privkey.pem;
  ssl_session_cache shared:SSL:10m;
  ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers  HIGH:!aNULL:!MD5;
  ssl_prefer_server_ciphers on;

  location /afkwspath {
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_pass "http://localhost:<port>/afkwspath";
  }

  location / {
    proxy_pass http://localhost:<port>/;
    proxy_buffering off;
    proxy_set_header X-Real-IP $remote_addr;
  }

  location = /arc-sw.js {
        proxy_pass https://arc.io;
        proxy_ssl_server_name on;
    }
}
```

<h2>Starting Reliactyl 2.0</h2>

1. Testing<br>
   `cd path/to/the/reliactyl`<br>
   `node index.js`<br>

2. Production<br>
   `cd path/to/the/reliactyl`<br>
   `npm install pm2 -g`<br>
   `pm2 start index.js`<br>
   `pm2 save`

# Join our [![Reliactyl](https://img.shields.io/badge/reliactyl-support%20server-7289da.svg)](https://discord.gg/9kz4n2F3th)
