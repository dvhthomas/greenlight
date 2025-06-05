# Greenlight

Learning Go API development with [Let's Go Further](https://lets-go-further.alexedwards.net).

## Dependencies

* Go 1.24.3 - `asdf install go 1.24.3`
* Bruno - `npm install @usebruno/cli`

### Postgres

Use Docker compatible tool to host this, e.g., [OrbStack](https://orbstack.dev/) on Mac (`brew install orbstack`).

* Postgres - `docker-compose up -d`
* Postgres client - `brew install libpq` and add it to the path. `brew` will tell you how to do that for Zsh.

Test the connection:

```shell
psql -h localhost -p 5432 -U greenlight -d greenlight
```

And type the password (see [docker-compose.yml](docker-compose.yml)) when prompted.

If you change the password in the `docker-compose.yml` completely tear down the DB and recreate it otherwise it'll still be in the persistent disk volume.

```shell
cd ~$HOME/location/of/docker-compose.yml
docker compose down --rmi all -v
docker compose up -d
```

## Development

Copy the `.env.example` file to `.env` and set the `DB_CONNECTION` variable.

```shell
cp .env.example .env
```

Run any DB setup:

```shell
psql -h localhost -p 5432 -d greenlight -U greenlight -f migrations/db-setup.sql
```

Run the dev server:

```sh
# start a server
go run ./cmd/api
```

Test the server:

```sh
curl -i http://localhost:4000/healthcheck
```

Or run the [whole suite]():

  ``` sh
  cd bruno
  bru run --env dev
  cd ..
  ```

Bruno [has instructions](https://docs.usebruno.com/bru-cli/commandOptions) on how to run a subset of tests.
