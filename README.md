# Ansible VXLAN Notes

This repo provides a basic VXLAN spine/leaf configuration using Ansible and Cisco Nexus 9000 switches

[If you're viewing this through CML and the images don't appear, the lab notes can also be found here](https://github.com/conmurphy/ansible-basic-vxlan-evpn-nexus9000)

## Table of Contents
- [Devices, Interfaces, and Addresses](#devices-interfaces-and-addresses)
- [Directory and File Structure](#directory-and-file-structure)
- [Building And Destroying The Lab](#building-and-destroying-the-lab)
- [Verification and Troubleshooting Playbook](#verification-and-troubleshooting-playbook)

## Devices, Interfaces, and Addresses

<img src="https://github.com/conmurphy/ansible-basic-vxlan-evpn-nexus9000/blob/main/images/vxlan-lab-topology.png?raw=true" alt="Lab Topology" />


<img src="https://github.com/conmurphy/ansible-basic-vxlan-evpn-nexus9000/blob/main/images/management-lab-topology.png?raw=true" alt="Management Topology" />

## Directory and File Structure

<img src="https://github.com/conmurphy/ansible-basic-vxlan-evpn-nexus9000/blob/main/images/directory.png?raw=true" alt="Directory and file structure" />

### Ansible configuration

An `ansible.cfg` file is available in the root directory of the repo and is configured with the following settings:

- `force_color=True`
- `[colors]` 

## Building and Destroying The Lab

There is an Ansible Playbook, `configure_vxlan.yml`, which you can use to configure VXLAN on the two spine and two leaf switches.

`ansible-playbook -i hosts.yml configure_vxlan.yml`

To reset the environent use the `delete_vxlan_configuration.yml` playbook.

`ansible-playbook -i hosts.yml delete_vxlan_configuration.yml`

## Verification and Troubleshooting Playbook

There is an Ansible Playbook to verifiy and troubleshoot the environment. The tasks run show commands against the spine and leaf switches as well as pinging between hosts in the same VNI and between VNIs.

The following example runs all tasks against all devices which may be too much detail. Therefore, it's recommended to filter the output using the tags below. 

`ansible-playbook -i hosts troubleshooting_commands.yml`

### Optional Tags

The following tags are available to filter the output of the troubleshooting playbook. Additionally you can `limit` the hosts.

- mgmt
- control
- underlay
- multicast
- overlay
- l2vni
- l3vni
- ping

`ansible-playbook -i hosts troubleshooting_commands.yml --extra-vars "tag=ping"`

`ansible-playbook -i hosts troubleshooting_commands.yml --limit leaf -e "tag=l2vni"`
