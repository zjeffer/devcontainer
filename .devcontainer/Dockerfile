FROM archlinux:latest

RUN pacman -Syyu --noconfirm python3 openssh zsh git curl wget sudo base-devel

RUN echo 'Include = /etc/pacman.d/mirrorlist' >> /etc/pacman.conf && \
    useradd -m -r -s /bin/bash user && \
    passwd -d user && \
    echo 'user ALL=(ALL) ALL' > /etc/sudoers.d/user && \
    mkdir -p /home/user/.gnupg && \
    echo 'standard-resolver' > /home/user/.gnupg/dirmngr.conf && \
    chown -R user:user /home/user && \
    mkdir /build && \
    chown -R user:user /build && \
    cd /build && \
    sudo -u user git clone --depth 1 https://aur.archlinux.org/paru.git && \
    cd paru && \
    sudo -u user makepkg --noconfirm -si && \
    sed -i 's/#RemoveMake/RemoveMake/g' /etc/paru.conf && \
    pacman -Qtdq | xargs -r pacman --noconfirm -Rcns && \
    rm -rf /home/user/.cache && \
    rm -rf /build

USER root
ENV HOME /root

################# ZSH #################
ENV TERM xterm
ENV SHELL /bin/zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true
ADD .zshrc $HOME
