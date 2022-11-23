# Setup a full Iris node on an Amazon AWS EC2

This document explains how to run a full Iris node an AWS EC2 instance running Amazon Linux 2. This guide can also apply to most substrate based nodes, with the IPFS specific steps beings extreneous. If you just want to get to the script, it's [here](../resources/scripts/ec2_setup.sh).

## Create an EC2 instance 
Create an EC2 instance with the amazon linux 2 AMI. We used a t2.micro.

### Configuring Security Groups
TODO: Verify 

Iris uses ports 9933, 9944, 9615, and 30333, so you must allow inbound/outbound traffic on those ports at least.

Additionally, if you're running the IPFS node as well, you can choose to allow the IPFS gateawy to be exposed from your instance as well by exposing the proper ports (default 8080).

### Setup Elastic IP (optional)
You'll find it useful to allocate an elastic IP to your EC2 instance. It's not required, but will save you time in the future to avoid your instance's IP changing. 

### Update instance

Update the EC2 instance's libraries to the latest versions.

``` bash
sudo yum update -y
sudo yum upgrade -y
```

## IPFS Installation and Configuration

The first thing we will do is install IPFS. 

``` bash
wget https://dist.ipfs.io/kubo/v0.14.0/kubo_v0.14.0_linux-amd64.tar.gz
tar -xvzf kubo_v0.14.0_linux-amd64.tar.gz
cd kubo
sudo bash install.sh
ipfs --version
```

### Configure IPFS
We'll make the IPFS API and Gateway listen on 0.0.0.0 instead of 127.0.0.1.

``` bash
ipfs config Addresses.API "/ip4/0.0.0.0/tcp/5001"
ipfs config Addresses.Gateway "/ip4/0.0.0.0/tcp/8080"
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin "[\"*\"]"
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Credentials "[\"true\"]"
```

### Setup as Service

Finally, setup IPFS as a system service. Doing this will allow you to enable IPFS to start when the instance starts. This is optional, however doing so is a good practice.

1. run `sudo nano /etc/systemd/system/ipfs.service`
 and paste the below file:
```
[Unit]
Description=IPFS Daemon
After=network.target

[Service]
User=ec2-user
Group=ec2-user
Environment=IPFS_PATH=/home/ec2-user/.ipfs
ExecStart=/usr/local/bin/ipfs daemon --init --migrate
StandardOutput=journal
Restart=on-failure
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target
```

and run the following:

``` bash
# to enable the service on startup
sudo systemctl enable ipfs
# to start the service
sudo systemctl start ipfs
# verify ipfs is running
sudo systemctl status ipfs 
```

*Note: your IPFS node's storage is limited by your EC2's storage capacity, so make sure you don't tell Iris you have more capacity than is provided.*

You can now use IPFS on your EC2! Try adding and fetching some data. However, we won't be able to securely communicate with our IFPS instance quite yet. We will need to install and configure Nginx, which we cover [here](#nginx-installation-and-configuration)

## Docker Installation and Configuration

``` bash
# install docker
sudo yum install docker
# add group membership for default user 
# (can avoid using `sudo docker ...` later (e.g. in a script))
sudo usermod -a -G docker ec2-user
id ec2-user
newgrp docker
# enable as system service at startup
sudo systemctl enable docker
# start service
sudo systemctl start docker
# verify running
sudo systemctl status docker
```

## Iris Installation and Configuration

``` bash
# pull the latest iris docker image
docker pull ideallabs/iris
# run your iris node
# there are many variations you can use to run your node
# see the [getting started guide](../quickstart/getting_started.md) for details
docker run --add-host host.docker.internal:host-gateway -p 9944:9944 \
  -p 9933:9933 \
  -p 30333:30333 \
  -p 9615:9615 \
  -it \
  --rm \
  --name iris-node \
  ideallabs/iris \
  --rpc-cors all --unsafe-ws-external --rpc-external --rpc-methods=unsafe --dev \
  --bootnodes /ip4/18.118.65.202/tcp/30333/p2p/12D3KooWEyoppNCUx8Yx66oV9fJnriXwCcXwDDUA2kj6vnc6iDEp
```

### Setup as service

## Nginx and Certbot Installation and Configuration

### install nginx
``` bash
sudo amazon-linux-extras install -y nginx1
# enable as system service
sudo systemctl enable nginx
# start service
sudo systemctl start nginx
```

### setup certs with certbot
Follow the guide here to create certs for your instance: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-2.html#letsencrypt.

You can find your nginx config at `/etc/nginx/nginx.conf`.
And then paste the server blocks:

``` 
server {

  server_name <your server name>;

  root /var/www/html;
  index index.html;

  location / {
    try_files $uri $uri/ =404;

    proxy_buffering off;
    proxy_pass http://localhost:9944;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
  }

  listen [::]:443 ssl ipv6only=on;
  listen 443 ssl;
  ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
  ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

  ssl_session_cache shared:cache_nginx_SSL:1m;
  ssl_session_timeout 1440m;

  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_prefer_server_ciphers on;

  ssl_ciphers "ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS";

  ssl_dhparam /etc/ssl/certs/dhparam.pem;
}
```