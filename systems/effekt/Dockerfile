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

RUN echo 'tzdata tzdata/Areas select Europe' | sudo debconf-set-selections
RUN echo 'tzdata tzdata/Zones/Europe select London' | sudo debconf-set-selections
RUN sudo apt-get install -qqy --no-install-recommends tzdata

# Install mlton
RUN sudo apt install -y mlton git make wget default-jdk
# RUN npm install -g https://github.com/effekt-lang/effekt/releases/latest/download/effekt.tgz

# Install Multicore OCaml
# RUN sudo apt install -y wget git curl gcc make m4 unzip bubblewrap bzip2
# RUN curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh > /tmp/install.sh
# RUN ["/bin/bash", "-c", "sudo /bin/bash /tmp/install.sh <<< /usr/local/bin"]

# RUN opam init -y --disable-sandboxing --bare
# RUN echo "test -r /home/ubuntu/.opam/opam-init/init.sh && . /home/ubuntu/.opam/opam-init/init.sh > /dev/null 2> /dev/null || true" >> /home/ubuntu/.profile

# RUN opam switch create -y 4.12.0+domains+effects
# RUN eval $(opam env)

RUN wget https://github.com/sharkdp/hyperfine/releases/download/v1.11.0/hyperfine_1.11.0_amd64.deb
RUN sudo dpkg -i hyperfine_1.11.0_amd64.deb
# RUN opam install dune

ENV DEBIAN_FRONTEND teletype
CMD ["/bin/bash"]
