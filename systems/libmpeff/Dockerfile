FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

# Get the basic stuff
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y \
    sudo

# Create ubuntu user with sudo privileges
RUN useradd -ms /bin/bash ubuntu && \
    usermod -aG sudo ubuntu
# New added for disable sudo password
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set as default user
USER ubuntu
WORKDIR /home/ubuntu

# Configure tzdata
RUN echo 'tzdata tzdata/Areas select Europe' | sudo debconf-set-selections
RUN echo 'tzdata tzdata/Zones/Europe select London' | sudo debconf-set-selections
RUN sudo apt-get install -qqy --no-install-recommends tzdata

# Install libmprompt/libmpeff
RUN sudo apt install -y wget git curl gcc make cmake
RUN curl -o libmprompt-0.6.3.tar.gz -sL https://github.com/koka-lang/libmprompt/archive/refs/tags/v0.6.3.tar.gz
RUN tar xvf libmprompt-0.6.3.tar.gz
WORKDIR ./libmprompt-0.6.3

CMD ["/bin/bash" "mkdir" "-p" "out/release"]
WORKDIR ./out/release
CMD ["/bin/cmake" "../.."]
CMD ["/bin/make"]

ENV DEBIAN_FRONTEND teletype

CMD ["/bin/bash"]