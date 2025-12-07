
I used Ubuntu as my distro of choice. 

Downloading Docker by using DockerDocs, then going to ubuntu installation

Uninstall all conflicting packages:

		sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc | cut -f1)
		
		
Set up Docker apt repository, Copy and paste into terminal.

		# Add Docker's official GPG key: sudo apt update sudo apt install ca-certificates curl sudo install -m 0755 -d /etc/apt/keyrings sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc sudo chmod a+r /etc/apt/keyrings/docker.asc # Add the repository to Apt sources: sudo tee /etc/apt/sources.list.d/docker.sources <<EOF Types: deb URIs: https://download.docker.com/linux/ubuntu Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") Components: stable Signed-By: /etc/apt/keyrings/docker.asc EOF sudo apt update
		

Installing Docker Packages.

	sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	
Verify if running

	sudo systemctl status docker
	
Then verify bye running test message:

	sudo docker run hello-world
	

Now finally Starting DockerVPN project:


Make a DigitalOcean.com Account sign up with link for 200$ credit.

Make Droplet, at least $6/month, then make ssh or password

ssh into droplet IP

Installing Wireguard in ubuntu:

	$ sudo apt install wireguard

Make new directory then go into it

	Mkdir wg then cd wg

Then 

	nano docker-compose.yml.

Copy and paste text into docker-compose.yml

	
version: "3.8"
services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Chicago
      - SERVERURL=<157.230.140.219>
      - SERVERPORT=51820
      - PEERS=2
    volumes:
      - ./config:/config
    ports:
      - 51820:51820/udp
    restart: unless-stopped

Then run the command:

	docker compose up -d
	
Finally test the VPN with QR code so you can do it on mobile device

Showing IP before then with Wireguard on.

