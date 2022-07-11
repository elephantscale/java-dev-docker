# Java Development Enviroment in Docker

Configured from [maven:3-jdk-11](https://hub.docker.com/_/maven)

Added a [maven settings.xml](config/settings.xml) so we can reuse downloaded artifacts from host and docker container.

Find it at Dockerhub [elephantscale/java-dev](https://hub.docker.com/r/elephantscale/java-dev)

## Quick start

Run it by running this script: [start-java-dev.sh](start-java-dev.sh)

A few notes:

* We run the container as `CURRENT_USER`.  This makes sure that all artifacts created have proper permissions by current user.
* Also we mount `$HOME/.m2` directory into `/var/maven/.m2` directory in container.  This allows maven to reuse downloaded artifacts.  This will hugely speed up compiles
* The current directory is mounted as `/workspace` within container

```bash
$   ./start-java-dev.sh
```

Within the container: 

```bash
# you will be in /workspace directory
# all your files will be here
$   cd to/your/project
$   mvn clean package
```

## Building the Image (Devs Only)

```bash
$   docker build .  -t elephantscale/java-dev
$   docker build .  -t elephantscale/java-dev:1.0
```

Publishing to dockerhub

```bash
$   docker login
$   docker push  elephantscale/java-dev
$   docker push  elephantscale/java-dev:1.0
```
