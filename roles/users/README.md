users
=========

Configure local users on remote host and set up SSH for key auth.

Requirements
------------

No external requirements is needed.

Role Variables
--------------

```yaml
users_root_group: # OS-specific root group
users_common_group: # Default group for users
users_default_shell: # Default user shell
users_gitlab_url: # Gitlab base URL for keys GET

users_default_userdb: # Dict with users and user settings
  UserName:
    authorized: # If authorized section is absent -- attempts to get key from users_gitlab_url/UserName.keys
      - ssh-rsa long_rsa_public_key_here
    pass: SHA512_password_hash
    home: /home/UserName
    email: UserName@huawei.com
    name: UserName Readable name
    state: present

users_default_user_list: # List of users to create
  - UserName

users_userdb: '{{ global_users_userdb | default(users_default_userdb, True) }}' # userdb with fallback to default
users_user_list: '{{ global_users_user_list | default(users_default_user_list, True) }}' # List of users with fallback to default
users_group_list: '{{ global_users_group_list | default(users_common_group, True) }}' List of groups with fallback to default
```

Usage
-----
for new Ubunta server:
```
--extra-vars "ansible_user=huawei ansible_password=pass ansible_sudo_pass=pass"
```

```yaml
  - role: users
    users:
      - n00540050
      - kwx768532
    users_groups:
      - "{{root_group}}"
```

TODO
-----

```yaml
- name: disable passwordless login
  become: true
  lineinfile:
    dest:/etc/ssh/sshd_config
    state: present
    regexp: '^#?PasswordAuthentication'
    line: 'PasswordAuthentication no'
  notify: reload ssh
  when: remote_enable | changed
 TODO:
- name: flush root pass
  become: true
  user:
    name: root
    password: "*"
  when: root_password_enabled is not defined
- name: disable password login to root via ssh
  become: true
  lineinfile:
    dest: /etc/ssh/sshd_config
    regexp: '^PermitRootLogin .*$'
    line: 'PermitRootLogin without-password'
    state: present
  notify: reload ssh
```

Generate hash password
------------------

ansible all -i localhost, -m debug -a "msg={{ 'mypassword' | password_hash('sha512') }}"

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
