# Ansible roles for Batfish

Intentionet has created this Ansible role to allow users to embed pre-deployment validation into any Ansible playbook. This role is hosted on Ansible Galaxy as `batfish.base`. The role includes a set of Ansible modules that analyze configuration files for an entire (or subset of a) network, allowing users to extract configuration data and perform network-wide validation tests in a completely vendor agnostic manner.

## Overview of Modules

**bf_session** - Setup the connection to the server running Batfish or Batfish Enterprise

**bf_init_snapshot** - Initialize a network snapshot

**bf_extract_facts** - Retrieve configuration facts for devices in the snapshot

**bf_validate_facts** - Validate configuration facts for devices in the snapshot

**bf_assert** - Validate network behavior

## Documentation
Ansible module documentation can be found at https://docs.ansible.com by searching for Batfish.

## Examples
This example playbook outlines how to use the `batfish.base` role to extract the list of interfaces for all devices in the network.

```yaml
---
- name: Extract network device facts using Batfish and Ansible
  hosts: localhost
  connection: local
  gather_facts: no
  roles:
    - batfish.base

  tasks:

  - name: Setup connection to Batfish service
    bf_session:
      host: localhost
      name: local_batfish
  
  - name: Initialize the example network
    bf_init_snapshot:
      network: example_network
      snapshot: example_snapshot
      snapshot_data: ../networks/example
      overwrite: true

  - name: Retrieve Batfish Facts
    bf_extract_facts:
      output_directory: data/bf_facts
    register: bf_facts
```

For additional examples and a step-by-step tutorial of the Batfish Ansible role, please visit the [Batfish Ansible Utilities and Playbooks](https://github.com/batfish/ansible-utils) repository

## Installation  
You must have the [Dependencies](#dependencies) installed on the system before you can use the role.

### Ansible Galaxy Role
To download the latest released version of the Batfish role to the Ansible server, execute the ansible-galaxy install command, and specify batfish.base

```
ansible-galaxy install batfish.base
```

## Dependencies

This module requires the following packages to be installed on the Ansible control machine:

- Python >= 2.7
- Ansible 2.7 or later
- Pybatfish >= 0.36
- PyYAML >= 3.10

## License
Apache 2.0

## Support
Support for this role is provided by the community and Intentionet. If you have an issue with a module in this role, you may:

- Open a Github issue
- Post a question on our Slack Group

## Contributors
Intentionet is actively contributing to and maintaining this repository.
