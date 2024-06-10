# Docker Compose Cheat Sheet

## Basic Commands
- **Start services in detached mode:** `docker-compose up -d`
- **Stop services:** `docker-compose down`
- **Restart services:** `docker-compose restart`
- **View running services:** `docker-compose ps`
- **Build or rebuild services:** `docker-compose build`
- **Rebuild and start services:** `docker-compose up -d --build`
- **Scale services:** `docker-compose up -d --scale service_name=n`

## Viewing Logs
- **All services:** `docker-compose logs`
- **Specific service:** `docker-compose logs service_name`
- **Follow logs (real-time):** `docker-compose logs -f`
- **Follow logs for a specific service:** `docker-compose logs -f service_name`

## Specifying a Compose File
- **Specify a different compose file:** `docker-compose -f custom-docker-compose.yml up -d`

## Executing Commands in Containers
- **Access a running container:** `docker exec -it container_name_or_id sh`
- **Run a command in a service's container:** `docker-compose exec service_name command`
  - Example: `docker-compose exec web bash`

## Miscellaneous
- **List all containers (including stopped ones):** `docker ps -a`
- **Remove stopped containers:** `docker-compose rm`
- **List images:** `docker images`
- **Remove unused images:** `docker image prune`