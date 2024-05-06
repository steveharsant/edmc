# Emby Dynamic Collections Manager

EDCM - A Companion Tool For Emby To Manage Emby Collections Based On User Specified Rules

## Overview

EDCM is a small Python app that reads a config file containing rules for collections, searches for media that satisfies those rules, and creates/updates the collection with the results. This allows users to create more specific collections.

## Installation

First, generate an API token following the [official documentation](https://dev.emby.media/doc/restapi/API-Key-Authentication.html).

Next, follow your preferred installation method:

### Option 1: Docker (Recommended)

Run the command after replacing values within `<< >>`:

> ***Note:** For all options see Options section below*

```bash
docker run -d \
  --name=edcm \
  -e EMBY_ADDRESS=<<emby-ip-address-here>> \
  -e EMBY_TOKEN=<<your-emby-api-token-here>> \
  -v <</path/to/config/dir>>:/config \
  --restart unless-stopped \
  ghcr.io/steveharsant/edcm:latest
```

Or, for Docker Compose:

```yaml
services:
  edcm:
    container_name: edcm
    image: ghcr.io/steveharsant/edcm:latest
    environment:
      - EMBY_ADDRESS=<<emby-ip-address-here>>
      - EMBY_TOKEN=<<your-emby-api-token-here>>
    volumes:
      - <</path/to/config/dir>>:/config
    restart: unless-stopped
```

### Option 2: Direct

1. Clone this repository
2. `cd` to the `src` subdirectory
3. Run `pip install -r requirements.txt`
4. Run `python app.py`

## Options

The following environment variables provide configuration to EDCM:

| Name                           | Default Value        | Required |
|--------------------------------|----------------------|----------|
| `EDCM_CONFIG_PATH`             | `/config/config.ini` | `False`  |
| `EMBY_ADDRESS`                 | `N/A`                | `True`   |
| `EMBY_PORT`                    | `8096`               | `False`  |
| `EMBY_TOKEN`                   | `N/A`                | `True`   |
| `EDCM_SCAN_INTERVAL` (seconds) | `600`                | `False`  |
| `EDCM_USE_SSL`                 | `False`              | `False`  |
