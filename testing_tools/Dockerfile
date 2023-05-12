FROM jiseongg301/evosuite as evosuite
FROM jiseongg301/randoop as randoop
FROM jiseongg301/npetest as npetest

FROM jiseongg301/java_base

# Copy Tools
COPY --from=evosuite /tools/evosuite /tools/evosuite
COPY --from=randoop /tools/randoop /tools/randoop
COPY --from=npetest /tools/npetest /tools/npetest

WORKDIR /

ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
CMD [ "/bin/bash" ]
