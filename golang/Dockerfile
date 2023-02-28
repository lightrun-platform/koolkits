FROM ubuntu:20.04
ENV GO_VERSION=go1.19.6
ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-c"]

RUN apt-get update && \
    apt-get install --yes --no-install-recommends --quiet \
    apache2-utils \
    binutils \
    bird \
    bison \
    bpfcc-tools \
    bridge-utils \
    build-essential \
    conntrack \
    ctop \
    curl \
    dhcping \
    dnsutils \
    ethtool \
    fping \
    fzf \
    gdb \
    git \
    gnupg2 \
    htop \
    httpie \
    iftop \
    iperf \
    iproute2 \
    ipset \
    iptables \
    iptraf-ng \
    iputils-ping \
    ipvsadm \
    jq \
    liboping-dev \
    libunwind8 \
    linux-tools-common \
    mtr \
    mycli \
    netcat \
    netgen \
    nftables \
    ngrep \
    nmap \
    pgcli \
    postgresql \
    python3-pip \
    python3.8 \
    scapy \
    snmp \
    snmpd \
    socat \
    software-properties-common \
    strace \
    tcpdump \
    tcptraceroute \
    termshark \
    tmux \
    tshark \
    unzip \
    util-linux \
    vim \
    wuzz 

WORKDIR /usr/local/bin

# Get pip packages 
RUN pip3 install litecli iredis 
# Get flamegraph 
RUN curl -L https://github.com/brendangregg/FlameGraph/archive/refs/heads/master.zip -o flamegraph.zip && \
    unzip flamegraph.zip && \
    rm flamegraph.zip && \
    echo "alias flamegraph='/usr/local/bin/FlameGraph-master/flamegraph.pl'" >> /root/.bashrc && \
    # Get redis-cli
    curl http://download.redis.io/redis-stable.tar.gz -o redis-stable.tar.gz && \ 
    tar -xvzf redis-stable.tar.gz && \
    rm redis-stable.tar.gz && \
    cd redis-stable && \
    make && \ 
    echo "alias redis-cli='/usr/local/bin/redis-stable/src/redis-cli'" >> /root/.bashrc 
# Get alp
RUN curl -L https://github.com/tkuchiki/alp/releases/download/v1.0.8/alp_linux_amd64.zip -o alp.zip && \
    unzip alp.zip && \
    rm alp.zip 
#Get gvm and install golang
RUN bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer) && \
    source /root/.gvm/scripts/gvm && \
    gvm install $GO_VERSION -B && \
    gvm use $GO_VERSION --default 
# Get pprof
RUN GOBIN=/usr/local/bin ~/.gvm/gos/go1.19.6/bin/go install github.com/google/pprof@latest &&\
    # Get dlv
    ~/.gvm/gos/go1.19.6/bin/go install github.com/go-delve/delve/cmd/dlv@latest && \
    # Get go-callvis
    ~/.gvm/gos/go1.19.6/bin/go install github.com/ofabry/go-callvis@latest
# Get mongo shell (not available over apt)
RUN curl -L https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-shell_5.0.5_amd64.deb -o mongodb-org-shell_5.0.5_amd64.deb && \
    dpkg -i mongodb-org-shell_5.0.5_amd64.deb && \
    rm mongodb-org-shell_5.0.5_amd64.deb && \
    #Get calicoctl (inside the pod)
    curl -L https://github.com/projectcalico/calico/releases/latest/download/calicoctl-linux-amd64 -o calicoctl && \
    chmod +x calicoctl && \
    #Get websocat (not available over apt)
    curl -L https://github.com/vi/websocat/releases/latest/download/websocat_linux64 -o websocat && \
    chmod +x websocat    

CMD ["/bin/bash"]