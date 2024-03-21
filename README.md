# Docker localhost-network

Creates a local Docker network using nginx-proxy as a reverse proxy to allow multiple local domain names to use the same standard 80 or 443 ports.

For example, instead of having to configure each local domain with an unused port, such as `yourdomain.localhost:8080` and `yourdomain2.localhost:8081`, the reverse proxy takes care of the ports so you can use clean domain names, such as `yourdomain.localhost` and `yourdomain2.localhost`.

## Installation

1. In the parent directory where you want to store your network files (such as `/Users/Name/Projects/Assets/Docker/`), run: `git clone git@github.com:jacobcassidy/docker-localhost-network.git`.
2. In the `docker-localhost-network` directory you cloned, run: `docker compose up -d` to create the container.

## Usage

- Include the network settings as a top-level element in each project's `compose.yaml` file:
  ```yaml
  networks:
    default:
      name: localhost-network
      external: true
  ```
- Don't include ports in the project's frontend services as the localhost-network will take care of them. Backend services, such as databases should use ports as normal.

> Example projects that use the localhost-network include [Docker WordPress Setup](https://github.com/jacobcassidy/docker-wordpress-setup) and [Docker Nginx PHP-FPM Setup](https://github.com/jacobcassidy/docker-nginx-phpfpm-setup).
