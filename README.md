# Dockerize Magento 2

A composer package for dockerizing Magento 2

The composer package **arvatoscm/dockerize-magento2** deploys docker infrastructure defintion files such as [docker-compose.yml](docker-compose.yml) to your Magento 2 root folder and enables you to host your Magento 2 shops without having to install Apache/Nginx, MySQL or PHP on your system.

## Package Name

`arvatoscm/dockerize-magento2`

## Software Requirements

For Linux users you must have a recent version of [docker](https://github.com/docker/docker/releases) and [docker-compose](https://github.com/docker/compose/releases) installed.

If you are a Mac or Windows user, use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox).

## Installation

Add `arvatoscm/dockerize-magento2` to your existing Magento 2 shop:

```bash
composer require --ignore-platform-reqs arvatoscm/dockerize-magento2
chmod +x bin/console
```

This will place some files in your Magento root:

- `docker-compose.yml`
The docker infrastructure definition
- `bin/console`
A utility script for controlling dockerized Magento projects
- `config`
A folder which contains the configuration files for PHP, Nginx and phpMyAdmin


## Usage

`dockerize-magento2` comes with `bin/console` script that can be used to install Magento and to execute Magentos' bin/magento script inside the PHP docker container:

Trigger the Magento 2 installation process:

```bash
bin/console install <hostname>
```

Initialize a 121ecommerce Magento 2 project:

```bash
bin/console init <hostname> [crypt]
```

Import an Magento 2 existing project:

```bash
bin/console import <hostname> [crypt]
```

Start the docker containers:

```bash
bin/console start
```

Stop the docker containers:

```bash
bin/console stop
```

Execute `bin/magento` inside the docker container:

```bash
bin/console exec [arguments]
```

For more information on how to use docker-compose visit: https://docs.docker.com/compose/

## Configuration

The `install` action depends on some parameters such as usernames and passwords. We have put in some default values for you that will work for a quick test:

```
DATABASE_NAME="magento2dockerized"
DATABASE_USER="magento"
DATABASE_PASSWORD="enAVINa2"
DATABASE_ROOT_PASSWORD="enAVINa2"

ADMIN_USERNAME="admin"
ADMIN_FIRSTNAME="Admin"
ADMIN_LASTNAME="Inistrator"
ADMIN_EMAIL="johndoe@example.com"
ADMIN_PASSWORD="enAVINa2"

DEFAULT_LANGUAGE="en_US"
DEFAULT_CURRENCY="EUR"
DEFAULT_TIMEZONE="Europe/Berlin"

BACKEND_FRONTNAME="management"
```

If you want to use different parameters change the values in the [.env](.env) file to your needs.
After customizing the parameters just run trigger the installation with `bin/console install <hostname>`.

## Initialize 121eCommerce Project

The `init` action gives you the ability to set up a 121eCommerce's existing project. You only need to specify the proper parameters within the file `.env`.
This an example of the required parameters:

```
DATABASE_NAME=weld
DATABASE_USER=weld
DATABASE_PASSWORD=1213c0mm3rc3!
DATABASE_ROOT_PASSWORD=root

ADMIN_USERNAME=admin
ADMIN_FIRSTNAME=Admin
ADMIN_LASTNAME=121
ADMIN_EMAIL=johndoe@example.com
ADMIN_PASSWORD=121ecommerce

SSH_HOST=dev121.magemojo.com
SSH_USER=weld
SSH_PRIVATE_KEY_FILE=config/private_key.txt

GITHUB_REPO=https://github.com/121eCommerceLLC/weld.git
GITHUB_FORK=https://github.com/fsspencer/weld.git

DEFAULT_LANGUAGE=en_US
DEFAULT_CURRENCY=USD
DEFAULT_TIMEZONE=America/New_York

BACKEND_FRONTNAME=backend
```

Once you fill up tne `env.php`with your project parameters, execute the following command:

```bash
bin/console init <hostname> [crypt]
```

This will detect if your Magento project is an Enterprise or Community version and download an env.php template and fill it up automatically.

The `crypt` parameter is optional but we recommend to provide it based on the original env.php file.

## Import

The `import` action gives you the ability to set up your existing project. You only need to place you database sql file(s) into `config/mysql/` and provide the following parameters.

```bash
bin/console import <hostname> [crypt]
```

This will detect if your Magento project is an Enterprise or Community version and download an env.php template and fill it up automatically.

The `crypt` parameter is optional but we recommend to provide it based on the original env.php file.

## Licensing

dockerize-magento2 is licensed under the Apache License, Version 2.0.
See [LICENSE](LICENSE) for the full license text.
