# Cloud Root

This host is meant to be a low-cost VM to handle "global" functions. So managing VPNs, remote management services and a reverse proxy.  
Many commands may be copy pasted from reference material, but I'm assuming everything was run as `root`.  
VM may need a second IP to run Teleport.

!> TODO Automate this entire process

[docker](common/docker.md ':include')

## Utility Containers

### Autoheal

[autoheal](compose/autoheal.yml ':include :type=code yaml')

## Setup dnsrobocert

This is for seeding our first wildcard certificates as needed.

https://github.com/adferrand/dnsrobocert

!> TODO Turn this into a CI/CD job and prepare a distribution method

### Prepare env_file

[dnsrobocert.env](compose/dnsrobocert/dnsrobocert.env ':include :type=code bash')

### Prepare compose file

[dnsrobocert.yml](compose/dnsrobocert/dnsrobocert.yml ':include :type=code yaml')

### Prepare config file

[Docs](https://dnsrobocert.readthedocs.io/en/latest/configuration_reference.html)

[dnsrobocert-config.yml](compose/dnsrobocert/config.yml ':include :type=code yaml')

### Launch

```bash
cd /srv/compose && docker-compose up -d
```

## Setup traefik

Reverse proxy

### Prepare env_file

[traefik.env](compose/traefik/traefik.env ':include :type=code bash')

### Prepare compose file

[traefik.yml](compose/traefik/traefik.yml ':include :type=code yaml')

### Prepare config files

[Docs](https://doc.traefik.io/traefik/)

#### Manual cert files and/or dnsrobocert

[traefik-config-tls.yml](compose/traefik/config-tls.yml ':include :type=code yaml')

#### LetsEncrypt

[traefik-config-letsencrypt.yml](compose/traefik/config-letsencrypt.yml ':include :type=code yaml')

### Launch

```bash
cd /srv/compose && docker-compose up -d
```

## Setup lldap

User database

### Set some .env config
```shell
# /srv/compose/.env
ROOT_DOMAIN=""

LDAP_BASE_DN="dc=traefik,dc=me"
LLDAP_PSQL_PASSWORD=""
LLDAP_JWT_SECRET=""
LLDAP_KEY_SEED=""
```

### Prepare compose file
!> Once `docker-mailserver` is online, the `LLDAP_SMTP_OPTIONS` section can be configured for sending mail. A user will need to be created for it.

[lldap.yml](compose/lldap.yml ':include :type=code yaml')

## Setup docker-mailserver
### Prepare compose file

[docker-mailserver.yml](compose/docker-mailserver.yml ':include :type=code yaml')

## Setup Authelia
OpenID Single Sign On Portal

### Prepare compose file
!> Authelia may not be happy starting up until there is an OIDC client configured

[authelia.yml](compose/authelia.yml ':include :type=code yaml')


## Setup Homepage
Simple at-a-glance dashboard

### Prepare compose file

[homepage.yml](compose/homepage.yml ':include :type=code yaml')

## Setup Headscale
VPN mesh solution.

### Prepare configuration

!> This is mostly copy-pasted from upstream example, still needs oidc configured

[headscale-config.yml](compose/headscale/config.yaml ':include :type=code yaml')

### Add configuration to authelia

!> This is just copy-pasted from upstream example, still needs configuring

[authelia-headscale.yml](compose/headscale/authelia.yml ':include :type=code yaml')

### Prepare compose file

[headscale.yml](compose/headscale/headscale.yml ':include :type=code yaml')


## Setup Teleport
Centralized remote shell

### Prepare compose file

[teleport.yml](compose/teleport/teleport.yml ':include :type=code yaml')

### Prepare config file

[teleport-config.yml](compose/teleport/config.yaml ':include :type=code yaml')
