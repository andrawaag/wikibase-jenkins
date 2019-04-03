FROM jenkins/jenkins:lts

MAINTAINER Andra Waagmeester <andra@micelio.be>

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
RUN install-plugins.sh slack conditional-buildstep parameterized-trigger
# # # COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
# # # RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

USER root

RUN apt-get update && apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev  libncursesw5-dev xz-utils tk-dev
RUN wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz && tar xvf Python-3.6.4.tgz
RUN cd Python-3.6.4 && ./configure --enable-optimizations && make -j8 && make altinstall

RUN apt-get update && apt-get install -y git virtualenv

USER jenkins 
RUN pwd

# docker build -t wurssb/jenkins .
# docker run -it wurssb/jenkins

ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]


