### Base image we use to create our image from
FROM jenkins/jenkins

### info about 
### MAINTAINER atlas-team (email)

### get rid of admin password setup
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

### automatically installing plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

USER root
### create folders for maven & JDK
RUN mkdir /usr/share/jenkins/ref/downloads && \
        mkdir /tools

RUN curl "http://mirror.vorboss.net/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz" > /usr/share/jenkins/ref/downloads/apache-maven-3.5.2-bin.tar.gz
RUN curl "http://ftp.osuosl.org/pub/funtoo/distfiles/oracle-java/jdk-8u144-linux-x64.tar.gz" > /usr/share/jenkins/ref/downloads/jdk-8u144-linux-x64.tar.gz

RUN cd /usr/share/jenkins/ref/downloads && \
        tar xzvf jdk-8u144-linux-x64.tar.gz -C /tools && \
        tar xzvf apache-maven-3.5.2-bin.tar.gz -C /tools

### copy maven settings file
RUN cd /tools && \
        mkdir -m 777 maven_repository
COPY settings.xml /tools/apache-maven-3.5.2/conf/settings.xml


USER jenkins
COPY groovy/* /usr/share/jenkins/ref/init.groovy.d/
