FROM jenkins/jenkins:lts
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
RUN install-plugins.sh slack conditional-buildstep parameterized-trigger
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

USER root
RUN apt-get update && apt-get install -y python3 python3-venv python3-pip python3-numpy python3-pandas
RUN apt-get install -y jq python3-click
RUN apt-get install -y virtualenv

# drop back to the regular jenkins user - good practice
USER jenkins

COPY --chown=jenkins:jenkins jenkins_home/jobs /var/jenkins_home/jobs
COPY --chown=jenkins:jenkins jenkins_home/hudson.plugins.git.GitTool.xml /var/jenkins_home/hudson.plugins.git.GitTool.xml