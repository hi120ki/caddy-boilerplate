# Caddy Boilerplate

## Quick start

### Run a development server

```
$ make dev
```

<http://localhost:8080/>

<http://localhost:8080/nginx/>

<http://localhost:8080/apache/>

### Run a production server (with SSL)

You need to set the hostname (domain) in `env/caddy.env` `caddy/prod/Caddyfile` file and add a record (A or AAAA) to the DNS before starting the container.

```
$ cp env/caddy.env.example env/caddy.env
$ nano env/caddy.env
$ make prod
```

<https://example.com/>

<https://example.com/nginx/>

<https://example.com/apache/>

<https://nginx.example.com/>

<https://apache.example.com/>

## Configuration

<https://caddyserver.com/docs/caddyfile/concepts>

***Be careful not to refer to the v1 documentation***

### environment variable

<https://caddyserver.com/docs/caddyfile/concepts#environment-variables>

```
{$HOST}
```

```
{$HOST:localhost}
```

### virtual host

```
nginx.example.com {
  import default_options
  reverse_proxy http://nginx:80 {
    import proxy_options
  }
}

apache.example.com {
  import default_options
  reverse_proxy http://apache:80 {
    import proxy_options
  }
}
```

### custom header

<https://caddyserver.com/docs/caddyfile/directives/header#header>

- set Strict-Transport-Security all path

```
header Strict-Transport-Security max-age=31536000
```

- set cache exept `/`

```
header   Cache-Control max-age=31536000
header / Cache-Control no-cache
```
