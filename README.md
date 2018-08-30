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

# Usage

1. Clone the repo

```
git clone https://github.com/WordCannon/deploy.git
cd deploy
```

2. Run the stack

As a foreground process:

```
docker-compose up
```

As a background process:

```
docker-compose up -d
```

3. Tear down

If running in the foreground:

```
CTRL-C
```

If running in the background:

```
docker-compose down
```

3. Accessing the UI

The the web container binds to port 80 on the host by default.  

Visit [http://localhost](http://localhost)

You can change this by modifying the number `80` in the `80:8080` part of the `docker-compose.yml` file.
