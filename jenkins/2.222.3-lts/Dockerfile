# Build Jenkins image for Raspberry PI 4
FROM ubuntu:18.04

LABEL version="1.0" \
      description="Jenkins for Raspberry PI, with Ubuntu and OpenJDK." \
      mantainer="Antonio Gracia <pagracia@gmail.com>"

# Versions
ARG JENKINS_VERSION=2.222.3

# Add needed software and create sonarqube user
RUN ["/bin/bash", "-c", "set -o pipefail && \
      apt-get update &&  \
      apt-get -y install openjdk-8-jre-headless wget && \
      wget -O jenkins.deb https://pkg.jenkins.io/debian-stable/binary/jenkins_${JENKINS_VERSION}_all.deb && \
      apt install -y ./jenkins.deb && \
      rm -rf /var/lib/apt/lists/* jenkins.deb"]
	  
# Ports
EXPOSE 8080/tcp
EXPOSE 50000/tcp

# Jenkins Environment
ENV JENKINS_HOME=/var/lib/jenkins
ENV JAVA_ARGS="-Djava.awt.headless=true"

USER jenkins

ENTRYPOINT java $JAVA_ARGS -jar /usr/share/jenkins/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
