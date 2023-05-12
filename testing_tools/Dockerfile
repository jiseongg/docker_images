FROM jiseongg301/evosuite as evosuite
FROM jiseongg301/randoop as randoop
FROM jiseongg301/npetest as npetest

FROM jiseongg301/java_base

# Copy Tools
COPY --from=evosuite /tools/evosuite-1.1.0 /tools/evosuite-1.1.0
COPY --from=evosuite /tools/evosuite-1.2.0 /tools/evosuite-1.2.0
COPY --from=randoop /tools/randoop /tools/randoop
COPY --from=npetest /tools/npetest /tools/npetest

WORKDIR /

ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD [ "/bin/bash" ]
