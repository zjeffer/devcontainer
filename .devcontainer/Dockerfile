FROM archlinux:latest

RUN pacman -Syyu --noconfirm python3 openssh zsh git curl wget sudo base-devel cmake make gcc gdb ninja

RUN echo 'Include = /etc/pacman.d/mirrorlist' >> /etc/pacman.conf && \
    useradd -m -r -s /bin/bash aur && \
    passwd -d aur && \
    echo 'aur ALL=(ALL) ALL' > /etc/sudoers.d/aur && \
    mkdir -p /home/aur/.gnupg && \
    echo 'standard-resolver' > /home/aur/.gnupg/dirmngr.conf && \
    chown -R aur:aur /home/aur && \
    mkdir /build && \
    chown -R aur:aur /build && \
    cd /build && \
    sudo -u aur git clone --depth 1 https://aur.archlinux.org/paru.git && \
    cd paru && \
    sudo -u aur makepkg --noconfirm -si && \
    sed -i 's/#RemoveMake/RemoveMake/g' /etc/paru.conf && \
    pacman -Qtdq | xargs -r pacman --noconfirm -Rcns && \
    rm -rf /home/aur/.cache && \
    rm -rf /build

USER root
ENV HOME /root

################# ZSH #################
ENV TERM xterm
ENV SHELL /bin/zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true
ADD .zshrc $HOME
