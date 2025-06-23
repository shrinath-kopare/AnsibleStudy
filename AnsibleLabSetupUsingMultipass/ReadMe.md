# Ansible Lab Setup Using Multipass

This document describes how to automate the creation of Ubuntu VMs for an Ansible lab environment using Multipass and Ansible.

---

## Overview

You can use the provided Ansible playbook to launch multiple Ubuntu VMs locally with Multipass. This is useful for quickly setting up a test environment for Ansible playbooks and roles.

---

## Prerequisites

- **Multipass** installed on your machine ([installation guide](https://multipass.run/docs/installing-on-macos))
- **Ansible** installed (`pip install ansible`)
- macOS, Linux, or Windows with WSL

---

## Playbook: `launch_multipass_vms.yaml`

This playbook launches a configurable number of Ubuntu VMs using Multipass.

### Example Content

```yaml
- name: Launch 3 local VMs using Multipass
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
    vm_count: 2
    base_name: "ansible-vm"
    image: 22.04
    memory: 1G
    disk: 3G
    cpus: 1

  tasks:
    - name: Launch Multipass VMs
      ansible.builtin.command: >
        multipass launch {{ image }}
        --name {{ base_name }}-{{ item }}
        --memory {{ memory }} --disk {{ disk }} --cpus {{ cpus }}
      loop: "{{ range(1, vm_count + 1) | list }}"