FROM archlinux/base:latest
RUN pacman -Sy --noconfirm reflector;reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
RUN pacman -Syu --noconfirm tar openssh git sudo man python-pip make rsh docker wget socat htop texlive-most texlive-lang texlive-langextra biber pandoc
ENV PATH=$PATH:/usr/bin/core_perl
RUN groupadd sudo
RUN useradd -mG sudo user
RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL">/etc/sudoers.d/sudo_nopass
COPY ./docker-redirect /bin/docker-redirect
RUN chmod 744 /bin/docker-redirect && chown root:root /bin/docker-redirect && chmod u+s /bin/docker-redirect
USER user
COPY ./.zshrc /home/user/.zshrc
SHELL ["/usr/bin/zsh","-c"]
ONBUILD RUN sudo reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
ONBUILD RUN sudo pacman -Syu --noconfirm
