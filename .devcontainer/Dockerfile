FROM mcr.microsoft.com/devcontainers/dotnet:0-7.0
RUN dotnet dev-certs https

USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    ca-certificates \
    git \
    git-lfs \
    unzip \
    wget \
    zip \
    adb \
    libxkbcommon-x11-0 \
    dbus-x11 \
    x11-apps \
    x11-xserver-utils \
    libxinerama-dev \
    libx11-dev \
    openssh-server \
    xauth \
    mesa-utils \
    mesa-utils-extra \
    libxcursor1 \
    libxinerama1 \
    libxrandr2 \
    libxi6 \
    && apt-get -y autoremove \
    && apt-get clean \
    && mkdir /var/run/sshd \
    && mkdir /root/.ssh \
    && chmod 700 /root/.ssh \
    && ssh-keygen -A \
    && sed -i "s/^.*PasswordAuthentication.*$/PasswordAuthentication no/" /etc/ssh/sshd_config \
    && sed -i "s/^.*X11Forwarding.*$/X11Forwarding yes/" /etc/ssh/sshd_config \
    && sed -i "s/^.*X11UseLocalhost.*$/X11UseLocalhost no/" /etc/ssh/sshd_config \
    && grep "^X11UseLocalhost" /etc/ssh/sshd_config || echo "X11UseLocalhost no" >> /etc/ssh/sshd_config \
# my extras
    && rm -rf /var/lib/apt/lists/*

ARG GODOT_VERSION="4.1"
ARG RELEASE_NAME="stable"

RUN wget https://github.com/godotengine/godot/releases/download/${GODOT_VERSION}-${RELEASE_NAME}/Godot_v${GODOT_VERSION}-${RELEASE_NAME}_mono_linux_x86_64.zip

RUN mkdir ~/.cache \
    && mkdir -p ~/.config/godot \
    && mkdir -p ~/.local/share/godot/export_templates/${GODOT_VERSION}.${RELEASE_NAME} \
    && unzip Godot_v${GODOT_VERSION}-${RELEASE_NAME}_mono_linux_x86_64.zip \
    && mv Godot_v${GODOT_VERSION}-${RELEASE_NAME}_mono_linux_x86_64 /usr/local/bin/godot

ENV DISPLAY=${DOCKER_GATEWAY_HOST:-host.docker.internal}:0.0
ENV BLAH=TEST
ENV $BLAH=Test2

#RUN /usr/local/bin/godot/Godot_v4.1-stable_mono_linux.x86_64 -v -e --quit --display-driver headless