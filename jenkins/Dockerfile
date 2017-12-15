FROM jenkins/jenkins:lts
USER root
COPY docker-engine.key /tmp/docker-engine.key
RUN apt-get update && echo "deb https://apt.dockerproject.org/repo debian-stretch main" > /etc/apt/sources.list.d/docker.list \
    && apt-get install apt-transport-https && apt-key add /tmp/docker-engine.key && apt-get update && apt-get install -y docker-engine
RUN usermod -aG docker jenkins 

USER jenkins
