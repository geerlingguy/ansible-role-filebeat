# Ansible Role: Filebeat for ELK Stack

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-filebeat)

An Ansible Role that installs Filebeat on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    TODO

## Dependencies

None.

## Example Playbook

    - hosts: logs
      roles:
        - geerlingguy.java
        - geerlingguy.elasticsearch
        - geerlingguy.logstash
        - geerlingguy.filebeat

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Jeff Geerling](http://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
