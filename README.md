# Broadcom Linux hybrid wireless driver 6.30.223.271

Set of patch for Broadcom wireless adapters

**Patched for Linux >= 4.15**

Tested on Fedora 33/35 Kernel 5.12.rc2 - 5.18.5

```bash
$ uname -r
5.12.0-rc2  # check your kernel version
```

With a Broadcom Inc. and subsidiaries **BCM4352** 802.11ac Wireless Network Adapter (rev 03)

```bash
$ lspci -nn | grep 14e4
03:00.0 Network controller [0280]: Broadcom Limited BCM4352 802.11ac Wireless Network Adapter [14e4:43b1] (rev 03)
```

## Compile and install

* ### Clone/Download this repo:

```bash
git clone https://github.com/hansyao/broadcom-wl.git
cd broadcom-wl/

dnf -y install kernel-devel kernel-headers

```

* ### Build and Install
```bash
$ make clean
$ make
$ make install
$ depmod -A
$ modprobe wl
```

The following kernel modules are incompatible with this driver and should not be loaded:
```bash
ssb
bcma
b43
brcmsmac
```
Make sure to unload (rmmod command) and blacklist those modules in order to prevent them from being automatically reloaded during the next system startup:

```bash
/etc/modprobe.d/blacklist.conf
```

wireless drivers (conflict with Broadcom hybrid wireless driver 'wl')
```bash
blacklist ssb
blacklist bcma
blacklist b43
blacklist brcmsmac
```

## See also

* [Official README file][1] (download)


[1]: https://docs.broadcom.com/docs-and-downloads/docs/linux_sta/README_6.30.223.271.txt