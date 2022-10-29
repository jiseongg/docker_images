FROM jiseongg301/java_base as build

# Build EvoSuite
WORKDIR /tmp
RUN git clone https:///github.com/jiseongg/evosuite -b experiment_v1.1.0 --depth 1 --quiet && \
    cd evosuite && \
    JAVA_HOME=/usr/java/openjdk-11 mvn package -DskipTests -DskipITs -B && \
    ls && \
    mkdir -p /tools/evosuite && \
    mv master/target/evosuite-master-*-tests.jar /tools/evosuite/evosuite-tests.jar && \
    mv master/target/evosuite-master-*.jar /tools/evosuite/evosuite.jar && \
    mv standalone_runtime/target/evosuite-standalone-runtime-*-tests.jar /tools/evosuite/evosuite-rt-tests.jar && \
    mv standalone_runtime/target/evosuite-standalone-runtime-*.jar /tools/evosuite/evosuite-rt.jar

# Setup path
FROM jiseongg301/java_base as evosuite
WORKDIR /tools/evosuite
COPY --from=build /tools/evosuite/evosuite.jar ./evosuite.jar
COPY --from=build /tools/evosuite/evosuite-tests.jar ./evosuite-tests.jar
COPY --from=build /tools/evosuite/evosuite-rt.jar ./evosuite-rt.jar
COPY --from=build /tools/evosuite/evosuite-rt-tests.jar ./evosuite-rt-tests.jar
