FROM maven:3.8.1-openjdk-15 as mvn_java15
FROM openjdk:8-jdk as java8
FROM openjdk:11-jdk as java11
FROM ubuntu:20.04 as base

LABEL maintainer="jiseongg"

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --no-install-recommends install \
      sudo vim wget git python3-pip jq &&\
    useradd -m jiseongg && \
    echo jiseongg:jiseongg | chpasswd && \
    cp /etc/sudoers /etc/sudoers.bak && \
    echo 'jiseongg ALL=(root) NOPASSWD: ALL' >> /etc/sudoers

COPY --chown=jiseongg:jiseongg --from=java8 /usr/local/openjdk-8 /usr/java/openjdk-8
COPY --chown=jiseongg:jiseongg --from=java11 /usr/local/openjdk-11 /usr/java/openjdk-11
COPY --chown=jiseongg:jiseongg --from=mvn_java15 /usr/java/openjdk-15 /usr/java/openjdk-15
COPY --chown=jiseongg:jiseongg --from=mvn_java15 /usr/share/maven /usr/share/maven

USER jiseongg

ENV JAVA_HOME="/usr/java/openjdk-15"
ENV PATH="/home/jiseongg/tools/npetest/apps/bin:${JAVA_HOME}/bin:/usr/share/maven/bin:${PATH}"

RUN echo "# JAVA, Maven" >> /home/jiseongg/.bashrc
RUN echo "alias setJava8='export JAVA_HOME=/usr/java/openjdk-8 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /home/jiseongg/.bashrc
RUN echo "alias setJava11='export JAVA_HOME=/usr/java/openjdk-11 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /home/jiseongg/.bashrc
RUN echo "alias setJava15='export JAVA_HOME=/usr/java/openjdk-15 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /home/jiseongg/.bashrc

