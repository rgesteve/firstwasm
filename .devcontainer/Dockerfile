FROM ubuntu:focal

ARG USERNAME=codespace
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ENV EMSDK /opt/emsdk

RUN apt update \
    && apt install -y \
    wget \
    ca-certificates \
    build-essential \
    python python-pip \
    python3 python3-pip \
	git-core \
    # Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    # [Optional] Add sudo support for the non-root user
    && apt install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME 
    #
    # Clean up
    #&& apt autoremove -y \
    #&& apt clean -y

RUN git clone https://github.com/emscripten-core/emsdk.git ${EMSDK} \
    && cd ${EMSDK} \
    # Fetch the latest version of the emsdk (not needed the first time you clone)
    && git pull

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog
