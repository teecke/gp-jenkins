FROM teecke/jenkins-dind:2.222.1

# Packages
RUN apk add --no-cache rsync jq libxml2-utils docker-compose

# Jenkins plugin installation
USER jenkins
COPY --chown=jenkins:jenkins plugins.txt /var/jenkins_home/plugins.txt
RUN install-plugins.sh < /var/jenkins_home/plugins.txt
USER root

# Copy backup/cleanup scripts
COPY backup /usr/local/bin/backup
COPY cleanup /usr/local/bin/cleanup

# Entrypoint
COPY start.sh /
ENTRYPOINT ["/start.sh"]

# GP service identification
RUN echo "jenkins" > /gp.service