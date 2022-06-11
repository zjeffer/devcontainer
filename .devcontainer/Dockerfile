FROM ubuntu:latest

RUN apt update && apt -y install python3 python3-pip ssh zsh git curl wget sudo

RUN apt install -y locales
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && /usr/sbin/locale-gen

USER root
ENV HOME /root

################# ZSH #################
ENV TERM xterm
ENV SHELL /bin/zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true
ADD .zshrc $HOME
