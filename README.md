# Firmware Builder

The firmware builder is a Makefile and a directory structure to create multiple
firmwares. It's meant to help you creating your own firmware. It's based on the
on https://github.com/freifunk-berlin/firmware but don't contain any freifunk
related changes. 

# Create your own firmware

A firmware based on:

- a LEDE commit on which your release is based (and a repository url) **config.mk**
- a collection of pre-installed packages E.g. tcpdump, foo **/packages**
- a collection of target device. E.g. tl-wdr4300 tl-wdr3600 **/profiles**
- (optional) a patchset **/patches**
- a config file per target **/configs**

## Build Prerequisites

Please take a look at the [OpenWrt documentation](http://wiki.openwrt.org/doc/howto/buildroot.exigence#examples.of.package.installations)
for a complete and uptodate list of packages for your operating system. Make
sure the list contains `quilt`. We use it for patch management.

On Ubuntu/Debian:
```
apt-get install git subversion build-essential libncurses5-dev zlib1g-dev gawk \
  unzip libxml-perl flex wget gawk libncurses5-dev gettext quilt python libssl-dev
```

On openSUSE:
```
zypper install --type pattern devel_basis
zypper install git subversion ncurses-devel zlib-devel gawk \
  unzip perl-libxml-perl flex wget gawk gettext-runtime quilt python libopenssl-devel
```

# How does this work?

 * git clone LEDE
 * update feeds from **feeds.conf**
 * apply **/patches**
 * cat **configs/common.config** **config/ar71xx.config** > lede/.config
 * compile the target including CONFIG\_IB which required for a successful firmware
 * use /bin/targets/ar71xx/lede-imagebuilder\*.tar.gz
 * use imagebuilder with **/profiles** and **/packages** to get multiple firmware images
 
