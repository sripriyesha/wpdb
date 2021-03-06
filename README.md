# wpdb

Tools for Handling WordPress Database by Docker and WP-CLI.

[![NPM](https://nodei.co/npm/wpdb.png)](https://nodei.co/npm/wpdb/)
[![Build Status](https://travis-ci.org/isaxxx/wpdb.svg?branch=master)](https://travis-ci.org/isaxxx/wpdb)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

## Installation

### NPM

You must install [Docker](https://www.docker.com/) for this module to work.

```bash
$ npm install wpdb --save
```

## Usage

### CLI

```
Options:
  --version, -v   show this version. [boolean]
  --help, -h      show this help. [boolean]
```

#### Initialize

Install the Docker files.

```bash
$ wpdb
```

#### Start

Start Docker.

```bash
$ docker-compose build
$ docker-compose up -d
```

#### Stop

Stop Docker.

```bash
$ docker-compose down -v
```

#### Restart

Restart Docker (When fixed php.ini etc.).

```bash
$ docker-compose restart
```

#### Reset

Reset Database.

```bash
$ docker-compose exec wordpress wp db reset --allow-root
```

#### Import

Import the SQL file.

```bash
$ docker-compose exec wordpress wp db import /var/lib/mysql/import.sql --allow-root
```

#### Export

Export the SQL file.

```bash
$ docker-compose exec wordpress wp db export /var/lib/mysql/export.sql --allow-root
```

#### Replace

##### Import

```bash
$ docker-compose exec wordpress wp db import /var/lib/mysql/import.sql --allow-root
$ docker-compose exec wordpress wp search-replace http://example.com http://localhost --allow-root
```

##### Export

```bash
$ docker-compose exec wordpress wp db export /var/lib/mysql/export.sql --allow-root
```

###### Upload

```bash
$ docker-compose exec wordpress wp search-replace http://localhost http://example.com --allow-root
$ docker-compose exec wordpress wp db export /var/lib/mysql/upload.sql --allow-root
$ docker-compose exec wordpress wp search-replace http://example.com http://localhost --allow-root
```

```bash
$ docker-compose exec wordpress wp search-replace http://localhost http://example.com --export=/var/lib/mysql/upload.sql --allow-root
```

##### ACF Block

```bash
$ docker-compose exec wordpress wp search-replace 'http:\/\/example.com' 'http:\/\/localhost' --allow-root
```

##### Change PHP Version

Please change the first line of `/docker/wordpress/Dockerfile`.

```
# Default
FROM wordpress:latest

# PHP 7.0
FROM wordpress:php7.0-apache
```

Please refer to the link below for usable containers.

[WordPress Docker Official Images](https://hub.docker.com/_/wordpress/)

##### Docker Logs

```bash
$ docker-compose logs | grep wordpress
```

##### Bash

```bash
$ docker-compose exec wordpress /bin/bash
```

##### Composer

```bash
$ docker-compose exec wordpress composer -v
```

##### PHP CodeSniffer

```bash
$ docker-compose exec wordpress ./vendor/bin/phpcs --standard=PSR2 ./wp-content/themes/my-theme/
```

##### PHP CS Fixer

```bash
$ docker-compose exec wordpress ./vendor/bin/php-cs-fixer fix --dry-run --diff --diff-format udiff ./wp-content/themes/my-theme/
$ docker-compose exec wordpress ./vendor/bin/php-cs-fixer fix ./wp-content/themes/my-theme/
```

### Use SSL

#### Rename docker-comopse-ssl.yml and WordPress Docker file

```bash
$ cp ./docker-comopse-ssl.yml ./docker-compose.yml
$ cp ./docker/wordpress/Dockerfile-ssl ./docker/wordpress/Dockerfile
```

#### Install mkcert

```bash
$ brew install mkcert
$ brew install nss
$ mkcert -install
```

#### make SSL Certificate

```bash
$ cd ./docker/certs/
$ mkcert localhost 127.0.0.1
$ ls
---
localhost+1-key.pem
localhost+1.pem
```

#### Docker Build & Start

```bash
$ docker-compose build
$ docker-compose up -d
```

Access SSL URL !!!

### JavaScript

```js
wpdb().then(() => {
  console.log('Complete!!');
});
```

### Access

* WordPress

[http://localhost](http://localhost)

* WordPress（SSL）

[https://localhost](https://localhost)

Please Edit Hosts File. Then you will be able to access it with the URL you want.

```bash
$ sudo vi /etc/hosts
---
127.0.0.1       example.com
```

* phpMyAdmin

[http://localhost:8080/](http://localhost:8080/)

* MailHog

[http://localhost:8025/](http://localhost:8025/)

## [Changelog](CHANGELOG.md)

## [License](LICENSE)
