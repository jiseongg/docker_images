FROM maven:3.8.1-openjdk-11 as build

# Build Randop
WORKDIR /tmp
RUN git clone http://github.com/randoop/randoop -b v4.3.0 --depth 1 --quiet && \
    cd randoop && \
    ./gradlew assemble -x test && \
    mkdir -p /tools/randoop && \
    mv build/libs/randoop-all*.jar /tools/randoop/randoop.jar

# Setup path
FROM openjdk:11-jdk as randoop
WORKDIR /tools/randoop
COPY --from=build /tools/randoop/randoop.jar .
