# VPS docker base

## Description
This is a base config for a VPS running docker images. It includes :
- Traefik, a reverse proxy and load balancer
- Portainer, a docker management tool

## Requirements
- A VPS with a public IP
- A domain name
- Docker and docker-compose installed on the VPS

## Installation
1. Clone this repository on your VPS
2. Copy the `.env.example` file to `.env` and fill the environment variables with your own values
    ```bash
    cp .env.example .env
    ```
3. Generate a password for the Traefik dashboard using (replace `<username>` with your chosen traefik username):
    ```bash
    htpasswd -n <username>
    ```
4. Copy the generated password and paste it in the `.env` file in `TRAEFIK_PASSWORD` variable
5. Fill the environment variable within the `.env` file with your own values
6. Generate the local certificates using:
    ```bash
    mkcert -cert-file traefik-config/certs/local-cert.pem -key-file traefik-config/certs/local-key.pem "*.docker.localhost" "*.local"
    ```
7. Create a docker network with name `proxy` to allow the services to communicate with each other: 
    ```bash
    docker network create proxy
    ```
8. Ensure that acme.json has the correct permissions
    ```bash
    chmod 600 traefik-config/acme.json
    ``` 
9. Run `docker-compose up -d` to start the services
10. Go to `https://portainer.yourdomain.com` and create a new admin user

## Usage
- Access the Traefik dashboard at `https://traefik.yourdomain.com`
- Access Portainer at `https://portainer.yourdomain.com`
