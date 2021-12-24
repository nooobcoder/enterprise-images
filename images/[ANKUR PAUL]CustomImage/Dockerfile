FROM codercom/enterprise-base:ubuntu

SHELL ["/bin/bash", "-c"]
USER root

# Install baseline packages
RUN apt-get update && \
    DEBIAN_FRONTEND="noninteractive" apt-get install --yes \
      bash \
      build-essential \
      ca-certificates \
      curl \
      docker.io \
      htop \
      locales \
      man \
      python3 \
      python3-pip \
      software-properties-common \
      sudo \
      systemd \
      systemd-sysv \
      g++ \
      zsh \
      gcc \
      gdb \
      unzip \
      vim \
      wget && \
    # Install latest Git using their official PPA
    add-apt-repository ppa:git-core/ppa && \
    DEBIAN_FRONTEND="noninteractive" apt-get install --yes git

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y nodejs

RUN mkdir project

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN DEBIAN_FRONTEND="noninteractive" apt-get update && apt-get install -y yarn
RUN sudo npm i -g nodemon serve eslint typescript npkill

COPY [ "configure", "/coder/configure" ]
COPY [ ".zshrc", "~/.zshrc" ]

RUN chmod +x /coder/configure

USER coder
RUN sudo chsh -s /bin/zsh $USER
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended


USER coder