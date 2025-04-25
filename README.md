# auth0-gateway-on-home-nas

## TL;DR

- Uses **OpenResty + Lua** as a drop-in alternative to nginx+ for OIDC negotiation.
- Relies on **Auth0** and **DuckDNS** to provide zero-cost auth and dynamic DNS for a home lab setup.

![auth_sequence.puml.svg](auth_sequence.puml.svg)

## Walkthrough

### Landscape

My online identity is Google-based, so I wanted SSO using my Google account.  
For experiments like this, I use a disposable identity (`<username>.spam@gmail.com`).

External providers involved:
- **Identity & Authentication:** [Auth0](https://auth0.com/)
- **Dynamic DNS:** [DuckDNS](https://duckdns.org/)
- **PKI (Certificates):** [Let's Encrypt](https://letsencrypt.org/)

Home setup:
- Synology NAS with Docker Compose support (upgraded RAM to handle multiple containers).
- ISP provides a public IPv4 lease, allowing external access with router port forwarding.
- NAS hosts the gateway, terminates TLS, and reverse-proxies traffic to internal services — only for authenticated users.

Internal traffic remains decrypted for easy capture and diagnostics.

### Background

Previously worked with HAProxy (TCP routing over Kubernetes) and NGINX+SPNEGO setups in corporate environments to enable SSO for internal tools.  
Always wanted a clean OAuth2 flow for personal projects at home.

### How It Was Done

- Followed tutorials for each provider (Auth0, DuckDNS, Let's Encrypt).
- Adapted the Auth0 OIDC flow for nginx+ to OpenResty+lua fork.
- Spent ~2 days vibing up a working prototype (with some AI assistance), and 2 more days cleaning it up to a standard.
