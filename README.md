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
Install docker compose

`sudo apt install docker-compose-plugin`

check version 

`docker compose version`