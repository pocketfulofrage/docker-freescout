# docker-freescout
Docker image for FreeScout - and open source helpdesk

# hub.docker.com/r/pocketfulofrage/freescout

[![Build Status](https://img.shields.io/docker/cloud/build/pocketfulofrage/freescout)](https://hub.docker.com/r/pocketfulofrage/freescout)
[![Docker Pulls](https://img.shields.io/docker/pulls/pocketfulofrage/freescout)](https://hub.docker.com/r/pocketfulofrage/freescout)
[![Docker Stars](https://img.shields.io/docker/stars/pocketfulofrage/freescout)](https://hub.docker.com/r/pocketfulofrage/freescout)


# Introduction

This will build a container for [Freescout](https://freescout.net/) - An open source Helpscout / Zendesk alternative.

* Automatically installs and sets up installation upon first start
        
This Container uses [tiredofit/alpine:3.8](https://hub.docker.com/r/tiredofit/alpine) as a base.


[Changelog](CHANGELOG.md)

# Authors

- [Dave Conroy](https://github.com/tiredofit)
- [Russ Bryan](https://github.com/pocketfulofrage) - (fixes, updates)

# Table of Contents

- [Introduction](#introduction)
    - [Changelog](CHANGELOG.md)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
    - [Data Volumes](#data-volumes)
    - [Environment Variables](#environmentvariables)   
    - [Networking](#networking)
- [Maintenance](#maintenance)
    - [Shell Access](#shell-access)
   - [References](#references)

# Prerequisites

This image assumes that you are using a reverse proxy such as 
[jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) and optionally the [Let's Encrypt Proxy 
Companion @ 
https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) 
in order to serve your pages. However, it will run just fine on it's own if you map appropriate ports. See the examples folder for a docker-compose.yml that does not rely on a reverse proxy.

You will also need an external MySQL/MariaDB Container

# Installation

Automated builds of the image are available on [Docker Hub](https://hub.docker.com/r/tiredofit/freescout) and is the recommended method of installation.


```bash
docker pull pocketfulofrage/freescout
```

# Quick Start

* The quickest way to get started is using [docker-compose](https://docs.docker.com/compose/). See the examples folder for a working [docker-compose.yml](examples/docker-compose.yml) that can be modified for development or production use.

* Set various [environment variables](#environment-variables) to understand the capabilities of this image.
* Map [persistent storage](#data-volumes) for access to configuration and data files for backup.
* Make [networking ports](#networking) available for public access if necessary

*The first boot can take from 2 minutes - 5 minutes depending on your CPU to setup the proper schemas.

Login to the web server and enter in your admin email address, admin password and start configuring the system!

# Configuration

### Data-Volumes

The following directories are used for configuration and can be mapped for persistent storage.

| Directory    | Description                                                 |
|--------------|-------------------------------------------------------------|
| `/www/logs` | Nginx and PHP Log files |

### Environment Variables

Along with the Environment Variables from the [Base image](https://hub.docker.com/r/tiredofit/alpine), below is the complete list of available options that can be used to customize your installation.

| Parameter        | Description                            |
|------------------|----------------------------------------|
| `ADMIN_EMAIL` | Administrator Email Address - Needed for logging in |
| `ADMIN_FIRST_NAME` | Admin user First Name - Default `Admin` |
| `ADMIN_LAST_NAME` | Admin user First Name - Default `User` |
| `ADMIN_PASS` | Administrator Password - Needed for Logging in | 
| `DB_HOST` | Host or container name of MySQL Server e.g. `freescout-db` |
| `DB_PORT` | MySQL Port - Default `3306` |
| `DB_NAME` | MySQL Database name e.g. `asterisk` |
| `DB_USER` | MySQL Username for above Database e.g. `asterisk` |
| `DB_PASS` | MySQL Password for above Database e.g. `password`|
| `DISPLAY_ERRORS` | Display Errors on Website - Default `FALSE`|
| `ENABLE_SSL_PROXY` | If using SSL reverse proxy force application to return https URLs `TRUE` or `FALSE` |
| `SITE_URL` | The url your site listens on example `https://freescout.example.com`|
| `TIMEZONE` | Timezone - Use Unix Style - Default `America/Vancouver` |

### Networking

The following ports are exposed.

| Port      | Description |
|-----------|-------------|
| `80`      | HTTP        |

# Maintenance

#### Shell Access

For debugging and maintenance purposes you may want access the containers shell. 

```bash
docker exec -it (whatever your container name is e.g. freescout) bash
```

# References

* https://freescout.net/
* https://github.com/freescout-helpdesk/freescout/wiki/Installation-Guide
