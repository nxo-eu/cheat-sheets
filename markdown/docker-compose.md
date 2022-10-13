```yml
title: docker-compose
category: Devops
layout: 2022/sheet
prism_languages: [yaml]
weight: -1
updated: 11-Oct-2022
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Docker Compose](#DockerCompose)
	* 1.1. [Basic example](#Basicexample)
	* 1.2. [Commands](#Commands)
	* 1.3. [Building](#Building)
	* 1.4. [Ports](#Ports)
	* 1.5. [Commands](#Commands-1)
	* 1.6. [Environment variables](#Environmentvariables)
	* 1.7. [Dependencies](#Dependencies)
	* 1.8. [Other options](#Otheroptions)
* 2. [Advanced features](#Advancedfeatures)
	* 2.1. [Labels](#Labels)
	* 2.2. [DNS servers](#DNSservers)
	* 2.3. [Devices](#Devices)
	* 2.4. [External links](#Externallinks)
	* 2.5. [Hosts](#Hosts)
	* 2.6. [Network](#Network)
	* 2.7. [External network](#Externalnetwork)
	* 2.8. [Volume](#Volume)
	* 2.9. [User](#User)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

##  1. <a name='DockerCompose'></a>Docker Compose


###  1.1. <a name='Basicexample'></a>Basic example

```yaml
# docker-compose.yml
version: '2'

services:
  web:
    build:
    # build from Dockerfile
      context: ./Path
      dockerfile: Dockerfile
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: redis
```

###  1.2. <a name='Commands'></a>Commands

```sh
docker compose start
docker compose stop
```

```sh
docker compose pause
docker compose unpause
```

```sh
docker compose ps
docker compose up
docker compose down
```

```sh
# other cli commands are similar to docker ones, like
docker compose build
docker compose logs -f
```

###  1.3. <a name='Building'></a>Building

```yaml
web:
  # build from Dockerfile
  build: .
  args:     # Add build arguments
    APP_HOME: app
```

```yaml
  # build from custom Dockerfile
  build:
    context: ./dir
    dockerfile: Dockerfile.dev
```

```yaml
  # build from image
  image: ubuntu
  image: ubuntu:20.04
  image: nginx:latest
  image: tutum/influxdb
  image: example-registry:4000/postgresql
  image: a4bc65fd
```

###  1.4. <a name='Ports'></a>Ports

```yaml
  ports:
    - "3000"
    - "8000:80"  # host:container
```

```yaml
  # expose ports to linked services (not to host)
  expose: ["3000"]
```

###  1.5. <a name='Commands-1'></a>Commands

```yaml
  # command to execute
  command: bundle exec thin -p 3000
  command: [bundle, exec, thin, -p, 3000]
```

```yaml
  # override the entrypoint
  entrypoint: /app/start.sh
  entrypoint: [php, -d, vendor/bin/phpunit]
```

###  1.6. <a name='Environmentvariables'></a>Environment variables

```yaml
  # environment vars
  environment:
    RACK_ENV: development
  environment:
    - RACK_ENV=development
```

```yaml
  # environment vars from file
  env_file: .env
  env_file: [.env, .development.env]
```

###  1.7. <a name='Dependencies'></a>Dependencies

```yaml
  # makes the `db` service available as the hostname `database`
  # (implies depends_on)
  links:
    - db:database
    - redis
```

```yaml
  # make sure `db` is alive before starting
  depends_on:
    - db
```

###  1.8. <a name='Otheroptions'></a>Other options

```yaml
  # make this service extend another
  extends:
    file: common.yml  # optional
    service: webapp
```

```yaml
  volumes:
    - /var/lib/mysql
    - ./_data:/var/lib/mysql
```

```yaml
  # automatically restart container
  restart: unless-stopped
  # always, on-failure, no (default)
```

##  2. <a name='Advancedfeatures'></a>Advanced features

###  2.1. <a name='Labels'></a>Labels

```yaml
services:
  web:
    labels:
      com.example.description: "Accounting web app"
```

###  2.2. <a name='DNSservers'></a>DNS servers

```yaml
services:
  web:
    dns: 8.8.8.8
    dns:
      - 8.8.8.8
      - 8.8.4.4
```

###  2.3. <a name='Devices'></a>Devices

```yaml
services:
  web:
    devices:
    - "/dev/ttyUSB0:/dev/ttyUSB0"
```

###  2.4. <a name='Externallinks'></a>External links

```yaml
services:
  web:
    external_links:
      - redis_1
      - project_db_1:mysql
```

###  2.5. <a name='Hosts'></a>Hosts

```yaml
services:
  web:
    extra_hosts:
      - "somehost:192.168.1.100"
```

###  2.6. <a name='Network'></a>Network

```yaml
# creates a custom network called `frontend`
networks:
  frontend:
```

###  2.7. <a name='Externalnetwork'></a>External network

```yaml
# join a pre-existing network
networks:
  default:
    external:
      name: frontend
```

###  2.8. <a name='Volume'></a>Volume

```yaml
# mount host paths or named volumes, specified as sub-options to a service
  db:
    image: postgres:latest
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"

volumes:
  dbdata:
```

###  2.9. <a name='User'></a>User

```yaml
# specifying user
user: root
```

```yaml
# specifying both user and group with ids
user: 0:0
```