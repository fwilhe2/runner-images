FROM ubuntu:22.04

ENV HELPER_SCRIPTS=./helpers

COPY ./scripts .
COPY ./toolsets .

RUN  apt-get update -yqq && apt-get install -yqq jq wget curl unzip lsb-release sudo lbzip2 \
    && echo 'echo $@' > /usr/bin/invoke_tests \
    && chmod +x /usr/bin/invoke_tests \
    && echo 'echo "$(jq -r "$query" toolset-2204-slim.json)"' > /usr/bin/get_toolset_value \
    && chmod +x /usr/bin/get_toolset_value \
    && mkdir -p /imagegeneration/installers/ \
    && cp toolset-2204-slim.json /imagegeneration/installers/toolset.json \
    && bash base/repos.sh \
    && bash installers/configure-environment.sh \
    && apt-get install -yqq autoconf automake build-essential dbus dnsutils dpkg fakeroot fonts-noto-color-emoji gnupg2 imagemagick iproute2 iputils-ping lib32z1 libc++abi-dev libc++-dev libcurl4 libgbm-dev libgconf-2-4 libgsl-dev libgtk-3-0 libmagic-dev libmagickcore-dev libmagickwand-dev libsecret-1-dev libsqlite3-dev libyaml-dev libtool libunwind8 libxkbfile-dev libxss1 libssl-dev locales mercurial openssh-client p7zip-rar pkg-config python-is-python3 rpm tar texinfo tk tzdata upx xorriso xvfb xz-utils zsync \
    && apt-get install -yqq acl aria2 binutils bison brotli bzip2 coreutils curl file flex ftp haveged jq lz4 m4 mediainfo netcat net-tools p7zip-full parallel pass patchelf pollinate rsync shellcheck sphinxsearch sqlite3 ssh sshpass subversion sudo swig telnet time unzip wget zip \
    # && bash installers/git.sh \
    # && bash installers/github-cli.sh \
    # && bash installers/nodejs.sh \
    # && bash installers/python.sh \
    # && bash installers/java-tools.sh \
    && chmod -R 777 /opt \
    && chmod -R 777 /usr/share \
    && mkdir -p /home/runner \
    && echo "runner:x:1000:1000:runner:/home/runner:/bin/bash" >> /etc/passwd \
    && echo "runner:x:1000:" >> /etc/group \
    && echo "runner::::::::" >> /etc/shadow \
    && chown -R runner /home/runner \
    && echo 'runner ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
    && bash installers/cleanup.sh

USER runner

WORKDIR /home/runner
