Inventory
---------
- static inventory
    - contains a list of human readable hostname/ip pairs
    - list of nodes you wish to interact with
    - INI format
    - can contain groups
    [groupname]
    web1 ansible_ssh_host=10.10.10.10
- dynamic
    - static inventories have limitations in a cloud environment (nodes are coming and going, etc.)
    - can be a script as opposed to an ini
