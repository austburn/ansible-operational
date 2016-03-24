Targeting Hosts
---------------
- all or all/*
- Groups
- Exclusion (webservers:!nginxservers)
- Intersection (webservers:&staging)
- Other
    - combos
    - hostname/ip
    - regex
    - --limit


Executing a Task
----------------
- ad-hoc commands are single tasks which leverage modules
- modules are code executed on the remote host
    - host machine needs python
    - ansible ships the module over via ssh and executes them on the host
- ansible core modules
    - return json data
    - written in python ^^
- ansible webservers -f 10 -m setup (set fork level to 10)
    - useful for setting fork level to one to do a rolling deploy - finish one node before moving to the next


Tasks
-----
- ansible is idempotent - will not blindly perform the same task twice - knows that it doesn't have to redo work
    - notice the "changed" key in the output
- Copy
    ansible hosts -m copy -a "src=/path/to/src dest=/path/to/dest"
- Install nginx and add a user
    ansible all -m apt -a "pkg=nginx state=present" (must target debian/ubuntu)
    ansible all -m yum -a "pkg=nginx state=present" (centos)
    ansible all -m package -a "pkg=nginx state=present" (generic)
        - has to do fact gathering first
    ansible all -m user -a "name=bob state=present"
- clone a git repo
    ansible appservers -m git -a "repo=https://github.com/user/repo dest=/home/user/repo"
    - have to setup the authentication creds on the host machine
- service status
    ansible -m service -a "name=httpd state=started"
- Backgrounding tasks, with opt polling
    ansible all -B 3600 -a "/usr/bin/long_running_op --do-stuff"
    ansible all -B 1800 -P 60 -a "/usr/bin/long_running_op --do-stuff"
- setup gathers facts
    ansible host -m setup
