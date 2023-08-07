# traefik-docker-compose

Streamline microservices deployment with Traefik and Docker Compose.
And secure your website with security headers.

* Score on : [securityheaders.com](https://securityheaders.com/)
![securityheaders_score](docs/img/securityheaders_score.png)

* Score on : [observatory.mozilla.org](https://observatory.mozilla.org/)
![observatory_score](docs/img/observatory_score.png)

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

3. Configure the `traefik.toml` file by changing the email address:

```toml
# Change the email address
[certificatesResolvers.letsencrypt.acme]
  email = "YOUR_EMAIL_ADDRESS"
```

4. Configure labels:

Edit `docker-compose.yml` and `example/docker-compose.yml` :
```bash
vi docker-compose.yml
```

```yml
# Change the domain name
- "traefik.http.routers.<service>.rule=Host(`YOUR_DOMAIN_NAME`)"
# example:
- "traefik.http.routers.example.rule=Host(`test.example.com`)"

# Port configuration if the container don't expose port 80
- "traefik.http.services.<service>.loadbalancer.server.port=<port>"
# example: (3000 = grafana)
- "traefik.http.services.example.loadbalancer.server.port=3000"


# Add auth (just for traefik)
- "traefik.http.routers.<service>.middlewares=auth"
- "traefik.http.middlewares.auth.basicauth.users=<username>:<password>" # password generated with htpasswd (Bcrypt) and double $
# example:
- "traefik.http.routers.example.middlewares=auth"
- "traefik.http.middlewares.auth.basicauth.users=Example:$$2a$$10$$Bls.hNkCW3m4lBz9a592IOfom6U0dmFvIP9UUz.4VWbWF0x8Kn3WG"

# Add contentSecurityPolicy
# You need to custom this
- "traefik.http.routers.<service>.middlewares=security-headers@file, <service>-csp"
- "traefik.http.middlewares.<service>-csp.headers.contentSecurityPolicy=<policies>"
# example:
- "traefik.http.routers.example.middlewares=security-headers@file, example-csp"
- "traefik.http.middlewares.example-csp.headers.contentSecurityPolicy=default-src 'none'; script-src 'self' https://traefik.github.io; connect-src 'self'; img-src 'self' data:; style-src 'self'; font-src 'self'; object-src 'none'; frame-ancestors 'none'; form-action 'none'; base-uri 'none';"
```

5. ⚠️ WARNING: the `tls@file` block ssl activation by letsencrypt.
If you want to use ssl, you need to comment this line in docker-compose.yml and uncomment after the first start of the containers.

```toml
# - "traefik.http.routers.<service>.tls.options=tls@file"
```

7. DNS configuration

For this example, I made the following DNS configuration:

```bash
# A record
*.domain.tld A IP_ADDRESS_OF_YOUR_SERVER
```
To check the propagation of your DNS, you can use [dnschecker.org](https://dnschecker.org/) or [whatsmydns.net](https://www.whatsmydns.net/).

### Start

To start traefik:

```bash
docker compose up -d
```

To start the example container:
```bash
cd example
docker compose up -d
```

### Stop

To stop the containers:

```bash
docker compose down
```

### Logs

To view live logs:

```bash
docker compose logs -f
```

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

* [PaulsBlog](https://www.paulsblog.dev/harden-your-website-with-traefik-and-security-headers/) - for the security headers
* [Solution-Libre](https://github.com/solution-libre/docker-traefik) - for the TLS file