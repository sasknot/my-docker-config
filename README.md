# My Docker Config


## Requirements

- [Docker](https://www.docker.com)

## Running

1. Choose the config you want copy it to the root of your project
2. Run `docker build -t myconfig .`
3. Run `docker run -p 80:80 myconfig`

### Node

- Node 14.5.0
- sudo

### PHP with Apache

- Apache 2 (with rewrite, headers, setenvif)
- PHP 7.0 (with mysqli, pdo, pdo_mysql, intl, memcached, mcrypt)
- libmcrypt-dev
- libicu-dev
- libmemcached-dev zlib1g-dev
- vim

### Ruby

- Ruby 2.1
- libpq-dev
- nodejs
- Copies local gems at /gems (if you have)