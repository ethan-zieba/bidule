To install nginx:
```
sudo apt update
sudo apt install nginx
```

To create a self-signed certificate:
`sudo mkdir -p /etc/nginx/ssl`
`cd /etc/nginx/ssl`
`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./nginx-selfsigned.key -out ./nginx-selfsigned.crt -subj "/C=FR/ST=Provence/L=Marseille/O=LaPlateforme/OU=LaPlateforme/CN=localhost"`

Then edit the conf:
`sudo vim /etc/nginx/sites-available/default`

Add:
```
server {
    listen 443 ssl default_server;
    listen [::]:443 ssl default_server;

    ssl_certificate /etc/nginx/ssl/nginx-selfsigned.crt;
    ssl_certificate_key /etc/nginx/ssl/nginx-selfsigned.key;

    root /var/www/html;
    index index.html;

    server_name _;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Test and restart:
```
sudo nginx -t
sudo systemctl restart nginx
```
