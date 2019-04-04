FROM jenkins/jenkins:lts
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

USER root

RUN apt-get update && \
apt-get -y install apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common

RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-17.04.0-ce.tgz \
  && tar xzvf docker-17.04.0-ce.tgz \
  && mv docker/docker /usr/local/bin \
  && rm -r docker docker-17.04.0-ce.tgz

RUN groupadd docker
RUN usermod -a -G docker root

COPY ./plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh  < /usr/share/jenkins/ref/plugins.txt
ENV HOME $JENKINS_HOME

USER root

