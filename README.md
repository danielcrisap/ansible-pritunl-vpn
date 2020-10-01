Ansible role for Pritunl VPN
=========

[![Build Status](https://travis-ci.com/danielcrisap/ansible-pritunl-vpn.svg?branch=master)](https://travis-ci.com/danielcrisap/ansible-pritunl-vpn)

This role will install Pritunl VPN.

Requirements
------------
Adding new requirements

This aplication need it to run in an Linux server, can be  under Cent Os, Amazon Linux, Debian and Ubunto.

Pritunl using MongoDB as database so you should have some MongoDB server.

Role Variables
--------------

```yml
pritunl_mongodb_uri: 'mongodb://localhost:27017/pritunl?authSource=admin&ssl=true'
```
`pritunl_mongodb_uri` MongoDB URI for Pritunl to connect to the database.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yml
    - hosts: servers
      vars:
        pritunl_mongodb_uri: 'mongodb://localhost:27017/pritunl?authSource=admin&ssl=true'
      roles:
         - { role: danielcrisap.ansible-pritunl-vpn }
```

License
-------

MIT &copy;

Author Information
------------------

This collection was created in 2020 by [Daniel Cristian](https://github.com/danielcrisap).
