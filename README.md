# caddy

Automated caddy server container image build with acmeproxy plug-in.

## Local test

    podman build -t localhost/caddy .

    podman network create caddy
    podman run --rm --name caddy --network caddy -d -p 443:443 -p 80:80 -v ./config:/etc/caddy localhost/caddy
    podman run --rm --name whoami0 --network caddy -d traefik/whoami

    # Test reverse proxy
    curl -k --resolve whoami0.owny.cz:443:127.0.0.1 https://whoami0.owny.cz

    # Graceful caddy reload without restarting container
    alias caddy-reload="podman exec -w /etc/caddy caddy caddy reload"
