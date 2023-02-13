FROM maven:3.8.1-openjdk-8 as java8
FROM maven:3.8.1-openjdk-11 as java11
FROM maven:3.8.1-openjdk-15 as java15
COPY --from=java8 /usr/local/openjdk-8 /usr/java/openjdk-8
COPY --from=java11 /usr/local/openjdk-11 /usr/java/openjdk-11

RUN microdnf install jq tmux vim ctags python3-pip wget procps

# Install java 7
WORKDIR /tmp
ARG JAVA7_URL="https://download.java.net/openjdk/jdk7u75/ri/jdk_ri-7u75-b13-linux-x64-18_dec_2014.tar.gz"
RUN curl -o openjdk-7.tar.gz ${JAVA7_URL}
RUN mkdir -p /usr/java/openjdk-7 && \
      tar xf /tmp/openjdk-7.tar.gz -C /usr/java/openjdk-7 --strip-components 1

# Setup JDKs
RUN echo "alias setJava7='export JAVA_HOME=/usr/java/openjdk-7 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /root/.bashrc
RUN echo "alias setJava8='export JAVA_HOME=/usr/java/openjdk-8 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /root/.bashrc
RUN echo "alias setJava11='export JAVA_HOME=/usr/java/openjdk-11 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /root/.bashrc
RUN echo "alias setJava15='export JAVA_HOME=/usr/java/openjdk-15 && export PATH=\${JAVA_HOME}/bin:\${PATH}'" >> /root/.bashrc

# Install packages and setup
WORKDIR /tmp
COPY configs /tmp/configs

# vim
RUN git clone https://github.com/VundleVim/Vundle.vim.git /root/.vim/bundle/Vundle.vim
RUN cat configs/vimrc >> /root/.vimrc
RUN vim +PluginInstall +qall >/dev/null 2>&1

# tmux
RUN cat configs/tmux.conf >> /root/.tmux.conf

# bashrc
RUN cat configs/bashrc >> /root/.bashrc
RUN rm -rf /tmp/configs

# pandas
RUN pip3 install pandas

# disable maven-default-http-blocker
WORKDIR /tmp/scripts
COPY disable_maven_blocker.sh .
RUN ./disable_maven_blocker.sh

WORKDIR /root

ENTRYPOINT [ "/bin/bash" ]
