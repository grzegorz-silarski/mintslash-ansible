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