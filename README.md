# PINK-UNICORN

## Environment

- OS: Windows 10 Version 1903 (OS Build 18362.657)
- Docker Desktop for Windows 2.2.0.4 (stable)
- Docker Engine 19.03.8
- Compose 1.25.4

## Project structure

Project has been divided into two parts:
- Dockerized applications for TIY model
- Dockerized applications for JustGo model

## Deployment

Example applications (Alpha, Beta, Gamma), dockerfiles and docker-compose files have been uploaded to a public GIT repository. For testing purposes you can clone this GIT repository to a dockerized environment:

```ps
git clone https://github.com/zapolskas/pink-unicorn.git
```

Each individual container can be created manually, by opening directory (e.g. .\pink-unicorn\JustGo\alpha1) which contains a dockerfile and building an image:

```ps
docker build . -t alpha1:1.0.0
```

Once image is ready you can run a container:

```ps
docker run -d alpha1:1.0.0 --name alpha1
```

Container can be checked by:

```ps
docker logs alpha1
```

For containers (i.e. Alpha2, Beta, Gamma1, Gamma2) which service is accessible through a webbrowser:

```ps
docker build -t alpha2:1.0.0 .
docker run -d -p 5000:80 --name alpha2 alpha2:1.0.0
```

And checked by accessing configured port on a local machine via webbrowser, e.g.:

<http://localhost:5000>

## Deployment packages

There are two deployment packages, one for each bike model. Containers are defined in a docker-compose file. Package can be deployed by running:

```ps
docker-compose up -d --build
```

--build argument makes sure that the containers are rebuilt everytime. However, sometimes cache related issues can occur, in that case images can be built prior to running docker-compose:

```ps
docker-compose build --no-cache
```

## Updating

There are two scenarios how containers can be updated:

- When a system has internet connection
- When a system is offline, but has access to external media, e.g. USB drive.

When a dockerized system has internet connection, everything becomes so simple. Just update code in the GIT repository and dockerfile will make sure to use those updated files to create a new version of container. This has been achieved by running git checkout during image building process:

```ps
RUN git init && \
    git remote add origin https://github.com/zapolskas/pink-unicorn.git && \
    git fetch origin && \
    git checkout origin/master -- JustGo/Gamma1/src
```

In scenarios where dockerized environment has no internet access (air-gapped environment), docker images should be built where there is an internet access or at least application source code, all required apt packages(cmake, git, etc.) and all the prerequisite docker images are available, i.e. ubuntu:bionic, mcr.microsoft.com/dotnet/core/sdk:3.1, etc.

Image can be built:

```ps
docker build -t gamma1:1.0.0 .
```

Image can be saved to a .tar file and moved to external media:

```ps
docker save 76202d1c7bb2 -o gamma1.tar
```

When .tar file is available in an air-gapped environment it can be loaded:

```ps
docker load -i gamma1.tar
```

Finally an old container should be stoped and new one run:

```ps
docker run -d -p 6001:80 --name gamma1 gamma1:1.0.0
```
