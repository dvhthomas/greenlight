# Greenlight

Learning Go API development with [Let's Go Further](https://lets-go-further.alexedwards.net).

## Dependencies

* Go 1.24.3 - `asdf install go 1.24.3`
* Bruno - `npm install @usebruno/cli`
* [migrate](https://github.com/golang-migrate/migrate) - `brew install golang-migrate` for database migrations.

## Environment

The server will read environment variables by default from the `.env` file.
Copy the `.env.example` file to `.env` and set the `DB_CONNECTION` variable.

```shell
cp .env.example .env
vim .env # edit the file
source .env # load the variables into the terminal
```

If you want to have those variables also available in the terminal by default, [install and configure `direnv](https://bitsby.me/til/2021-08-31/#now-with-env-support).
That way you can use `$DB_CONNECTION` in your terminal rather than typing `source .env` each time.

## Postgres

Use Docker compatible tool to host this, e.g., [OrbStack](https://orbstack.dev/) on Mac (`brew install orbstack`).

* Postgres - `docker compose up -d`
* Postgres client - `brew install libpq` and add it to the path. `brew` will tell you how to do that for Zsh.

Test the connection:

```shell
psql $DB_CONNECTION
```

If you change the password in the `docker-compose.yml` completely tear down the DB and recreate it otherwise it'll still be in the persistent disk volume.

```shell
cd ~$HOME/location/of/docker-compose.yml
docker compose down --rmi all -v
docker compose up -d
```

### Prep the database

Run any one-time DB setup:

```shell
psql $DB_CONNECTION -f scripts/db-setup.sql
```

Then run any database migrations:

```shell
migrate -path=./migrations -database=$DB_CONNECTION up
```

## Development

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
