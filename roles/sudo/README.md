sudo
=========

Configure sudoers on remote host

Requirements
------------

No external requirements is needed.

Role Variables
--------------

```yaml
sudo_root_group: dynamicly generate root group name (**wheel** or **sudo**)
sudo_filename: name of file with sudo settings, which will be created in /etc/sudoers.d
sudo_remove: if false -- will create file with rules, if true -- will delete file

sudo_sudoers:
  custom_privileges:
    hosts:  # list of hosts
      test_server_group1:  # server groupname
        users: # list of users in groupname with privileges
          test_server_user1:
            - "NOPASSWD: ALL"
      test_server_group2:
        users:
          test_server_user2:
            - "NOPASSWD: ALL"
        usergroups: # list of groups with privileges
          test_team2:  # usergroup
            - "NOPASSWD: /bin/ls *"
```

Dependencies
------------

No additional dependencies is needed

Example Playbook
----------------

None

License
-------

GPLv3

Author Information
------------------

Kuznetsov Vladimir WX768954 <kuznetsov.vladimir@huawei.com>