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
2. Generate an encrypted password to protect the access to the Traefik dashboard using :
```bash
htpasswd -n username
```
3. Copy the generated password and paste it in the `.env` file in `TRAEFIK_PASSWORD` variable
4. Fill the environment variable within the `.env` file with your own values
5. Generate the local certificates using:
```bash
mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem "*.docker.localhost" "*.local"
```
5. Run `docker-compose up -f docker-compose.traefik -d` to start the services
6. Go to `https://portainer.yourdomain.com` and create a new admin user

## Usage
- Access the Traefik dashboard at `https://traefik.yourdomain.com`
- Access Portainer at `https://portainer.yourdomain.com`
