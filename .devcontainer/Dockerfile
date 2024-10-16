# syntax=docker.io/docker/dockerfile:1.10

# see https://gradle.org/install/#manually
ARG GRADLE_VERSION='8.10.2'

# see https://github.com/devcontainers/images/tree/main/src/base-debian/history
FROM mcr.microsoft.com/devcontainers/base:1.0.16-bookworm

RUN <<'EOF'
#!/usr/bin/bash
set -euxo pipefail
export DEBIAN_FRONTEND=noninteractive
apt-get update
apt-get -y install --no-install-recommends \
    bash-completion \
    curl \
    openjdk-17-jdk-headless \
    sudo \
    unzip
apt-get clean
rm -rf /var/lib/apt/lists/*
EOF

# install gradle.
# see https://gradle.org/releases/
ARG GRADLE_VERSION
RUN <<'EOF'
#!/usr/bin/bash
set -euxo pipefail
url="https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip"
t="$(mktemp -q -d --suffix=.gradle)"
wget -qO "$t/gradle.zip" "$url"
unzip "$t/gradle.zip" -d /opt/gradle
mv "/opt/gradle/gradle-${GRADLE_VERSION}/"* /opt/gradle
rmdir "/opt/gradle/gradle-${GRADLE_VERSION}"
rm -rf "$t"
EOF
ENV PATH="/opt/gradle/bin:$PATH"

RUN <<'EOF'
#!/usr/bin/bash
set -euxo pipefail
# ensure /etc/profile is called at the top of the file, when running in a
# login shell.
sed -i '0,/esac/s/esac/&\n\nsource \/etc\/profile/' /home/vscode/.bashrc
EOF
COPY inputrc /etc/inputrc
COPY login.sh /etc/profile.d/login.sh
