## golang KoolKit

<img src="./java-logo.png" style="max-width:20%;" />

KoolKits (**K**ubernetes t**oolkits**) are language-specific container images, that contain a (highly-opinionated) set of tools for debugging applications running in Kubernetes pods. You can read more about KoolKits [here](../README.md) or learn about the motivation behind this project [here](#Motivation).

To get started, first add the shorthand `kk` command to your shell by pasting the following snippet into your shell:

```bash
echo "## KoolKits - Shorthand
kk() {
	kubectl debug -it $1 --image=lightruncom/koolkits:$2 --image-pull-policy=Never --target=$3
}" >> ~/.bashrc
source ~/.bashrc
```

Then run the golang KoolKit with your pod:

```bash
kk <POD-NAME> golang <DEPLOYMENT-NAME>
```

The golang KoolKit contains the following golang utilities (available on `$PATH` wherever applicable):

* [`delve`](https://github.com/go-delve/delve) - Delve is a debugger for the Go programming language.
* [`pprof`](https://github.com/google/pprof) - pprof is a tool for visualization and analysis of profiling data.
* [`fzf`](https://github.com/junegunn/fzf) - fzf is a general-purpose command-line fuzzy finder.
* [`alp`](https://github.com/tkuchiki/alp) - Talp is Access Log Profiler.
* [`go-callvis`](https://github.com/ofabry/go-callvis) - go-callvis is a development tool to help visualize call graph of a Go program using interactive view.
* [`gvm`](https://github.com/moovweb/gvm) - GVM provides an interface to manage Go versions.

In addition, it contains the following utilities on top of the official [`ubuntu:20.04` image](https://hub.docker.com/layers/ubuntu/library/ubuntu/20.04/images/sha256-7c9c7fed23def3653a0da5bc9ecb651efe155ebd5802c7ba5d585edaa6c89496?context=explore):

```text
bird
calicoctl
conntrack
ctop
curl
dhcping
dnsutils
fping
gdb
htop
httpie
iftop
iperf
iproute2
ipset
iptraf-ng
iputils-ping
ipvsadm
iredis
jq
ldnsutils
liboping-dev
linux-tools-common
maven
mongo
mtr
mycli
mysql-client
netcat
netgen
nftables
ngrep
nmap
pgcli
postgresql-client
redis-tools
scapy
socat
software-properties-common
strace
tcpdump
tcptraceroute
termshark
tmux
tshark
unzip
vim
websocat
wuzz
zip
```