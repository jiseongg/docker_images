FROM jiseongg301/java_base as base

LABEL maintainer="jiseongg"
USER jiseongg

ENV JAVA_HOME /usr/java/openjdk-11

# Build Randop
WORKDIR /home/jiseongg/tools
RUN git clone https://github.com/randoop/randoop -b v4.3.0 --depth 1 --quiet && \
    cd randoop && \
    ./gradlew assemble -x test

# Reset JAVA_HOME to Java 15
ENV JAVA_HOME /usr/java/openjdk-15
