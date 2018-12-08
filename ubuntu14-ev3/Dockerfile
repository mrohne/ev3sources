FROM i686/ubuntu:14.04
ENV container docker

# install software
RUN apt-get update -y --fix-missing
RUN apt-get upgrade -y --fix-missing
RUN apt-get install -y --fix-missing apt-utils
RUN apt-get install -y --fix-missing sudo bash
RUN apt-get install -y --fix-missing default-jre
RUN apt-get install -y --fix-missing curl bzip2 make gcc doxygen imagemagick u-boot-tools

# make /bin/sh symlink to bash instead of dash:
RUN echo "dash dash/sh boolean false" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# copy and install CodeSourcery w/expect
# COPY arm-2009q1-203-arm-none-linux-gnueabi.bin .
# COPY arm-2009q1-203-arm-none-linux-gnueabi.exp .
#RUN ./arm-2009q1-203-arm-none-linux-gnueabi.exp
# download directly from mentor.com
RUN mkdir -p /local/CodeSourcery && \
    curl -s -L "https://sourcery.mentor.com/public/gnu_toolchain/arm-none-linux-gnueabi/arm-2009q1-203-arm-none-linux-gnueabi-i686-pc-linux-gnu.tar.bz2" |\
    bunzip2 -d --stdout | sudo tar -C /local/CodeSourcery -xf -
ENV PATH /local/CodeSourcery/arm-2009q1/bin:${PATH}

# set up user environment
RUN adduser --disabled-password --gecos '' ev3
RUN usermod -aG sudo ev3
RUN echo "ev3 ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER ev3
ENV TERM xterm
ENV HOME /opt/EV3
ENV LANG en_US.UTF-8
WORKDIR /opt/EV3
CMD bash