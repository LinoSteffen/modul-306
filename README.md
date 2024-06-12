# modul-306

## Install docker
Remove any Docker files that are running in the system

`sudo apt remove docker docker-engine docker.io`

Check if the system is up-to-date

`sudo apt update`

Install Docker

`sudo apt install docker.io`


Install all the dependency 

`sudo snap install docker`

check the version

`docker --version`

### Executing the Docker Command Without Sudo 
Making the docker group 

`sudo groupadd docker`

add the user to the group

`sudo usermod -aG docker $USER`

reboot

`reboot`


## Install docker compose
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install docker compose

`sudo apt install docker-compose-plugin`

check version 

`docker compose version`
