Content Organization
--------------------
- ansible expects files in certain locations
    - http://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout



Variables
---------
- Host Variables are facts about a server
    - Examples
        - hostname
        - ip addresses
        - date/time info
        - cpu/disk/memory
        - hardware architecture
        - os info
    - Come from
        - inventory
        - host name
        - host_vars
- Group Variables
    - Come from:
        - inventory
        - group_vars
    - `all` is a special keyword - applied to all hosts/groups/etc
- Precedence
    - should feel _natural_
    - Most specifically applied variable wins
- Uses `mustache`-like variable expansion
group_vars/all
```yaml
---
apache2_version: 2.2.22-1ubuntu1
```
tasks
```
- apt: name="apache2={{ apache2_version }}" state=present
```
- register is a special keyword that will assign the output of a module to a variable
```
- git: repo=git://github.com/ansible/ansible.git dest=/tmp/ansible
  register: ansible_git
```
- debug module
```
- debug: var=ansible_git
# prints information about the variable
```
