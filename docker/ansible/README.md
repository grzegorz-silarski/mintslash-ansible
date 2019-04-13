# Docker likes Ansible

## Docker commands for Ansible

Open a terminal window and execute one of the following commands to run Ansible container with a volume added in current directory.

Bash:

```text
docker run --rm -it --workdir /ansible -v $(pwd):/ansible willhallonline/ansible:2.7 /bin/sh
```

PowerShell:

```text
docker run --rm -it --workdir /ansible -v ${PWD}:/ansible willhallonline/ansible:2.7 /bin/sh
```

## Ansible commands

Checking ansible version:

```text
ansible --version
```

## CentOS static IP configuration

```text
cd /etc/sys_config/network-scripts/
vi <network_interface_name>
```

```text
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=eth1
UUID=66abf7dd-0cde-4c87-a8ad-0db463737589
DEVICE=eth1
ONBOOT=yes
IPADDR=192.168.56.100
PREFIX=24
IPV6_PRIVACY=no
```