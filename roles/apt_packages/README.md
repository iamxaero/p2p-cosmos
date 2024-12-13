apt_packages
=========

Install apt packages into system from apt repos or .deb files

Requirements
------------

No external requirements is needed.

Role Variables
--------------

```yaml
apt_packages:       # List of packages with versions
  - package=version

apt_debs:           # List of URLs o path to .deb files
  - url/to/package.deb
  - path/to/package.deb
```

Usage
-----

```yaml
  - role: apt_packages
    apt_packages:
    - package=version

    apt_debs:
    - url/to/package.deb
    - path/to/package.deb
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

Kuznetsov Vladimir <iamxaero@gmail.com>
