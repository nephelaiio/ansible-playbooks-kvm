# nephelaiio.playbooks-kvm

[![Build Status](https://travis-ci.org/nephelaiio/ansible-playbooks-kvm.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-playbooks-kvm)

A set of ansible playbooks to install KVM hosts and guests

## Playbook descriptions

The following lists the group targets and descriptions for every playbook

| playbook   | description          | target     |
| ---        | ---                  | ---        |
| hosts.yml  | configure a kvm host | kvm_hosts  |
| guests.yml | provision kvm guests | kvm_guests |

## Playbook variables

The following parameters are available/required for playbook invocation

### [hosts.yml](hosts.yml):
| required | variable    | description        | default |
| ---      | ---         | ---                | ---     |
| no       | kvm_release | target awx release | '8.0.0' |

### [guests.yml](guests.yml):
| required | variable          | description                                  | default |

## Data Formats

### Users
```{yaml}
awx_users:
  - first_name: First Name
    last_name: Last Name
    username: testuser
    password: supersecret
    superuser: yes
```

### Templates
```{yaml}
awx_templates:
  - name: ping
    state: absent
    job_type: run
    project: awx
    inventory: awx
    playbook: ping.yml
    credentials:
      - name: awx.ssh
        kind: ssh
```

## Dependencies

This playbook has the following role dependencies by play (no dependencies if play is not listed):

### [hosts.yml](hosts.yml):
* [nephelaiio.plugins](https://galaxy.ansible.com/nephelaiio/plugins)

### [guests.yml](guests.yml):
* [nephelaiio.plugins](https://galaxy.ansible.com/nephelaiio/plugins)

See the [requirements](requirements.yml) file for more details

## Example Usage

Assuming your inventory is available at path ``/inventory`` you can execute all playbooks from the command line with

```
git checkout https://github.com/nephelaiio/ansible-playbooks-kvm kvm
ansible-playbook -i inventory/ kvm/hosts.yml kvm/guests.yml
```

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
