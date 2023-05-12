FROM jiseongg301/java_base as build

# Build EvoSuite 1.1.0
WORKDIR /tmp
RUN git clone https://github.com/jiseongg/evosuite -b experiment_v1.1.0 --depth 1 --quiet && \
    cd evosuite && \
    JAVA_HOME=/usr/java/openjdk-8 mvn package -DskipTests -DskipITs -B

WORKDIR /tools/evosuite
RUN mv /tmp/evosuite/master/target/evosuite-master-*-tests.jar evosuite-tests.jar && \
    mv /tmp/evosuite/master/target/evosuite-master-*.jar evosuite.jar && \
    mv /tmp/evosuite/standalone_runtime/target/evosuite-standalone-runtime-*-tests.jar evosuite-rt-tests.jar && \
    mv /tmp/evosuite/standalone_runtime/target/evosuite-standalone-runtime-*.jar evosuite-rt.jar && \
    rm -rf /tmp/evosuite

WORKDIR /

ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD [ "/bin/bash" ]
