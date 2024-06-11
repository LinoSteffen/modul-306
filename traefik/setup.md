# Setup traefik with wordpress on docker

You can simply setup traefik (basic example) redirecting to wordpress with the `docker-compose.yaml` file.
```bash
docker-compose up -d
```

This will setup the traefik dashboard on `8080` and the wordpress instance on `80` on the hostsystem.