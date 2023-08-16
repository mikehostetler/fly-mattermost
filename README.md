# fly-mattermost

This repo contains a template to run [Mattermost](https://mattermost.com/) on Fly.io.  It is based on the [Mattermost Docker Image](https://hub.docker.com/r/mattermost/mattermost-team-edition) and the [Fly Postgres](https://fly.io/docs/postgres/) service.

## Setup

You will need an available Postgres database to store your config.  You can set one up using the [Fly Postgres](https://fly.io/docs/postgres/).

*Fly Postgres Speedrun*
```
fly pg create
```

## Deploy

To host Mattermost on Fly.io, clone this repo, enter the folder and run:

```
fly launch \
  --copy-config \
  --no-public-ips \
  --no-deploy \
  --ha=false

fly pg attach -a <YOUR_APP> <YOUR_PG_APP>

# Save the $DATABASE_URL from the output of the previous command

fly secrets set \
  MM_SQLSETTINGS_DRIVERNAME=postgres \
  MM_SQLSETTINGS_DATASOURCE=<YOUR_CONNECTION_STRING>

fly deploy
```

## Configuration

Mattermost has a number of configuration options that can be set via environment variables.  You can find a list of them [here](https://docs.mattermost.com/configure/environment-configuration-settings.html).

## Feedback?

https://community.fly.io/ ...TODO

## Wishlist

I'd love to scale this out to a High Availability solution using Mattermost clustering across multiple regions on Fly. If you have any ideas on how to do this, please let me know! PR's welcome!