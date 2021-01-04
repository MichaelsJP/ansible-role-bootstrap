MichaelsJP ansible-role-bootstrap
=========
![Build](https://github.com/MichaelsJP/ansible-role-bootstrap/workflows/Ansible%20Role%20Bootstrap%20Build/badge.svg)

- [MichaelsJP ansible-role-bootstrap](#michaelsjp-ansible-role-bootstrap)
    * [Introduction](#introduction)
    * [Requirements](#requirements)
    * [Role Tags](#role-tags)
    * [Role Variables](#role-variables)
    * [Dependencies](#dependencies)
    * [Example Playbook](#example-playbook)
    * [License](#license)
    * [Author Information](#author-information)

Introduction
------------
**Important:** Only used to provision ubuntu and debian for now.

This role bootstraps basic resources.

Important bootstrap results:

```text
- Base requirements. Mainly for debian and ubuntu. # See _bootstrap_packages in vars/main.yml
```

OS packages installed:

```text
- Debian: python3 sudo gnupg python3-apt git curl htop nload openssh-server vim gpg python3-setuptools python3-pip python3-setuptools cron dnsutils build-essential
- Ubuntu: python-apt python3 sudo gnupg python3-apt git curl htop nload openssh-server vim gnupg python3-setuptools python3-pip python-setuptools cron dnsutils build-essential python3-dev python3-wheel python-pip-whl
- Debian_9: python-apt python3 sudo gnupg python3-apt git curl htop nload openssh-server vim gpg python3-setuptools python3-pip python-setuptools python-pip cron dnsutils build-essential
- Debian_10: python3 sudo gnupg python3-apt git curl htop nload openssh-server vim gpg python3-setuptools python3-pip python3-setuptools cron dnsutils build-essential
- Debian_11: python3 sudo gnupg python3-apt git curl htop nload openssh-server vim gpg python3-setuptools python3-pip python3-setuptools cron dnsutils build-essential
```

Optional bootstrap results:

```text
- Hetzner debian setup. Automates network setup of vms.
- Hetzner facts cache. Facts from Hetzner are cached if needed. For the exact facts variables see below.
```

Cacheable Hetzner Facts:

```text
- HETZNER_FACT_BACKUP_WINDOW
- HETZNER_FACT_DATACENTER
- HETZNER_FACT_SERVER_ID
- HETZNER_FACT_ipv4
- HETZNER_FACT_ipv6
- HETZNER_FACT_LABELS
- HETZNER_FACT_LOCATION
- HETZNER_FACT_SERVER_NAME
- HETZNER_FACT_RECUE_ENABLED
- HETZNER_FACT_SERVER_TYPE
- HETZNER_FACT_STATUS
```

**Important:** For explanations
see: https://docs.ansible.com/ansible/latest/collections/hetzner/hcloud/hcloud_server_module.html

Requirements
------------
**None in default run.**

When hetzner facts should be gathered you need to define `hetzner.hcloud` in your `collection requirements.yml`.

Role Tags
--------------
The base installer is always executed. It needs to be to server the correct base to install the rest.

```shell
- bootstrap_ipv6 # Run the ipv6 bootstrap
- bootstrap_hetzner_utils # Run the hetzner .deb network install
- bootstrap_pip # Install python dependencies
- bootstrap_hetzner_facts # Make hetzner server facts available
```

Role Variables
--------------

```yaml
---
# Hetzner utils version
bootstrap_hc_utils_version: "0.0.3-1_all"

# The user to use to connect to machines.
bootstrap_user: root

# Do you want to wait for the host to be available?
bootstrap_wait_for_host: no

HCLOUD_TOKEN: [ ]

# Define additional packages to be bootstrapped. Debian and Ubuntu have to be present!
# You have to take care yourself that the os versions have the corresponding package in the default apt sources.
# Define the packages like "nload htop git"
additional_bootstrap_packages:
  Debian_11: ""
  Debian_10: ""
  Debian_9: ""
  Debian: ""
  Ubuntu: ""

# Define additional pip packages to be installed. They'll be installed with pip3!
# Define the packages like "bpytop molecule"
additional_bootstrap_pip_packages: ""
```

Dependencies
------------

```shell
- `hetzner.hcloud` # Is only needed if Hetzner facts should be gathered. Else ignore it.
- `setuptools` # Installed with pip.
- `hcloud` # Installed with pip when needed.
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for
users too:

    - hosts: servers
      gather_facts: false
      roles:
      - { role: michaelsjp.ansible_role_bootstrap }

License
-------

Apache-2.0

Based on:

```text
- https://github.com/robertdebock/ansible-role-bootstrap
```

Author Information
------------------

[Julian Psotta](https://github.com/MichaelsJP)
