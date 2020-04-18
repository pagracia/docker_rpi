# SonarQube in Raspberry Pi 4

[SonarQube](https://www.sonarqube.org/) is an open source product for continuous inspection of code quality. This image runs in Raspberry Pi 4 with linux/arm/v7 architecture (armv7l).

The base image is Ubuntu:18.04.

## Supported tags

- `7.9.3 -lts`, `latest`

## Get Started

1. Start the server by running:

```console
$ docker run -d --name sonarqube -p 9000:9000 <image_name>
```

2. Log in to [http://localhost:9000](http://localhost:9000/) with System Administrator credentials (login=admin, password=admin).

3. Click the **Create new project** button to analyze your first project.

## Docker Host Requirement

Because SonarQube uses an embedded Elasticsearch, make sure that your operating system configuration has the recommended value for `vm.max_map_count` (262144). Specially, this is needed when configure another database different to H2.

For example, you can set the recommended value for the current session by running the following command on the host:

```console
$ sudo sysctl -w vm.max_map_count=262144
```

## Configuration

### Database

By default, the image will use an embedded H2 database that is not suited for production.

> **Note**: Set up a different database by following the "Database Installation" section of [Install the Server](https://docs.sonarqube.org/latest/setup/install-server/)

### Use volumes

It is recommend creating volumes for the following directories:

-	`/opt/sonarqube/conf`: configuration files, such as `sonar.properties`.
-	`/opt/sonarqube/data`: data files, such as the embedded H2 database and Elasticsearch indexes
-	`/opt/sonarqube/logs`: contains SonarQube logs about access, web process, CE process, Elasticsearch logs
-	`/opt/sonarqube/extensions`: plugins, such as language analyzers

## Dockerfile

You can see the Dockerfile used to build the image in [GitHub](https://github.com/pagracia/docker_rpi/tree/master/sonarqube/7.9.3-community). Please, if you need other features or see any problem, open an issue in the [repository](https://github.com/pagracia/docker_rpi/issues). Thanks.

## License

View [license information](http://www.gnu.org/licenses/lgpl.txt) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses. As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.

