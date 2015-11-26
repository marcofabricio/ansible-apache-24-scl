# Apache 2.4 SCL

[![Build Status](https://travis-ci.org/unfinisheddev/ansible-apache-24-scl.svg)](https://travis-ci.org/unfinisheddev/ansible-apache-24-scl)

An Ansible role to install Apache 2.4 from the Software Collections Library.

As this role installs Apache from the SCL, it only supports RedHat family operating systems

## Requirements

None

## Role Variables

---

### `apache24_scl_install_apache`

Should this role install the Apache package? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `apache24_scl_install_packages`

List of packages that will be installed by this role.

These packages will only be installed if `apache24_scl_install_apache` is `yes`|`true`

Default value:
```
- httpd24
```

### `apache24_scl_manage_modules`

Should this role manage the Apache modules? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `apache24_scl_enabled_modules`

An array of modules that should be enabled

These modules will only be installed/enabled if `apache_scl_manage_modules` is `yes`|`true`

Default value: `[]`

### `apache24_scl_disabled_modules`

An array of modules that should be disabled

These modules will only be installed/enabled if `apache_scl_manage_modules` is `yes`|`true`

Default value: `[]`

### `apache24_scl_manage_service`

Should this role manage the Apache service? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `apache24_scl_service_name`

The name of the Apache service

Default value: `httpd24-httpd`

### `apache24_scl_service_status`

The status the Apache service should be in.

The service status will only be managed if `apache24_scl_manage_service` is `yes`|`true`

Default value: `started`

### `apache24_scl_service_enabled`

Should the Apache service be enabled (started on boot)? Valid values are `yes`, `true`, `no` or `false`

The service status will only be managed if `apache24_scl_manage_service` is `yes`|`true`

Default value: `yes`

### `apache24_scl_conf_d_directory_path`

The absolute path to the `conf.d` directory of the Apache install

Default value: `/opt/rh/httpd24/root/etc/httpd/conf.d`

### `apache24_scl_manage_vhosts`

Should this role manage the virtual hosts? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `apache24_scl_vhosts`

An array of virtual host objects that should exist

The virtual hosts will only be created / modified if `apache_scl_manage_vhosts` is `yes`|`true`

Default value: `[]`

### `apache24_scl_disabled_vhosts`

An array of virtual hosts that should be disabled. A disabled virtual host will have the configuration
file deleted

The virtual hosts will only be disabled if `apache_scl_manage_vhosts` is `yes`|`true`

Default value: `[]`

### `apache24_scl_install_scl_repo`

Should this role install the Software Collections repository? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `apache24_scl_scl_utils_packages`

List of packages to install for SCL utils

The packages will only be installed if `apache24_scl_install_scl_repo` is set to `yes`|`true`

Default value:
```
- scl-utils
```

### `apache24_scl_scl_repo_url`

Full URL of the RPM to install if `apache24_scl_install_scl_repo` is set to yes

Default value: `"https://www.softwarecollections.org/en/scls/rhscl/httpd24/epel-{{ ansible_distribution_major_version }}-{{ ansible_architecture }}/download/rhscl-httpd24-epel-{{ ansible_distribution_major_version }}-{{ ansible_architecture }}.noarch.rpm"`


## Dependencies

None

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

## License

MIT

## Author Information

Role created by [Dave Kirk](http://unfinisheddev.com)
