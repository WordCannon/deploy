<center><img src="https://user-images.githubusercontent.com/1438478/44830275-d41f3980-abd5-11e8-91a4-fa088c197c25.png"></center>


# deploy

Deployment Manifest for WordCannon Stack using docker-compose.

# Prerequisites

## Mac

Install [Docker for Mac](https://download.docker.com/mac/stable/Docker.dmg)

## Linux

```
$ curl -fsSL get.docker.com -o get-docker.sh
$ sh get-docker.sh
```

On Linux, you must also [separately install](https://docs.docker.com/compose/install/) `docker-compose`.  
## Windows

Install [Docker for Windows](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe)

# Configuring

The `docker-stack.yml` file exposes the following environment variables:

## `LANGUAGE`

Which language the words come from.  Default `english`.  See: [list of supported languages](https://github.com/WordCannon/service#supported-languages)

## `NUM_WORDS`

An integer `n` meaning `n most common` words in the dictionary.  Default `10000`

## `VOWEL_TRIGGER_COUNT`

An integer `n` whereby if `n` vowels appear in the word, some special backend behavior is triggered.  We suspect there may be a bug in this area as it appears to lead to crashes.

# Operating

## Environment Setup

1. On the host you want to deploy to (could be your local workstation) initialize Docker Swarm:

```
docker swarm init
```

1. Clone the repo

```
git clone https://github.com/WordCannon/deploy.git
cd deploy
```

## Running the Stack

```
docker stack deploy -c docker-stack.yml wordcannon
```

You should see output like this:

```
Creating network wordcannon_default
Creating service wordcannon_app
Creating service wordcannon_web
```

## Accessing the UI

The the web container binds to port 80 on the host by default.  

Visit [http://localhost](http://localhost)

You can change this by modifying the number `80` in the `80:8080` part of the `docker-stack.yml` file.

## Viewing logs

Backend:

```
docker service logs --follow wordcannon_app
```

Frontend:

```
docker service logs --follow wordcannon_web
```

## Restarting the backend

If the UI starts showing dots `...` instead of words, the backend may need to be restarted due to a bug.  You can also see this in the backend logs  Running the following command will force a redeploy, which will restart the backend container:

```
docker service update --force wordcannon_app
```

## Redeploying

If you make a change to `docker-stack.yml` you can redeploy it using the same command you used to bring up the stack:

```
docker stack deploy -c docker-stack.yml wordcannon
```

This will only redeploy services which had changes to their associated configuration the the yaml.

## Teardown

docker stack rm wordcannon
```

## 
