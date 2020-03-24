# Traefik Proxy
Reverse Proxy für Docker Container, welche als Subdomains registriert werden

## Setup
1. .htpasswd erstellen für den Zugriff auf das Traefik Dashboard
2. Env Variable BASE_DOMAIN in /etc/environment erstellen um die Basis Domain für Container Subdomains festzulegen
3. run.sh oder run-dev.sh ausführen

## Monitoring
https://BASE_DOMAIN:8080
Login mit eingestelltem Passwort der .htpasswd

## Hinzufügen von Usern
```
htpasswd .htpasswd USERNAME
```

Nach dem Hinzufügen muss der Traefik Container neu gestartet werden, damit der neue User von Traefik erkannt wird.

## Docker Labels
Zum Konfigurieren der Container zur Nutzung von Traefik folgende Labels nutzen:

```
traefik.enable=true
traefik.docker.network=intranet
traefik.port=REPLACE_ME
traefik.protocol=REPLACE_ME
traefik.frontend.rule=Host:REPLACE_ME.${BASE_DOMAIN}
```

- Network: Netzwerk in welchem sich der Container befindet. Auf dem DEV Server muss hier skynet eingetragen werden. Es greift nicht der Alias der im Docker-compose File eingetragen wurde
- Port: Port auf welchem der Container kontaktiert wird. Normalerweise 80 oder 443
- Protocol: http oder https
- Frontend.Rule: URL des vHosts in Traefik.
