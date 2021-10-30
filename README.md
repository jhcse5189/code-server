# code-server on ubuntu 18.04 LTS

- - -

## Install

- before, installing.
~~~
- clear nginx sites-available, sites-enable
- sudo apt remove code-server
~~~

~~~
curl -fsSL https://code-server.dev/install.sh | sh
sudo systemctl enable --now code-server@$USER

sudo vim code-server.conf
server {
        listen 80;
        listen [::]:80;
        server_name 52.78.235.235;
        location / {
                proxy_pass http://127.0.0.1:3000/;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection upgrade;
                proxy_set_header Accept-Encoding gzip;
        }
}
~~~

~~~
sudo ln -s /etc/nginx/sites-available/code-ser
ver.conf /etc/nginx/sites-enabled/code-server.conf
sudo nginx -t
sudo systemctl restart nginx

cat ~/.config/code-server/config.yaml
vim ~/.config/code-server/config.yaml
bind-addr: 127.0.0.1:8080
auth: password
password: (password)
cert: false

code-serer
-> can connect to (instance-ip)/login
~~~

~~~
- buy your domain, and add instance ip to A-record

sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python3-certbot-nginx

sudo vim /etc/nginx/sites-available/code-server.conf
server {
        listen 80;
        listen [::]:80;
        server_name <your domain>;
        location / {
                proxy_pass http://127.0.0.1:3000/;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection upgrade;
                proxy_set_header Accept-Encoding gzip;
        }
}

sudo nginx -t
sudo systemctl restart nginx
sudo certbot --nginx -d <your domain>
~~~


## Uninstall

~~~
sudo apt remove code-server
~~~

## Reference

- https://coder.com/docs/code-server/latest/install



