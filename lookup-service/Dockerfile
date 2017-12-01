#################################
# Dockerfile for Lookup Service #
# BigDataEurope                 #
#                               #
# java 1.8.0_151                #
# maven 3.0.5                   #
# git 1.9.1                     #
# tomcat 8.0.23                 #
#################################

FROM ubuntu:14.04
MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>

ENV PORT 8080
ENV TOMCAT_MAJOR_VERSION 8
ENV TOMCAT_MINOR_VERSION 8.0.23

# INSTALL PREREQUISITIES
RUN apt-get update \
 && apt-get install -y \
    wget \
    curl \
    maven \
    git \
    vim \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# (NEW) JAVA8-INSTALLATION
RUN apt-get update \
 && apt-get install -y software-properties-common \
 && add-apt-repository -y ppa:webupd8team/java \
 && apt update \
 && echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections \
 && apt install -y oracle-java8-installer

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* tomcat

RUN git clone https://github.com/big-data-europe/pilot-sc7-lookup-service.git && \
	cd pilot-sc7-lookup-service && \
	mvn clean package

RUN cp /pilot-sc7-lookup-service/target/*.war /tomcat/webapps

ADD lookup.sh /lookup.sh
ADD gadm28.zip /gadm28.zip
RUN chmod +x /*.sh \
    && unzip gadm28.zip

EXPOSE $PORT
CMD ["/bin/bash", "/lookup.sh"]
