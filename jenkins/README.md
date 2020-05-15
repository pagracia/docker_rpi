# Jenkins in Raspberry Pi 4

[Jenkins](https://www.jenkins.io/) is an open source automation server. This image runs in Raspberry Pi 4 with linux/arm/v7 architecture (armv7l).

The base image is Ubuntu:18.04.

## Supported tags

- `2.222.3-lts`, `latest`

## Get Started

1. Start the server by running:

```console
$ docker run -d --name jenkins -p 8080:8080 pagracia/rpi-jenkins:latest
```

2. Log in to [http://localhost:8080](http://localhost:8080/) in order to  start configuration.
3. The unlock password can be obtained with:

```console
$ docker logs jenkins
```

## Use volume

It is recommend creating volume for the Jenkins home:

-	`/var/lib/jenkins`: configuration and jobs directories

## Dockerfile

You can see the Dockerfile used to build the image in [GitHub](https://github.com/pagracia/docker_rpi/tree/master/jenkins/2.222.3-lts). Please, if you need other features or see any problem, open an issue in the [repository](https://github.com/pagracia/docker_rpi/issues). Thanks.

## License

View [license information](http://www.gnu.org/licenses/lgpl.txt) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses. As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.

