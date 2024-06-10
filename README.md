# modul-306

## Install docker
Remove any Docker files that are running in the system

`sudo apt-get remove docker docker-engine docker.io`

Check if the system is up-to-date

`sudo apt-get update`

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

`sudo apt-get install docker-compose-plugin`

check version 

`docker compose version`

### login to docker
`docker login`


## compose portainer
`docker compose -f portainer-compose.yaml up -d`

go to [http://localhost:9443](http://localhost:9443)


## compose wordpress
`docker compose -f wordpress-compose.yaml up -d`

go to [http://localhost:80](http://localhost:80)

## compose website on webflow
xx