[![Build Status](https://travis-ci.org/AdguardTeam/dnscrypt-proxy-static.png?branch=master)](https://travis-ci.org/AdguardTeam/dnscrypt-proxy-static?branch=master)

dnscrypt-proxy-static
---------------------

This is a fork of dnscrypt-proxy with libsodium source code bundled in, removing the need to compile it separately when cross-compiling dnscrypt-proxy for android and other platforms.

Android compile instructions
============================

First things first, download Android NDK from [here](https://developer.android.com/ndk/downloads/index.html) and unpack it somewhere. I'll assume you unpacked it into `$HOME/android-ndk-r14b`.

You will also need autoconf, automake, libtool and pkg-config to run autoreconf.

```bash
git clone https://github.com/AdguardTeam/dnscrypt-proxy-static
cd dnscrypt-proxy-static
export ANDROID_NDK_HOME=$HOME/android-ndk-r14b ## location of android NDK
autoreconf -f -i -v
dist-build/android-arm.sh
dist-build/android-armv7-a.sh
dist-build/android-armv8-a.sh
dist-build/android-mips32.sh
dist-build/android-mips64.sh
dist-build/android-x86.sh
dist-build/android-x86-64.sh
```

After everything compiles, there will be .zip files for each android architecture in current directory.

#### Original readme is kept below to avoid merge conflicts with upstream ####

---------------

[![DNSCrypt](https://raw.github.com/jedisct1/dnscrypt-proxy/master/dnscrypt-small.png)](https://dnscrypt.org)
============

DNSCrypt is a protocol for securing communications between a client
and a DNS resolver, using high-speed high-security elliptic-curve
cryptography.

While not providing end-to-end security, it protects the local network, which
is often the weakest point of the chain, against man-in-the-middle attacks.

`dnscrypt-proxy` is a client-implementation of the protocol. It
requires a [DNSCrypt server](https://www.dnscrypt.org/#dnscrypt-server) on
the other end.

Online documentation
--------------------

* [dnscrypt-proxy documentation](https://github.com/jedisct1/dnscrypt-proxy/wiki/)
* [dnscrypt website](https://dnscrypt.org).

Download and integrity check
----------------------------

dnscrypt-proxy can be downloaded here:
[dnscrypt-proxy download](https://download.dnscrypt.org/dnscrypt-proxy/).

Signatures can be verified with [Minisign](https://jedisct1.github.io/minisign/):

    $ minisign -VP RWQf6LRCGA9i53mlYecO4IzT51TGPpvWucNSCh1CBM0QTaLn73Y7GFO3 -m dnscrypt-proxy-1.9.5.tar.bz2

Plugins
-------

Aside from implementing the protocol, dnscrypt-proxy can be extended
with plug-ins, and gives a lot of control on the local DNS traffic:

- Review the DNS traffic originating from your network in real time,
and detect compromised hosts and applications phoning home.
- Locally block ads, trackers, malware, spam, and any website whose
domain names or IP addresses match a set of rules you define.
- Prevent queries for local zones from being leaked.
- Reduce latency by caching resposes and avoiding requesting IPv6
addresses on IPv4-only networks.
- Force traffic to use TCP, to route it through TCP-only tunnels or
Tor.
