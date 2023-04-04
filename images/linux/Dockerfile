FROM ubuntu:22.04

ENV HELPER_SCRIPTS=./helpers

COPY ./scripts .
COPY ./toolsets .


RUN apt-get update -yqq && apt-get install -yqq jq wget curl unzip lsb-release sudo


RUN echo 'echo $@' > /usr/bin/invoke_tests
RUN chmod +x /usr/bin/invoke_tests

RUN echo 'echo "$(jq -r "$query" toolset-2204.json)"' > /usr/bin/get_toolset_value
RUN chmod +x /usr/bin/get_toolset_value

RUN mkdir -p /imagegeneration/installers/
RUN cp toolset-2204.json /imagegeneration/installers/toolset.json

RUN bash base/repos.sh

RUN bash installers/git.sh
RUN bash installers/nodejs.sh
# RUN bash installers/nvm.sh
RUN bash installers/java-tools.sh

RUN chmod 777 /opt

RUN mkdir -p /home/runner \
 && echo "runner:x:1000:1000:runner:/home/runner:/bin/bash" >> /etc/passwd \
 && echo "runner:x:1000:" >> /etc/group \
 && echo "runner::::::::" >> /etc/shadow \
 && chown -R runner /home/runner \
 && echo 'runner ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER runner

WORKDIR /home/runner
