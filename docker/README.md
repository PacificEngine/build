![GitHub release (latest by date)](https://img.shields.io/github/v/release/PacificEngine/gradle-plugins?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/PacificEngine/gradle-plugins?label=last%20release&style=flat-square)

# How To Utilize Plugins

The Purpose of this plugin is to more easily bundle docker required packages into a docker image

This plugin will also copy anything from the `src/docker` folder into location

The docker dependencies will be built to `build/docker`

## Usage

Using the `toCopy` in your dependencies will automatically copy the dependencies to the docker java library location

__Gradle File__
```groovy
plugins {
    id 'io.github.pacificengine.build.docker' version "0.1.0"
}

dependencies {
    toCopy project(':instance')
}
```

__DockerFile__
```Dockerfile
FROM debian:bullseye-slim

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		openjdk-17-jre \
    && rm -rf /var/cache/apt/* \
    && rm -rf /var/lib/apt/lists/*

ENV USER_NAME=docker USER_GROUP=docker
RUN addgroup --system $USER_NAME && adduser --system $USER_NAME --ingroup $USER_GROUP
USER root:root

ENV GRADLE_VERSION
COPY build/docker /

RUN chown -R docker:docker /app
USER docker:docker
WORKDIR "/app"

ENTRYPOINT ["java","-jar","/app/app-${GRADLE_VERSION}.jar"]
```

## Properties
### Optional Properties
* `project.archive.docker.source` The location of files to be moved to the docker image (Defaults to `src/docker`)
* `project.archive.docker.build` The location of files to be uploaded to the docker image (Default to `build/docker`)
* `project.archive.docker.app` The location on the docker image to put the java libraries (Defaults to `app/lib`)