Control Structures
------------------
- `with_item`
```
- name: add users
  user: name={{ item }} state=present groups=wheel
  with_items:
    - user1
    - user2
```
Or...
```
- name: add users
  user: name={{ item }} state=present groups=wheel
  with_items: "{{ my_items_var }}"
```


Conditionals
------------
- Task conditionals
    - use `when`
    ```
    - name: install nginx
      yum: name=nginx state=present
      when: ansible_distribution == 'CentOS'
    - name: install nginx
      apt: name=nginx state=present
      # bare variables complaints?
      when: ansible_distribution == 'Debian'
- `group_by`: create dynamic groups
```
- name: grouping play
  hosts: all
  tasks:
    # this will create groups CentOS, Ubuntu, etc.
    - name: create distro groups
      group_by: key={{ ansible_distribution }}

- name: CentOS play
  hosts: CentOS
  gather_facts: False
  tasks:
    - # only affect CentOS hosts
```


Status Control
--------------
- `failed_when`
- `changed_when`

Local Action
------------
- `local_action` - perform task on local machine
- `connection: local` - perform this play locally
