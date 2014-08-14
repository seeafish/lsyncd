lsyncd
======

### Description
Lsyncd playbook to deploy a master server on CentOS/RHEL 6/7

### Important information
* Be sure to set up slave IPs and excludes in vars/main.yml
* If no excludes are required, leave the hash values under
lsyncd_excludes commented out, but the hash itself in place.

### Example playbook
```yaml
---
- hosts: all
  vars_files:
  - lsyncd/vars/{{ ansible_os_family }}.yml
  roles:
  - lsyncd
```

Alternatively, the vars can be overridden in the playbook:

```yaml
---
- hosts: all
  vars:
  - lsyncd_slaves:
    - { remote_ip: '10.10.10.1' }
    - { remote_ip: '10.10.10.2' }
    - { remote_ip: '10.10.10.1' }
  - lsyncd_excludes:
    - { exclude_dir: 'blah/' }
  vars_files:
  - lsyncd/vars/{{ ansible_os_family }}.yml
  roles:
  - lsyncd
```

### Todo
* SSH key to remote servers
* Other OS support
