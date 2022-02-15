## JVM KoolKit

<img src="./java-logo.png" style="max-width:20%;" />

KoolKits (**K**ubernetes t**oolkits**) are language-specific container images, that contain a (highly-opjnionated) set of tools for debugging applications running in Kubernetes pods. You can read more about KoolKits [here](../README.md) or learn about the motivation behind this project [here](#Motivation).

Using the JVM KoolKit you can use `async-profiler`,`jmxterm` or VisualVM with any JVM running inside your Kubernetes pods, without any extra configuration or setup.

To get started, first add the shorthand `kk` command to your shell by pasting the following snippet into your shell:

```bash
echo "## KoolKits - Shorthand
kk() {
	kubectl debug -it $1 --image=lightruncom/koolkits:$2 --image-pull-policy=Never --target=$3
}" >> ~/.bashrc
source ~/.bashrc
```

Then run the JVM KoolKit with your pod:

```bash
kk <POD-NAME> jvm <DEPLOYMENT-NAME>
```

The JVM KoolKit contains the following Java utilities (available on `$PATH` wherever applicable):

* [`sdk`](https://sdkman.io/) - SDKMAN!, A JVM version manager (and extras!) with [Adoptium Temurin (AdoptOpenJDK) 17.0.2](https://adoptium.net/?variant=openjdk17&jvmVariant=hotspot) - installed as the default JDK.
* [`jmxterm`](https://github.com/jiaqi/jmxterm) - Interactive command-line JMX client.
* [`honest-profiler`](https://github.com/jvm-profiling-tools/honest-profiler) - A sampling JVM profiler without the safepoint sample bias.
* [`jmxtrans`](https://github.com/jmxtrans/jmxtrans) - The missing connector between speaking to a JVM via JMX on one end and whatever logging / monitoring / graphing package that you can dream up on the other end.
* [`async-profiler`](https://github.com/jvm-profiling-tools/async-profiler) - Sampling CPU and HEAP profiler for Java featuring `AsyncGetCallTrace` + `perf_events`.
* [`VisualVM`](https://visualvm.github.io/) (CLI) - A profiler that bundles up a combination of JDK command line tools.
* [`Maven`](https://maven.apache.org/index.html) - The default build tool for the JVM world.

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
ipset
iptraf-ng
iproute2
iputils-ping
ipvsadm
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