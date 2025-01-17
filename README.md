# Geode-linux-dnscrypt-proxy
AMD Geode specific build of dnscrypt-proxy 2.0.34-beta1 (maintainer provided i386 binaries fail due to use of SSE instructions)

Prerequisites: go (compiled with Geode specific flags) and git

Note: walkthrough to compile the linux Geode specific go version as well as binaries are [here](https://github.com/rhy-ama/Geode-linux-go)

Using [How to build dnscrypt-proxy](https://github.com/dnscrypt/dnscrypt-proxy/wiki/building-from-source) instructions :

1. Create your working directory

2. Clone the dnscrypt proxy repo
```
> mkdir dnscrypt-proxy-src
> cd dnscrypt-proxy-src
> git clone https://github.com/jedisct1/dnscrypt-proxy src
```

3. Set variables
```
export PATH=$PATH:$HOME/your_go_bin_directory (or PATH=$PATH:/the_fullpath)
export GOPATH=$PWD
export GOOS=linux
export GOARCH=386
export GO386=387
export CGO_ENABLED=0 
```

**The main issue with standard i386 binaries is the absence of **_GO386=387_** parameter that is needed to indicate lack of support for SSE processor instructions**

4. Compile
```
go clean
go build -ldflags="-s -w" -o $GOPATH/linux-i386-geode/dnscrypt-proxy
```

The resulting binary will be under /dnscrypt-proxy-src/src/dnscrypt-proxy/linux-i386-geode/

5. I would recommend to download the same package as the one we compiled (2.0.34-beta1 for your reference) and untar it to ```/opt/dnscrypt-proxy``` or similar, replace the binary and reset the permissions as required.

For your convinience and subject to all relevant legal terms, this repo has the binary in the /bin directory compiled 29/11/2019.

Note that dnscrypt-proxy is licensed under [these](https://github.com/DNSCrypt/dnscrypt-proxy/blob/master/LICENSE) terms and have the following copyright notice ``` Copyright (c) 2018 Frank Denis <j at pureftpd dot org>```

**Sources**

[How to build dnscrypt-proxy](https://github.com/dnscrypt/dnscrypt-proxy/wiki/building-from-source)
