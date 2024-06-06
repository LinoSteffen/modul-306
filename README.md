# modul-306

## Install docker



## Install docker-compose
Install docker-compose
`sudo apt-get install docker-compose-plugin`
https://linosteffen.slab.com/posts/install-docker-compose-u69q6am4

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