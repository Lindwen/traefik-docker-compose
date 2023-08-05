# traefik-docker-compose

## Traefik

Traefik is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy. Traefik integrates with your existing infrastructure components and configures itself automatically and dynamically.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services.

## Usage

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)


### Configuration

```bash
# Clone the repository
git clone <repository>

# Change directory
cd <repository>

# Create data directory for the web service
mkdir data
# Create index.html file
echo "Hello World" > data/index.html
```

Configure traefik.toml file :
```toml
# Change the email address
[certificatesResolvers.letsencrypt.acme]
  email = "YOUR_EMAIL_ADDRESS"
```

Configure docker-compose.yml file :
```yml
# Change the domain name for the traefik and web service
- "traefik.http.routers.<service>.rule=Host(`YOUR_DOMAIN_NAME`)"
```

### Start

```bash
docker compose up -d
```

### Stop

```bash
docker compose down
```

### Logs

```bash
docker compose logs -f
```

---

### Thanks

* [PaulsBlog](https://www.paulsblog.dev/harden-your-website-with-traefik-and-security-headers/) - for the security headers