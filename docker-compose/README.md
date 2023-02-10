# Docker-compose configuration

Runs Blockscout locally in Docker containers with [docker-compose](https://github.com/docker/compose).

## Prerequisites
- Docker v20.10+
- Docker-compose 2.x.x+
- Running Ethereum JSON RPC client

## Building Docker containers from source
```
docker-compose up --build
```

This command uses by-default `docker-compose.yml`, which build the explorer into Docker image and runs 2 Docker containers:
- one for the database. Postgres 13.x, which will be available at port 7432 on localhost
- and the BlockScout explorer at http://localhost:4000

## Configs for different Ethereum clients

The repo contains built-in configs for different clients without needing to build the image.

- Erigon: `docker-compose -f docker-compose-no-build-erigon.yml up -d`
- Geth: `docker-compose -f docker-compose-no-build-geth.yml up -d`
- Nethermind, OpenEthereum: `docker-compose -f docker-compose-no-build-nethermind up -d`
- Ganache: `docker-compose -f docker-compose-no-build-ganache.yml up -d`
- HardHat network: `docker-compose -f docker-compose-no-build-hardhat-network.yml up -d`
- Running explorer only without DB: `docker-compose -f docker-compose-no-build-no-db-container.yml up -d`. In this case, one container is created - for the explorer itself. It assumes DB credentials are provided through the `DATABASE_URL` environment variable.

All of the configs assume the Ethereum JSON RPC is running at http://localhost:8545.

In order to stop launched containers, run `docker-compose -d -f config_file.yml down`, replacing `config_file.yml` with the file name of the config which was previously launched.

You can adjust BlockScout environment variables from `./envs/common-blockscout.env`. Descriptions of the ENVs are available in [the docs](https://docs.blockscout.com/for-developers/information-and-settings/env-variables).
