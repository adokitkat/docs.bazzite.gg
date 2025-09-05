---
title: "ZeroTier setup"
authors:
  - "@Zeglius"
  - "@adokitkat"
---

!!! warning
    Setup requires **layering** and is [not recommended](/Installing_and_Managing_Software/rpm-ostree/#major-caveats-using-rpm-ostree).

## Installing

Add ZeroTier repository to yum by copying the following to the terminal (pasting is <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>V</kbd>)

```sh
sudo tee >/dev/null /etc/yum.repos.d/zerotier.repo <<'EOF'
[zerotier]
name=ZeroTier, Inc. RPM Release Repository
baseurl=https://download.zerotier.com/redhat/fc/$releasever
enabled=1
gpgcheck=1
gpgkey=https://download.zerotier.com/contact@zerotier.com.gpg
EOF
```

Install ZeroTier One:

```sh
sudo rpm-ostree install zerotier-one
```

Reboot the system, and then enable ZeroTier service by running this command in the terminal:

```sh
sudo systemctl enable --now zerotier-one
```

## Uninstalling

Select, copy and paste the following to the terminal (pasting is <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>V</kbd>)

```sh
sudo systemctl disable zerotier-one.service
sudo rpm-ostree uninstall zerotier-one
```

Reboot, and run this at the terminal:

```sh
sudo rm -fv /etc/yum.repos.d/zerotier.repo
```

## Fix not seeing your teammates in games (set routing through the ZeroTier network interface)

Get your ZeroTier network interface name by running: `ifconfig -a` (compare the IP address to one in your ZeroTier web dashboard)

Add the route: `sudo route add -host 255.255.255.255 dev <interface name>`
