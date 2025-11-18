

# Docker Lab
 Step 1. Downloading Docker in your VM. 
		I personally used fedora, but https://docs.docker.com/engine/install/ . Docker Docs have installation guides for  different sources.

## Step 2: Terminal

First you want to uninstall these packages, before you can install Docker Engine

		sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
				  
Next, you want to set up the repository. To do so, implement these two lines of code

			sudo dnf -y install dnf-plugins-core
			sudo dnf-3 config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo

After you want to now install the Docker packages, 
To install the latest version run the commanded

		sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
		
Next you want to start you're Docker Engine by using the command

		sudo systemctl enable --now docker	

For verification, you can run the command 

		sudo docker run hello-world
If you see a text blob of commands that says Hello from Docker! in it, you know your docker is installed successfully

## Step 3. Uptime Kuma

From the options provided, that is not WordPress, I decided to use Uptime Kuma.

In order to start your gonna want to make a a Uptime Kuma folder and cd into it

		mkdir -p ~/uptime-kuma
		cd ~/uptime-kuma
		
After that is done, you are going to create the docker-compose.yml file. 

In order to get into the file your going to have to nano into it

			nano docker-compose.yml
			
Next Paste this command into it

	version: "3.9"

	services:
	  uptime-kuma:
 	   image: louislam/uptime-kuma:latest
 	   container_name: uptime-kuma
 	   volumes:
 	     - ./data:/app/data
	    ports:
	      - "3001:3001"
  	  restart: unless-stopped

In order to write and exit, your going to 
CTRL + O 
Press Enter
CTRL + X (leaving)

Next it starting up Uptime Kuma, for some of these commands I needed to use "sudo" in order for them to work

		docker compose up -d
		
This should have a download followed up by it

See if it is running

			docker ps
			
You should see a port in called uptime-kuma, if not make sure to go back and see if all is installed


## Step 4. On the Web

I personally used Firefox, but any internet browser should work. In the browser you are going have to put your vm_ip into it. 

To find you Ip you can run the command 

			ip route get 1.1.1.1
			
You will get a text line, the VM's IP is after the letters src

Next go onto your web browser 

			Type in : http://vm_ip:3001
			
You will be brought up the Uptime Kuma website, make an admin account with whatever username and password, and your done!


		






