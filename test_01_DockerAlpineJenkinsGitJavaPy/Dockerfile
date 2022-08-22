# Install the base requirements for the app.
# This stage is to support development.

#FROM alpine:3.14
#RUN apk add --update docker openrc
#ENTRYPOINT ["docker"]
#RUN "docker volume create jenkins-base"
#RUN "docker container run -d -p 24:8080 -v jenkins-base:/var/jenkins_home --name jenkins-local jenkins/jenkins:lts"

FROM jenkins/jenkins:alpine

USER root

# Update apk repositories
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/main" > /etc/apk/repositories
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

ARG version=8.342.07.4
# Install the latest Git, Java [amazoncorretto], Python [py3], Docker and Docker-compose binaries
RUN apk add --no-cache git 
# https://github.com/corretto/corretto-docker/blob/85b940cab0e1ea3d5c3ba7f566b127e673b2389d/8/jdk/alpine/3.13/Dockerfile 
RUN wget -O /THIRD-PARTY-LICENSES-20200824.tar.gz https://corretto.aws/downloads/resources/licenses/alpine/THIRD-PARTY-LICENSES-20200824.tar.gz && \
    echo "82f3e50e71b2aee21321b2b33de372feed5befad6ef2196ddec92311bc09becb  /THIRD-PARTY-LICENSES-20200824.tar.gz" | sha256sum -c - && \
    tar x -ovzf THIRD-PARTY-LICENSES-20200824.tar.gz && \
    rm -rf THIRD-PARTY-LICENSES-20200824.tar.gz && \
    wget -O /etc/apk/keys/amazoncorretto.rsa.pub https://apk.corretto.aws/amazoncorretto.rsa.pub && \
    SHA_SUM="6cfdf08be09f32ca298e2d5bd4a359ee2b275765c09b56d514624bf831eafb91" && \
    echo "${SHA_SUM}  /etc/apk/keys/amazoncorretto.rsa.pub" | sha256sum -c - && \
    echo "https://apk.corretto.aws" >> /etc/apk/repositories && \
    apk add --no-cache amazon-corretto-8=$version-r0
RUN apk add --no-cache docker 	
RUN apk add --no-cache py3-pip py3-docopt py3-yaml py3-texttable py3-websocket-client py3-distro py3-dockerpty py3-jsonschema py3-dotenv py3-paramiko \
	&& pip install docker-compose