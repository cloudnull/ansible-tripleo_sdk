# Software Development Kit for TripleO Developers

This Ansible role will setup an environment suited for TripleO development.
The role will apply patches and build packages as required or instructed,
which automates the hassle of most of the development tasks required to
effectively contribute to TripleO.

### Role Overview

* Repository installation, used to ensure relevant packages are available
  within the development environment.
* Package building using git checkouts or upstream gerrit reviews.
* The setup of a molecule test running environment with podman and/or docker.

## Role Installation

Installing the role is simple and can be expressed in a single command

``` shell
ansible-galaxy install --force git+https://github.com/cloudnull/ansible-role-tripleo_sdk,master,tripleo_sdk
```

This role can also be installed using a role requirements file.

``` yaml
- src: https://github.com/cloudnull/ansible-role-tripleo_sdk
  version: master
  name: tripleo_sdk
```

### Options

Please review the [defaults/main.yml](defaults/main.yml) file for all documented overrides for
this role.
