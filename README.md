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

### Modifying slaves and excludes
By changing either ```lsyncd_slaves``` or ```lsyncd_excludes``` hashes (either in vars/main.yml
or override fromm the playbook run itself), the master
can be modified to add/remove slaves and/or excluded directories by running the playbook
with tag 'reconfig':
```bash
ansible-playbook -i hosts playbook.yml --tags=reconfig
```
This will skip all the installation and checking sections, and simply rewrite the config
with the values specified in your hash.

### Todo
* SSH key to remote servers
* Other OS support
