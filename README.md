
# About

The image generated by this project can be used to run a NodeJS program

For example a backend server, but any other kind of Node.js application (Javascript/Ecmascript) can be run too.

In the folder `/examples`, a node js program shows how to do a simple calculation using environment variables that were set in using docker-compose.

- Uses NodeJS to execute a javascript file located at one of the following 
  locations:

   /mnt/nodejs/index.js
   /mnt/nodejs/index.mjs
   /mnt/nodejs/index.cjs
   /mnt/nodejs/dist/index.js
   /mnt/nodejs/dist/index.mjs
   /mnt/nodejs/dist/index.cjs

   (when using the default ROOT_FOLDER=/mnt/nodejs)

- Executes the NodeJs program not as root, but as normal user `nodejs`

# Usage

## Just try it out (using docker-compose)

See also the folder `/examples`.

Below an example of using the image in a docker-compose file

```yaml
version: "3.9"

services:
  nodejs:
    image: hkdigital/nodejs     # docker-hub
    # image: hkdigital-nodejs     # local    

    restart: on-failure # "no"|always|on-failure|unless-stopped

    environment:
      - WATCH=1                                   # 1 use `nodemon` not `node`
      - HEAP_SIZE_MB=1024                         # NodeJs --max-old-space-size
      - PARAMS=--radius=1 --calculation=surface   # NodeJs parameters
      - NODE_ENV=production

    volumes:
      - ./volumes/some-calculation:/mnt/nodejs
```

# Build locally

If you just want to use the image to create a container, there is no need to build the image locally. You can use the image from docker-hub.

Building the image locally is usually done for development of the image itself.

## Get a working copy from the repository

Clone the latest commit from github into a local working directory.

```bash
git clone --depth 1 \
  git@github.com:hkdigital/docker-image--nodejs.git \
  hkdigital-nodejs
```

## Build the docker image

```bash
./build-latest-image.sh
docker image ls
# Shows hkdigital-nodejs
```
