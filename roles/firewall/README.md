firewall
=========

Configure firewall on Ubuntu "ufw"

Requirements
------------

No external requirements is needed.

Role Variables
--------------

```yaml
allow_ports: # List of ports
  - 22   # SSH
  - 80   # HTTP
  - 443  # HTTPS
  - 8080 # exporter
default_policy: "allow"  # Default policy (deny or allow)
```

Usage
-----


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

Kuznetsov Vladimir <iamxaero@gmail.com>
