# Ansible Role: EMUX ([Ludus](https://ludus.cloud))

An Ansible Role that installs [EMUX](https://emux.exploitlab.net/) (formerly ARMX) and runs an emulated device on Debian based hosts.

The following ports are mapped to the emulated device:

```
Host Port:Emulated Device Port
23:23
80:80
443:443
2222:22
8080:8080
4433:4433
9999:9999
```

Note: Port 22 will SSH into the host, not the emulated device. Use port 2222 for SSH to the emulated device (assuming the device has SSH listening on port 22).
As ports 80 and 443 are mapped to the emulated device, this host should not be used for anything except running this role.

## Requirements

A Debian based OS.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ludus_emux_path: /opt/emux
    ludus_emux_device: 4 # See below for the devices
    ludus_emux_devices_map: # DO NOT MODIFY THIS VAR
      0: DV-ARM     # Damn Vulnerable ARM Router
      1: DV-MIPSEL  # Damn Vulnerable MIPS Router (Little Endian)
      2: DV-MIPSEB  # Damn Vulnerable MIPS Router (Big Endian)
      3: PH0WNCTF   # R0 Port Controller - Ph0wn 2021 CTF Challenge
      4: TRI227WF   # Trivision NC-227-WF IP Camera
      5: AC15       # Tenda AC15 Wi-Fi Router
      6: ARCHERC9   # Archer C9 Wi-Fi Router
      7: DIR615C    # D-Link DIR615C Wi-Fi Router
      8: DCS935L    # D-Link DCS-935L Camera

These options mirror the "Launcher" from EMUX

![EMUX Launcher](/imgs/emux_launcher.jpeg "EMUX Launcher")

## Dependencies

[geerlingguy.docker](https://github.com/geerlingguy/ansible-role-docker)

## Example Playbook

```yaml
- hosts: emux_hosts
  roles:
    - badsectorlabs.ludus_emux
  vars:
    ludus_emux_device: 0
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-EMUX"
    hostname: "{{ range_id }}-emux"
    template: debian-12-x64-server-template
    vlan: 10
    ip_last_octet: 1
    ram_gb: 4
    cpus: 2
    linux: true
    roles:
      - badsectorlabs.ludus_emux
    role_vars:
      ludus_emux_device: 0
```

## License

MPLv2

## Author Information

This role was created by [Bad Sector Labs](https://github.com/badsectorlabs), for [Ludus](https://ludus.cloud/).
