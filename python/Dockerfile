FROM ubuntu:20.04
ENV PYTHON_VERSION=3.9.16
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --yes --no-install-recommends --quiet \
    bird \
    build-essential \
    ca-certificates \
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
    iproute2 \
    ipset \
    iptraf-ng \
    iputils-ping \
    ipvsadm \
    jq \
    ldnsutils \
    libbz2-dev \
    libedit-dev \
    libffi-dev \
    liblzma-dev \
    libncursesw5-dev \
    liboping-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxmlsec1-dev \
    linux-tools-common \
    llvm \
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
    tk-dev \
    tmux \
    tshark \
    unzip \
    vim \
    wget \
    wuzz \
    xz-utils \
    zip \
    zlib1g-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/bin
# Get pyenv (Python version swapping)
RUN curl https://pyenv.run | bash && \
    echo 'export PATH="$HOME/.pyenv/bin:$PATH"' >> /root/.bashrc && \
    echo 'eval "$(pyenv init --path)"' >> /root/.bashrc && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> /root/.bashrc && \
    . /root/.bashrc && \
    pyenv install ${PYTHON_VERSION} && \
    pyenv global ${PYTHON_VERSION} && \
    pip install \
    ipdb \
    ipython \
    line_profiler \
    lptrace \
    memory_profiler \
    pdbpp \
    pudb \ 
    pyinstrument \
    scalene \
    vprof && \
    # pip in bash doesn't play nicely with package names with dashes 
    pip install py-heat-magic py-spy && \
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
