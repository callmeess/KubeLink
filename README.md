# KubeLink

A URL shortening service with authentication, built on a microservices architecture deployed to Kubernetes.

## Reverse Proxy

This project uses [Traefik](https://traefik.io/) as its ingress controller and reverse proxy. The Traefik configuration is located in `k8s/traefik/` and includes:

- **IngressRoute** (`ingressroute.yaml`): Routes requests to the appropriate backend services.
- **Middleware** (`middleware.yaml`): Handles JWT authentication (via ForwardAuth) and the root redirect.

### Routes

| Path | Service | Auth |
|------|---------|------|
| `/shorten/` | url-shortener-service (port 80) | JWT required |
| `/api/Auth/register/` | auth-service (port 80) | None |
| `/` | Redirect to `/api/Auth/` (302) | None |
