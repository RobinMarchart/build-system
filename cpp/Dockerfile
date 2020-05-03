FROM archlinux/base:latest
RUN pacman -Sy --noconfirm reflector;reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
RUN pacman -Syu --noconfirm tar openssh git sudo man gcc clang cmake meson llvm python-pip gdb awk make bison gettext bash-completion docker wget socat htop lib32-gcc-libs openmp openmpi
RUN pip install conan
ENV CONAN_CMAKE_GENERATOR=Ninja
ENV PATH=$PATH:/usr/bin/core_perl
RUN groupadd sudo
RUN useradd -G sudo user && mkdir /home/user && chown user:user /home/user
RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL">/etc/sudoers.d/sudo_nopass
COPY ./docker-redirect /bin/docker-redirect
RUN chmod 744 /bin/docker-redirect && chown root:root /bin/docker-redirect && chmod u+s /bin/docker-redirect
COPY ./conan /conan-setup
USER user
RUN conan config install /conan-setup
ONBUILD RUN sudo reflector --verbose --latest 10 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
ONBUILD RUN sudo pacman -Syu --noconfirm
