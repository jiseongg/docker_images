FROM jiseongg301/evosuite as evosuite
FROM jiseongg301/randoop as randoop
FROM jiseongg301/npetest as npetest

FROM jiseongg301/java_base

# junit test driver
WORKDIR /tools/junit
RUN wget https://repo1.maven.org/maven2/junit/junit/4.12/junit-4.12.jar -O junit.jar
RUN wget https://repo1.maven.org/maven2/org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar -O hamcrest-core.jar

# Copy Tools
COPY --from=evosuite /tools/evosuite /tools/evosuite
COPY --from=randoop /tools/randoop /tools/randoop
COPY --from=npetest /tools/npetest /tools/npetest

WORKDIR /

ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD [ "/bin/bash" ]
