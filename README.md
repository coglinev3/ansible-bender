# Ansible Role: ansible-bender

[![Build Status](https://travis-ci.org/coglinev3/ansible-bender.svg?branch=master)](https://travis-ci.org/coglinev3/ansible-bender)

This role installs [ansible-bender](https://github.com/TomasTomecek/ansible-bender),
a tool which bends containers using Ansible playbooks and turns them into
container images.

The supported Linux distribution are:
* Enterprise Linux 7[^newuidmap], 
* Enterprise Linux 8[^rootless], 
* Ubuntu 18.04 LTS (Bionic Beaver),
* Ubuntu 19.04 (Disco Dingo) and
* Ubuntu 19.10 (Eoan Ermine).


[^newuidmap]: The rootless mode for Podman requires the newuidmap and newgidmap
  programs to be installed. Note RHEL 7/CentOS 7 support this only since
  version 7.7.
[^rootless]: At the moment RHEL 8/CentOS 8 shipps with an old version of podman
  (see discussion on [RedHat Community](https://access.redhat.com/discussions/4288731 "RHEL 8.0 - latest version of Podman")).
  The old version of podman doesn't support [the rootless mode](https://github.com/containers/libpod#Rootless "rootless mode"). That's why you have to use podman with
  root under Enterprise Linux 8.

## Requirements

Ansible-bender requires a few binaries to be present on your host system:

* Podman
* Buildah
* Ansible (***Ansible needs to be built against python 3***)
* Python 3.6 or later (python 3.5 or earlier are not supported and known not to be working)

These requirements will be installed with this role.

## Role Variables

Available variables are listed below, along with default values
(see defaults/main.yml):

```yml

# dependencies for ansible-bender (like buildah, podman and python3.6 or higher)
ab_dependencies:
  - buildah
  - libffi-dev
  - libssl-dev
  - podman
  - python3
  - python3-setuptools
  - python3-pip
  - python3-virtualenv
  - procps
  - runc
  - slirp4netns
  - software-properties-common

# package state for dependencies: ( present ) | latest 
ab_dependencies_package_state: present

# Packages that are installed with the Python3 installer pip3.
ab_python_packges:
  - wheel
  - ansible
  - ansible-bender

# package state for python packages: ( present ) | latest
ab_python_packge_state: present


# comma separated list of container registries
ab_container_search_registry: "'docker.io', 'registry.fedoraproject.org', 'quay.io', 'registry.access.redhat.com', 'registry.centos.org'"

# a list of users which can use the rootless mode:
# (see https://github.com/containers/libpod#Rootless)
ab_users: []
```

## Dependencies

None.

## Example Playbook

```yml
---
# file: roles/ansible-bender/tests/test.yml

- hosts: all
  roles:
    - { role: coglinev3.ansible-bender }
```

## Version

Release: x.y.z

## License

BSD

## Author Information

This Ansible Role was created in 2019, by Cogline.v3.
