# ansible-role-iptables

Ansible role for deploying the iptables and ip6tables firewall

## How to install
### requirements.yml
**Put the file in your roles directory**
```yaml
---
- src: https://github.com/mohsenmirzaei1991/ansible-role-iptables.git
  scm: git
  version: main
  name: ansible-role-iptables
```
### Download the role
```Shell
ansible-galaxy install -f -r ./roles/requirements.yml --roles-path=./roles
```

## Requirements

- Ansible >= 2.9 **(No tests has been realized before this version)**

## Role Variables

All variables which can be overridden are stored in [default/main.yml](default/main.yml) file as well as in table below.

### iptables
##### filter table
| Name           | Default Value | Choices | Description                        |
| -------------- | ------------- | ------- | -----------------------------------|
| `iptables_filter_block_all_inputs` | 'true' | true / false | Enable or disable IPv4 firewall restrictions. |
| `iptables_filter_input_rules` | [] |  | A list with iptables filter INPUT rules. |
| `iptables_filter_forward_rules` | [] |  | A list with iptables filter FORWARD rules. |
| `iptables_filter_output_rules` | [] |  | A list with iptables filter OUTPUT rules. |

##### nat table
| Name           | Default Value | Choices | Description                        |
| -------------- | ------------- | ------- | -----------------------------------|
| `iptables_nat_prerouting_rules` | [] |  | A list with iptables nat PREROUTING rules. |
| `iptables_nat_input_rules` | [] |  | A list with iptables nat INPUT rules. |
| `iptables_nat_output_rules` | [] |  | A list with iptables nat OUTPUT rules. |
| `iptables_nat_postrouting_rules` | [] |  | A list with iptables nat POSTROUTING rules. |

### ip6tables
##### filter table
| Name           | Default Value | Choices | Description                        |
| -------------- | ------------- | ------- | -----------------------------------|
| `ip6tables_filter_block_all_inputs` | 'true' | true / false | Enable or disable IPv6 firewall restrictions. |
| `ip6tables_filter_input_rules` | [] |  | A list with ip6tables filter INPUT rules. |
| `ip6tables_filter_forward_rules` | [] |  | A list with ip6tables filter FORWARD rules. |
| `ip6tables_filter_output_rules` | [] |  | A list with ip6tables filter OUTPUT rules. |

## Example Playbook

```yaml
---
- hosts: all
  tasks:
    - name: Install and manage iptables
      include_role:
        name: ansible-role-iptables
      vars:
        ip6tables_filter_block_all_inputs: false
        iptables_filter_input_rules:
          - "-s 192.168.1.0/24 -p tcp -m tcp --dport 22 -j ACCEPT"
        iptables_nat_postrouting_rules:
          - "-o eth0 -j MASQUERADE"
```
