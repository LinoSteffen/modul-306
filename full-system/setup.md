# Setup bind, webmin, traefik, and wordpress on Docker

To install the full system, just start the `docker-compose.yaml` file:
```bash
docker-compose up -d
```

On the host system you are testing it, you will need to add the DNS server to the `/etc/resolv.conf`:
```bash
nameserver <serverhostip>
```

This will set up the following:
- Traefik dashboard on `http://traefik.somedomain.ch`
- WordPress instance on `http://wordpress.somedomain.ch`
- Portainer on `http://portainer.somedomain.ch`
- Webmin on `http://webmin.somedomain.ch`

Additionally, you can access Webmin directly via port 10000 on the host system.

## Configuring DNS Entries in Webmin

1. Access Webmin:
   Open your browser and navigate to `http://webmin.somedomain.ch:10000` or `http://<serverhostip>:10000` initially.

2. Login:
   Use the username `root` and the password `sml12345`.

3. Create a New Zone:
   - Navigate to `Servers` -> `BIND DNS Server`.
   - Click `Create master zone`.
   - Enter your domain name (e.g., `somedomain.ch`).
   - Set the `Master server` to `ns1.somedomain.ch`.
   - Click `Create`.

4. Add DNS Records:
   - After creating the zone, click on the domain name to edit it.
   - Add an `A` record for `ns1`:
     - Name: `ns1`
     - Address: `<serverhostip>`
     - Click `Create`.
   - Add an `A` record for `traefik`:
     - Name: `traefik`
     - Address: `<serverhostip>`
     - Click `Create`.
   - Add an `A` record for `wordpress`:
     - Name: `wordpress`
     - Address: `<serverhostip>`
     - Click `Create`.
   - Add an `A` record for `portainer`:
     - Name: `portainer`
     - Address: `<serverhostip>`
     - Click `Create`.
   - Add an `A` record for `webmin`:
     - Name: `webmin`
     - Address: `<serverhostip>`
     - Click `Create`.

5. Apply Configuration:
   - Click `Apply Configuration` to reload the DNS server with your new settings.

Now your DNS server should correctly resolve the domains `traefik.somedomain.ch`, `wordpress.somedomain.ch`, `portainer.somedomain.ch` and `webmin.somedomain.ch` to your server's IP address.
