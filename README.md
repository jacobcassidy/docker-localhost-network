# Docker Localhost Network

These files create a local Docker network using nginx-proxy as a reverse proxy to allow multiple local domain names to use the same standard 80 or 443 ports.

For example, instead of having to configure each local domain with an unused port, such as `yourdomain.localhost:8080` and `yourdomain2.localhost:8081`, the reverse proxy takes care of the ports so you can use clean domain names, such as `yourdomain.localhost` and `yourdomain2.localhost`.

## Installation

1. In the parent directory where you want to store your Docker network files (such as `/Users/Username/Projects/Assets/Docker/`), run: `git clone git@github.com:jacobcassidy/docker-localhost-network.git`.
2. Open the [Docker Desktop](https://www.docker.com/products/docker-desktop/) app so the Docker engine is on.
3. In the `docker-localhost-network` directory you cloned, run: `docker compose up -d` to create and start the Docker container.

## Usage

- Include the network settings as a top-level element at the bottom of each project's `compose.yaml` file:
  ```yaml
  networks:
    default:
      name: localhost-network
      external: true
  ```
- Don't include ports in your project's Docker services that will run on port 80 or 443 because the localhost-network will take care of them. Other services, such as databases, should still use ports as usual.
- If you're using port 443 for the HTTPS protocol, you must create and add SSL certs for your local domains in the `/docker-localhost-network/certs` directory. You can do this by installing the command line tool [mkcert](https://github.com/FiloSottile/mkcert), then running the following command in the aforementioned directory: `mkcert yourlocaldomain.tld`. Make sure you replace "yourlocaldomain.tld" with the local domain name you are using for your project. After mkcert creates your certs, rename them from `yourlocaldomain.tld-key.pem` to `yourlocaldomain.tld.key` and `yourlocaldomain.tld.pem` to `yourlocaldomain.tld.crt`.

> Example projects that use the localhost-network include the [Docker WordPress Setup](https://github.com/jacobcassidy/docker-wordpress-setup) and the [Docker Nginx PHP-FPM Setup](https://github.com/jacobcassidy/docker-nginx-phpfpm-setup).
