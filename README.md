# Init  
`cd /opt`  
`sudo apt-get update`  
`sudo apt-get install ca-certificates curl gnupg lsb-release git`  
# Docker  
`sudo curl -fsSL https://get.docker.com -o get-docker.sh`  
`sh get-docker.sh`  
`docker --version`  
# Docker-compose  
`sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`  
`sudo chmod +x /usr/local/bin/docker-compose`  
# Clone repo  
`sudo git clone https://github.com/pontem-network/bootstrap.git pontem-bootstrap`  
`cd pontem-bootstrap`  
# Set environment in .env  
`sudo cp .env.testnet .env`  
# Generate keys  
`sudo docker-compose pull`  

Now you need to generate an mnemonic phrase for your account (if you don't have one):  
`sudo docker-compose run pontem-node pontem key generate --scheme sr25519`  
`sudo docker-compose run pontem-node pontem key insert --suri "<you_mnemonic>" --keystore-path /opt/pontem/keys --key-type nmbs`  
# Become collator  
https://www.youtube.com/watch?v=KBfXZt_vjPc  
05:30 - 10:55  
# Launch node  
`sudo docker-compose up -d`  
`sudo docker-compose logs -f --tail 10`  
# Monitoring  
`sudo docker-compose -f monitoring.docker-compose.yml up -d`  

On the browser  
`<IP>:3000`  
(user: admin, password: admin)  
# Node autorestart  
`sudo docker run -d --name autorestart-pontem --restart always -v /var/run/docker.sock:/var/run/docker.sock pontem/pontem-scripts:latest autorestart pontem-node 300 5`  
`sudo docker-compose up -d`  
