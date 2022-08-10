# Ansible VXLAN Notes

## Table of Contents
- [Devices, Interfaces, and Addresses](#devices-interfaces-and-addresses)
- [Directory and File Structure](#directory-and-file-structure)
- [Building The Lab](#building-the-lab)
- [Verification and Troubleshooting Playbook](#verification-and-troubleshooting-playbook)

## Devices, Interfaces, and Addresses

<img src="https://github.com/conmurphy/ansible-basic-vxlan-evpn-nexus9000/blob/main/images/topology.png?raw=true" alt="Lab Topology" />

## Directory and File Structure

## Setup configuration

Proxy

An `ansible.cfg` is available in the root directory of the repo and is configured with the following settings:

- `force_color=True`
- `[colors]` 

## Building The Lab


## Verification and Troubleshooting Playbook

### Optional Tags

The following tags are available to filter the output of the troubleshooting playbook. Additionally you can `limit` the hosts.

- mgmt
- control
- underlay
- multicast
- overlay
- l2vni
- l3vni

`ansible-playbook -i hosts troubleshooting_commands.yml --extra-vars "tag=l2vni"`

`ansible-playbook -i hosts troubleshooting_commands.yml --limit leaf-1 -e "tag=l2vni"`
