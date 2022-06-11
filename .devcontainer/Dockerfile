FROM archlinux:latest

RUN pacman -Syyu --noconfirm python3 openssh zsh git curl wget sudo

USER root
ENV HOME /root

################# ZSH #################
ENV TERM xterm
ENV SHELL /bin/zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true
ADD .zshrc $HOME
