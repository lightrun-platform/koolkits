## Node.js KoolKit

<img src="./node-logo.png" style="max-width:20%;" />

KoolKits (**K**ubernetes t**oolkits**) are language-specific container images, that contain a (highly-opjnionated) set of tools for debugging applications running in Kubernetes pods. You can read more about KoolKits [here](../README.md) or learn about the motivation behind this project [here](#Motivation).

Using the Node.js KoolKit you can spin up `0x` for fancy flamegraphs or `ndb` for debugging your app your Kubernetes pods without any configuration or extra setup.

To get started, first add the shorthand `kk` command to your shell by pasting the following snippet into your shell:

```bash
echo "## KoolKits - Shorthand
kk() {
	kubectl debug -it $1 --image=lightruncom/koolkits:$2 --image-pull-policy=Never --target=$3
}" >> ~/.bashrc
source ~/.bashrc
```

Then run the Node.js KoolKit with your pod:

```bash
kk <POD-NAME> node <DEPLOYMENT-NAME>
```

The Node.js KoolKit contains the following Node utilities  (available on `$PATH` wherever applicable):

* [`nvm`](https://github.com/nvm-sh/nvm) - A Node version manager, with [Node 16.13.2](https://github.com/nodejs/node/blob/master/doc/changelogs/CHANGELOG_V16.md#16.13.2) installed as the default Node version.
* [`ndb`](https://github.com/GoogleChromeLabs/ndb) - An improved debugging experience for Node.js, enabled by Chrome DevTools.
* [`0x`](https://github.com/davidmarkclements/0x) - Single-command flamegraph profiling.
* [`vtop`](https://github.com/MrRio/vtop) - A graphical activity monitor for the command line. `top`, but better.
* [`whistle`](https://github.com/avwo/whistle)  - A cross-platform web debugging tool based on Node.js (mostly a debugging proxy).

In addition, it contains the following utilities on top of the official [`ubuntu:20.04` image](https://hub.docker.com/layers/ubuntu/library/ubuntu/20.04/images/sha256-7c9c7fed23def3653a0da5bc9ecb651efe155ebd5802c7ba5d585edaa6c89496?context=explore):

```
bird
conntrack
calicoctl
ctop
curl
dhcping
dnsutils
fping
gdb
git
htop
httpie
iftop
iperf
ipset
iptraf-ng
iproute2
iputils-ping
ipvsadm
jq
ldnsutils
liboping-dev
linux-tools-common
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
vim
websocat
wuzz
```
