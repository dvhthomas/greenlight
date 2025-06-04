# Greenlight

Learning Go API development with [Let's Go Further](https://lets-go-further.alexedwards.net).

## Dependencies

* Go 1.24.3 - `asdf install go 1.24.3`
* Bruno - `npm install @usebruno/cli`

## Development

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
