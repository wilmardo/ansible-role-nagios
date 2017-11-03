# wilmardo.nagios

[![Build Status](https://travis-ci.org/wilmardo/ansible-role-nagios.svg?branch=master)](https://travis-ci.org/wilmardo/ansible-role-nagios)
[![Galaxy](http://img.shields.io/badge/galaxy-wilmardo.nagios-blue.svg)](https://galaxy.ansible.com/wilmardo/nagios/)

Installs Nagios 4.3.2 from source. Once Nagios is installed you can login to http://ip-address/nagios/ using the username and password you configure in the nagios_users variable.
The NRPE client can be installed through [wilmardo.nrpe_client](https://galaxy.ansible.com/wilmardo/nrpe-client/), this enables Nagios to monitor the server.

## Requirements

None.

## Role Variables

### Default usage

For default usage of this role you only need to define the following:
```yaml  
# The users which should be allowed to login to the Nagios web GUI.
nagios_users:
  - user: nagiosadmin
    pass: Password1change
```

### Advance usage

For more advanced usage the following variables are available:
```yaml
# The directory where the downloaded files will be placed and extracted.
nagios_download_dir: "{{ ansible_env.HOME }}/nagios"

# The version of Nagios to be installed    
nagios_version: 4.3.4

# The Nagios download url
nagios_url: https://github.com/NagiosEnterprises/nagioscore/archive/nagios-{{ nagios_version }}.tar.gz

# The name of the untarred Nagios directory
nagios_src: "nagioscore-nagios-{{ nagios_version }}"

# The version of Nagios Plugins to be installed
nagios_plugins_version: 2.2.1

# The Nagios Plugins download url
nagios_plugins_url: http://www.nagios-plugins.org/download/nagios-plugins-2.1.1.tar.gz

# The name of the untarred Nagios Plugins directory
nagios_plugins_src: nagios_plugins_src: "nagios-plugins-release-{{ nagios_plugins_version }}"

# The user which the Nagios daemon runs as
nagios_monitoring_user: nagios

# The group which the Nagios daemon runs as
nagios_monitoring_command_group: nagios
```

## Dependencies

None.

## Example Playbook

Install Nagios and setup the password for your nagiosadmin user.
It is better to move the nagios_users to host_vars of your project but this will work.
```yaml  
- hosts: nagios
  vars_files:
   - vars/main.yml
  roles:
     - { role: wilmardo.nagios, nagios_users: [{name: nagiosadmin, pass: Password1change}, {name: nagiosadmin1, organization: Password2change}] } }
```

## Upgrading

The role has automatic upgrade when you change the version with var:
```yaml  
nagios_version: 4.3.4
```

But the upgrade requires to remove some old files to, check [build-nagios.yml](tasks/build-nagios.yml) for details.

## License

BSD-3-Clause-Clear

## Author Information

This role was originally created by [Patrick Ogenstad](http://networklore.com).
Forked in 2017 by [Wilmar den Ouden](https://wilmardenouden.nl).
