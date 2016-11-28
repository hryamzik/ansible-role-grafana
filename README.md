# Grafana
## Summary
This role installs and configures _Grafana_.

## Variables
Any variables in _defaults/main.yml_ can be redefined in a playbook. There are no mandatory variables, the role will work fine with default settings.

## Configuration of _Grafana_
This role installs Grafana with the default configuration (only with some minor security fixes). Usage of custom configuration hasn't been supported yet.
If you would like to install the latest beta version, define the _grafana_beta_ variable. If _grafana_latest: true_ the role will update the current version of Grafana on your server or will install the latest version from scratch. If _grafana_latest: false_, the role will not update the current version of Grafana (if exists on your server), but if there is no Grafana found on the server, it will install the latest version anyway.

## systemd/sysvinit/upstart
We install Grafana from pre-built DEB/RPM packages. All these packages work correctly with sysvinit, upstart and sysvinit. No additional actions required.

## Dependencies
None.

In some cases, you should manually install _python2_ (absent in Ubuntu 16.04). Example playbook:
```
- hosts: all
  become: yes
  gather_facts: no
  tasks:
    - name: install python2
      raw: test -e /usr/bin/python || (apt update && apt install -y python-minimal)
      changed_when: false
    - name: gather facts
      setup:

- hosts: all
  roles:
    - { role: grafana,  grafana_beta: no }
```

## Platforms
All supported platforms are listed in _molecule.yml_.
