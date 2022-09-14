FROM jiseongg301/java_base as base

LABEL maintainer="jiseongg"
USER jiseongg

ENV JAVA_HOME /usr/java/openjdk-11

# Build EvoSuite
WORKDIR /home/jiseongg/tools
RUN git clone https://github.com/jiseongg/evosuite -b experiment_v1.2.0 --depth 1 --quiet && \
    cd evosuite && \
    mvn clean package -DskipTests -DskipITs -B

# Reset JAVA_HOME to Java 15
ENV JAVA_HOME /usr/java/openjdk-15
