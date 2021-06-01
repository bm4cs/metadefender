
# Core

1. Download distribution from [OPSWAT portal](https://portal.opswat.com/products/metadefender-core)
2. Place a copy of the `rpm` installer in `core/src`
3. Install [pre-requistites](https://onlinehelp.opswat.com/corev4/2.1._Recommended_System_Configuration.html)

In the `core` directory:

```
docker build . -t md-core
docker run --name md-core -it --entrypoint /bin/bash --rm md-core:latest
```

# Troubleshooting (WIP)

To debug the container interactively:

```
docker run --name md-core -it --entrypoint /bin/bash --rm md-core:latest
```

Dump the contents of the provided installer:

```
rpm -qlp ometascan-4.20.1-1.x86_64.rpm
```

The rpm installer bundles in an init script `/etc/init.d/ometascan`, which gives some clues how to run the binary:

```
daemon --user $USER --pidfile $PIDFILE $DAEMON $DAEMON_OPTS &
# USER=metascan PIDFILE=/var/run/ometascan/ometascan.pid DAEMON=/usr/sbin/ometascan DAEMON_OPTS=""
```

Lots of dependencies are needed, including postgresql:

```
[root@29a4cbc95bed opswat]# rpm --install --quiet ometascan-4.20.1-1.x86_64.rpm 
error: Failed dependencies:
	ld-linux.so.2 is needed by ometascan-4.20.1-1.x86_64
	ld-linux.so.2(GLIBC_2.3) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6 is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.0) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.1) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.1.2) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.1.3) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.10) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.2) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.2.4) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.3) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.3.2) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.3.4) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.4) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.7) is needed by ometascan-4.20.1-1.x86_64
	libc.so.6(GLIBC_2.9) is needed by ometascan-4.20.1-1.x86_64
	libdl.so.2 is needed by ometascan-4.20.1-1.x86_64
	libdl.so.2(GLIBC_2.0) is needed by ometascan-4.20.1-1.x86_64
	libdl.so.2(GLIBC_2.1) is needed by ometascan-4.20.1-1.x86_64
	libecpg.so.6()(64bit) is needed by ometascan-4.20.1-1.x86_64
	libecpg_compat.so.3()(64bit) is needed by ometascan-4.20.1-1.x86_64
	libgcc_s.so.1 is needed by ometascan-4.20.1-1.x86_64
	libgcc_s.so.1(GCC_3.0) is needed by ometascan-4.20.1-1.x86_64
	libgcc_s.so.1(GCC_3.4) is needed by ometascan-4.20.1-1.x86_64
	libgcc_s.so.1(GLIBC_2.0) is needed by ometascan-4.20.1-1.x86_64
	libm.so.6 is needed by ometascan-4.20.1-1.x86_64
	libm.so.6(GLIBC_2.0) is needed by ometascan-4.20.1-1.x86_64
	libm.so.6(GLIBC_2.1) is needed by ometascan-4.20.1-1.x86_64
	libpgtypes.so.3()(64bit) is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0 is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0(GLIBC_2.0) is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0(GLIBC_2.1) is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0(GLIBC_2.2) is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0(GLIBC_2.3.2) is needed by ometascan-4.20.1-1.x86_64
	libpthread.so.0(GLIBC_2.3.3) is needed by ometascan-4.20.1-1.x86_64
	librt.so.1 is needed by ometascan-4.20.1-1.x86_64
	librt.so.1(GLIBC_2.2) is needed by ometascan-4.20.1-1.x86_64
	libstdc++(x86-32) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6 is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(CXXABI_1.3) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(GLIBCXX_3.4) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(GLIBCXX_3.4.10) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(GLIBCXX_3.4.11) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(GLIBCXX_3.4.14) is needed by ometascan-4.20.1-1.x86_64
	libstdc++.so.6(GLIBCXX_3.4.9) is needed by ometascan-4.20.1-1.x86_64
	openssl is needed by ometascan-4.20.1-1.x86_64
```

Dependency install list:

```
yum -y install glibc libpq openssl libstdc++ libgcc
```


