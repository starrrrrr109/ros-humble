FROM ros:humble-ros-base-jammy

ENV RUNNING_IN_DOCKER true
ENV SHELL /bin/bash

ARG USER=humble
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y \
    git \
    sudo \
    curl \
    wget \
    usbutils \
    v4l-utils \
    && apt clean -y && rm -rf /var/lib/apt/lists/*

RUN groupadd --gid $USER_GID $USER \
    && useradd --uid $USER_UID --gid $USER_GID -ms /bin/bash $USER \
    && usermod -aG sudo,video $USER \
    && echo "$USER ALL=(ALL) NOPASSWD:ALL" | tee /etc/sudoers.d/$USER \
    && echo "source /opt/ros/humble/setup.bash" >> /home/$USER/.bashrc

USER $USER
WORKDIR /home/$USER/humble_ws

CMD [ "/bin/bash" ]