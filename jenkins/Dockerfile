FROM teecke/jenkins-dind:2.204.2

# Packages
RUN apk add --no-cache rsync openjdk8 jq libxml2-utils docker-compose

# Jenkins plugin installation
USER jenkins
COPY --chown=jenkins:jenkins plugins.txt /var/jenkins_home/plugins.txt
RUN install-plugins.sh < /var/jenkins_home/plugins.txt

# Aditional tools installation
USER root
RUN wget https://raw.githubusercontent.com/kairops/docker-command-launcher/master/kd.sh -O /usr/sbin/kd -q && \
    chmod +x /usr/sbin/kd && \
    curl https://raw.githubusercontent.com/teecke/devcontrol/master/install.sh | bash

# Copy backup/cleanup scripts
COPY backup /usr/local/bin/backup
COPY cleanup /usr/local/bin/cleanup

# GP service identification
RUN echo "jenkins" > /gp.service