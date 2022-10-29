FROM jiseongg301/java_base as build

# Build Randop
WORKDIR /tmp
RUN git clone http://github.com/randoop/randoop -b v4.3.0 --depth 1 --quiet && \
    cd randoop && \
    JAVA_HOME=/usr/java/openjdk-11 ./gradlew assemble -x test && \
    mkdir -p /tools/randoop && \
    mv build/libs/randoop-all*.jar /tools/randoop/randoop.jar

# Setup path
FROM jiseongg301/java_base as randoop
WORKDIR /tools/randoop
COPY --from=build /tools/randoop/randoop.jar .
