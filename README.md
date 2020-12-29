MichaelsJP ansible-role-bootstrap
=========

**Important:** Only used to provision ubuntu and debian for now.

This role bootstraps basic resources.
It is heavily based on the following roles:

```text
- https://github.com/robertdebock/ansible-role-rsyslog
- https://github.com/robertdebock/ansible-role-bootstrap
```

Important bootstrap results:

```text
- Base requirements. Mainly for debian and ubuntu. # See _bootstrap_packages in vars/main.yml
- Hetzner debian setup. Automates network setup of vms.
- Hetzner facts cache. Facts from Hetzner are cached if needed. For the exact facts variables see below.
- Custom Rsyslog integration
- IPTABLES integration with rsyslog. Logging goes into /var/logs/iptables.log.
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
Only Ubuntu and Debian for now.

Role Tags
--------------
The base installer is always executed. It needs to be to server the correct base to install the rest.

```shell
- bootstrap_ipv6 # Run the ipv6 bootstrap
- bootstrap_hetzner_utils # Run the hetzner .deb network install
- bootstrap_pip # Install python dependencies
- bootstrap_rsyslog # Install Rsyslog and iptables logging file
- bootstrap_hetzner_facts # Make hetzner server facts available
```

Role Variables
--------------

```shell
- bootstrap_hc_utils_version # Set hetzner util default
- bootstrap_user # default user to run the role
- bootstrap_wait_for_host # Decide if ansible should wait for the host
- bootstrap_timeout # Set custom timeout
- HCLOUD_TOKEN # Set HETZNER Key to provision hetzner facts
```

Dependencies
------------

```shell
- hetzner.hcloud # Collection is installed via meta/main.yml.
- `setuptools` # Installed with pip.
- `hcloud` # Installed with pip.
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for
users too:

    - hosts: servers
      gather_facts: false
      roles:
      - { role: ansible-role-bootstrap }

License
-------

Apache-2.0

Based on:

```text
- https://github.com/robertdebock/ansible-role-rsyslog
- https://github.com/robertdebock/ansible-role-bootstrap
```

Author Information
------------------

[Julian Psotta](https://github.com/MichaelsJP)
