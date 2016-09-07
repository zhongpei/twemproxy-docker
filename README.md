# Twemproxy for Tarantool

This is a Docker image with a custom build of Twemproxy, implementing Tarantool protocol.

## Usage

Create a `nutcracker.yml` file with the following content:

``` yaml
alpha:
  listen: 127.0.0.1:3301
  hash: fnv1a_64
  distribution: ketama
  auto_eject_hosts: true
  protocol: tarantool
  server_retry_timeout: 2000
  server_failure_limit: 1
  servers:
   - tarantool1:3301:1
   - tarantool2:3301:1
   - tarantool3:3301:1
```

Then create a custom `Dockerfile`:

``` yaml
FROM tarantool/twemproxy

COPY nutcracker.yml /etc/
```

Build new image:

``` bash
docker build -t my-twemproxy-image .
```

And run it:

``` bash
docker run -d --name twemproxy my-twemproxy-image
```
