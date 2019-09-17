# Grandus Docker

Experimental repository for running Grandus 3 inside Docker containers

## Prerequisites
1. Install [Docker Desktop](https://docs.docker.com/install/) based on your OS
2. Install [Docker Compose](https://docs.docker.com/compose/install/) if it is not part of Docker Desktop App. On desktop systems like Docker Desktop for Mac and Windows, Docker Compose is included as part of those desktop installs. You can verify it by running following command in your command line:

```bash
docker-compose version
```

## Setup
1. Clone repository you want to work with to `./src` folder
2. Create `.env` file
```bash
cp .env-example .env
```

## Usage

### Build and start
**Build and start** docker containers using `docker-compose up -d` or just **start** docker containers by `docker-compose start -d` command if containers have already been built

To **stop** containers use `docker-compose stop` command or `docker-compose down`
to **stop and remove** containers (won't remove database and elasticsearch data)

### Connect to container
To run composer and php commands, you have to connect to php container using following command:

```bash
bash -c "clear && docker exec -it php sh"
```

### Install Grandus dependencies
After connecting to container you can run commands like in your ordinary terminal.

### Grandus
To access Grandus, open [http://0.0.0.0](http://0.0.0.0:80) in your browser. You can set different domain name by adding following to your `etc/hosts`

```bash
0.0.0.0    grandus.docker
```


## Settings
All docker containers are within one virtual network and are accessible under following names:

|     Service   |      Host     | Port |
|---------------|:-------------:|-----:|
| Maria DB      | mariadb       | 3306 |
| Elasticsearch | elasticsearch | 9000 |
| Kibana        | kibana        | 5601 |

> **Note:** This **hosts** and **ports** should be used to connect Grandus to database or elasticsearch. If you want to access Maria DB or Kibana from your host, use `localhost:port`