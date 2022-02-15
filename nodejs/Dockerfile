FROM ubuntu:20.04
ENV NODE_VERSION=16.13.1
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --yes --no-install-recommends --quiet \
    bird \
    conntrack \
    ctop \
    curl \
    dhcping \
    dnsutils \
    fping \
    gdb \
    git \
    htop \
    httpie \
    iftop \
    iperf \
    ipset \
    iptraf-ng \
    iproute2 \
    iputils-ping \
    ipvsadm \
    jq \
    ldnsutils \
    liboping-dev \
    linux-tools-common \
    mtr \
    mycli \
    mysql-client \
    netcat \
    netgen \
    nftables \
    ngrep \
    nmap \
    pgcli \
    postgresql-client \
    redis-tools \
    scapy \
    socat \
    software-properties-common \
    strace \
    tcpdump \
    tcptraceroute \
    termshark \
    tmux \
    tshark \
    vim \
    wuzz && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install node and relevant tools
WORKDIR /usr/local/bin
RUN apt-get update && apt-get install -y curl && cd /usr/local/bin && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash && \
    . /root/.nvm/nvm.sh && \
    export NODE_VERSION=16.13.1 && \
    # Set up node and global npm packages
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    nvm use default && \
    npm --install prefix "usr/local/bin" && \
    npm install ndb 0x whistle vtop && \
    # Get everything on path instead of installing globally
    echo "alias ndb='/usr/local/bin/node_modules/.bin/ndb'" >> /root/.bashrc && \
    echo "alias 0x='/usr/local/bin/node_modules/.bin/0x'" >> /root/.bashrc && \
    echo "alias whistle='/usr/local/bin/node_modules/.bin/whistle'" >> /root/.bashrc && \
    echo "alias vtop='/usr/local/bin/node_modules/.bin/vtop'" >> /root/.bashrc && \
    # Get calicoctl (inside the pod)
    curl -L https://github.com/projectcalico/calico/releases/latest/download/calicoctl-linux-amd64 -o calicoctl && \
    chmod +x calicoctl && \
    # Get websocat (not available over apt)
    curl -L https://github.com/vi/websocat/releases/latest/download/websocat_linux64 -o websocat && \
    chmod +x websocat && \
    # Get mongo shell (not available over apt)
    curl -L https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-shell_5.0.5_amd64.deb -o mongodb-org-shell_5.0.5_amd64.deb && \
    dpkg -i mongodb-org-shell_5.0.5_amd64.deb && \
    rm mongodb-org-shell_5.0.5_amd64.deb

CMD ["/bin/bash"]

