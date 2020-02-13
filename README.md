# nephelaiio.playbooks-kvm

[![Build Status](https://travis-ci.org/nephelaiio/ansible-playbooks-kvm.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-playbooks-kvm)

A set of ansible playbooks to install KVM hosts and guests

## Playbook descriptions

The following lists the group targets and descriptions for every playbook

| playbook   | description          | target     | supported os                    |
| ---        | ---                  | ---        | ---                             |
| hosts.yml  | configure a kvm host | kvm_hosts  | Ubuntu Bionic                   |
| guests.yml | provision kvm guests | kvm_guests | Ubuntu Xenial/Bionic, CentOS7/8 |

## Requirements

Hosts need to be pre-configured with ip-reachable bridge interfaces for kvm guest placement

## Playbook variables

The following parameters are available/required for playbook invocation

### [hosts.yml](hosts.yml): N/A

### [guests.yml](guests.yml):

| required    | variable        | description                                           | default                                                                                          |
| ---         | ---             | ---                                                   | ---                                                                                              |
| *yes* (1)__ | kvm_networks    | global list of networks availeble for guest placement | see [roles/nephelaiio.kvm_guest/defaults/main.yml](roles/nephelaiio.kvm_guest/defaults/main.yml) |
| *yes* (1)__ | kvm_network     | network for particular guest placement                | see [roles/nephelaiio.kvm_guest/defaults/main.yml](roles/nephelaiio.kvm_guest/defaults/main.yml) |
| no _        | ansible_host    | guest address                                         | N/A (must be set to static ip or kvm_dhcp='yes' is required)                                     |
| no          | kvm_dhcp        | dhcp assignment for particular guest                  | no (must be set to true or ansible_host=<static ip> is required)                                 |
| no          | kvm_base_domain | base domain for kvm guests save                       | domain name from `inventory_hostname`                                                            |
| no          | kvm_profiles    | hardware profiles for kvm guests                      | see [roles/nephelaiio.kvm_guest/defaults/main.yml](roles/nephelaiio.kvm_guest/defaults/main.yml) |

(1) defaults are provided for local demo purposes. I.e set up br0 with a dummy interface

## Dependencies

This playbook has the following role dependencies by play (no dependencies if play is not listed):

### [hosts.yml](hosts.yml):
* [nephelaiio.plugins](https://galaxy.ansible.com/nephelaiio/plugins)

### [guests.yml](guests.yml):
* [nephelaiio.plugins](https://galaxy.ansible.com/nephelaiio/plugins)

See the [requirements](roles/requirements.yml) file for more details

## Example Usage

Assuming your inventory is available at path ``inventory`` you can execute all playbooks from the command line with

```
git checkout https://github.com/nephelaiio/ansible-playbooks-kvm kvm
ansible-playbook -i inventory/ kvm/hosts.yml kvm/guests.yml
```

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
