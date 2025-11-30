# traefik-docker-compose

Streamline microservices deployment with Traefik and Docker Compose.
And secure your website with security headers.

## Traefik

Traefik is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy. Traefik integrates with your existing infrastructure components and configures itself automatically and dynamically.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services.

## Usage

### Prerequisites

Make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Configuration

1. Clone the repository and navigate to it:

```bash
git clone https://github.com/Lindwen/traefik-docker-compose.git
cd traefik-docker-compose
```

1. Create `acme.json` file for traefik:

```bash
touch acme.json
chmod 600 acme.json
```

2. Copy `.env.example` to `.env` and edit the variables

```bash
cp .env.example .env
```

3. Edit `traefik.yml` and `configurations/security-headers.yml` and `configurations/tls.yml` to your needs

### Start

To start traefik:

```bash
docker compose up -d
```

### Stop

To stop the container:

```bash
docker compose down
```

### Logs

To view live logs:

```bash
docker compose logs -f
```

You can go to check your website to:
`https://${DOMAIN}`
And register with your user / password

### Add a service to the proxy

Need to be written.

## Need Help?

If you encounter any issues, need help, or have questions, please don't hesitate to reach out. You can create an [issue](https://github.com/Lindwen/traefik-docker-compose/issues/new) here on GitHub. We're here to assist you and improve this project based on your feedback.

### How to Create an Issue

1. Click on the "Issues" tab at the top of this repository.
2. Click the green "New Issue" button.
3. Provide a descriptive title and detailed description of the problem you're facing or the help you need.
4. Submit the issue, and we'll get back to you as soon as possible.

Your feedback is valuable, and we appreciate your contributions to making this project better.

---

### Thanks

- [PaulsBlog](https://www.paulsblog.dev/harden-your-website-with-traefik-and-security-headers/) - for the security headers
- [Solution-Libre](https://github.com/solution-libre/docker-traefik) - for the TLS file
