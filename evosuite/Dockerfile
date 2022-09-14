FROM maven:3.8.1-openjdk-11 as build

# Build EvoSuite
WORKDIR /tmp
RUN git clone https://github.com/jiseongg/evosuite -b experiment_v1.2.0 --depth 1 --quiet && \
    cd evosuite && \
    mvn package -DskipTests -DskipITs -B && \
    mkdir -p /tools/evosuite && \
    mv master/target/evosuite-master-*-tests.jar /tools/evosuite/evosuite-tests.jar && \
    mv master/target/evosuite-master-*.jar /tools/evosuite/evosuite.jar

# Setup path
FROM openjdk:11-jdk as evosuite
WORKDIR /tools/evosuite
COPY --from=build /tools/evosuite/evosuite.jar ./evosuite.jar
