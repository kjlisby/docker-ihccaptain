# docker-ihccaptain
Dockerfile for IHC Captain

See 
* https://docs.docker.com/guides/docker-concepts/the-basics/what-is-a-container/
* https://raspberrytips.com/docker-on-raspberry-pi/
* https://www.instructables.com/Build-Docker-Image-for-Raspberry-Pi/
* https://hub.docker.com/r/arberg/ihccaptain/
* https://www.ihc-user.dk/forum/forums/topic/7151-ihc-captain-p%C3%A5-linux-milj%C3%B8docker/
* http://jemi.dk/ihc/
* Current version: http://jemi.dk/ihc/#changelog

## Running docker-ihccaptain

Note that it may be necessary to change the default port to an unused port on your host system. see run.sh

The contents of this repository is only used for building and uploading the container to DockerHub. See https://hub.docker.com/search?q=ihccaptain

The author (https://github.com/arberg) seem to be updating on DockerHub pretty often. So this repository is only needed when you want to modify something in the container, or if you for other reasons want to rebuild the image yourself.

Those who only want to use the image, should only have to:
1. Install Docker on your Raspberry Pi (see the guides above)
2. Download the ihccaptain image from DockerHub
*           docker pull arberg/ihccaptain
3. Run the image as a daemon:
*           use the run.sh script
*       or
*           docker run -d --name IHCCaptain -p 8100:80 -p 9100:443 -v ./ihccaptain/data:/opt/ihccaptain/data/ -v ./ihccaptain/host:/host/ -v "/etc/localtime:/etc/localtime:ro" arberg/ihccaptain:latest

See also https://hub.docker.com/r/arberg/ihccaptain

## How To build docker image again

* Manually update file VERSION
* run build.sh or just release.sh
* or `./build.sh; ./run.sh` to build at run the build

## How To debug build-process if it fails

Probably its the install.sh that wil be failing. Download (install script)[http://jemi.dk/ihc/files/install] to host/custom_installer/installer.sh, and edit Dockerfile so it uses the downloaded version. See the ADD line. Now we can edit the build-script locally and run build.sh to build it.

If IHC-captain docker fails to start, start a bash inside a container with `run_debug.sh <optional image>`.

Alternatively edit the Dockerfile so it stops at where it fails, and run the container with interactive bash. Search for `how to debug Dockerfile` to learn more, ie. https://www.joyfulbikeshedding.com/blog/2019-08-27-debugging-docker-builds.html
