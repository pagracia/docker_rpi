# Build SonarQube image for Raspberry PI 4
FROM ubuntu:18.04

LABEL version="1.0" \
      description="Sonarqube for Raspberry PI, with Ubuntu and OpenJDK." \
      mantainer="Antonio Gracia <pagracia@gmail.com>"

# Versions
ARG SONAR_VERSION=7.9.3
ARG WRAPPER_VERSION=3.5.43

# Add needed software and create sonarqube user
RUN ["/bin/bash", "-c", "set -o pipefail && \
      apt-get update &&  \
      apt-get -y install openjdk-11-jre-headless unzip wget && \
      rm -rf /var/lib/apt/lists/* && \
      cd /opt && \
      wget -O sonarqube.zip https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-$SONAR_VERSION.zip && \
      unzip sonarqube.zip && \
      mv sonarqube-$SONAR_VERSION sonarqube && \
      wget -O - https://download.tanukisoftware.com/wrapper/$WRAPPER_VERSION/wrapper-linux-armhf-32-$WRAPPER_VERSION.tar.gz | tar xzf - && \
      cp -r sonarqube/bin/linux-x86-64 sonarqube/bin/linux-armhf-32 && \
      cp wrapper-linux-armhf-32-$WRAPPER_VERSION/bin/wrapper sonarqube/bin/linux-armhf-32 && \
      cp wrapper-linux-armhf-32-$WRAPPER_VERSION/lib/libwrapper.so sonarqube/bin/linux-armhf-32/lib && \
      rm -f sonarqube/lib/jsw/wrapper-*.jar && \
      cp wrapper-linux-armhf-32-$WRAPPER_VERSION/lib/wrapper.jar sonarqube/lib/jsw/wrapper-$WRAPPER_VERSION.jar && \
      useradd -md /opt/sonarqube -s /bin/bash sonarqube && \
      chown -R sonarqube:sonarqube sonarqube && \
      rm -rf wrapper-linux-armhf-32-$WRAPPER_VERSION \
             sonarqube.zip \
             sonarqube/bin/win* \
             sonarqube/bin/mac* \
             sonarqube/bin/linux-x86*"]

# Get software and prepare
USER sonarqube
WORKDIR /opt/sonarqube

# Port
EXPOSE 9000

# Check health with status
HEALTHCHECK --interval=5m --timeout=5s \
    CMD ["bin/linux-armhf-32/sonar.sh", "status", "|", "grep", "-q", "SonarQube is running"]

# Command sonar.sh console / start
ENTRYPOINT ["bin/linux-armhf-32/sonar.sh"]
CMD ["console"]
