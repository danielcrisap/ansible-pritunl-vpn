Ansible role for Pritunl VPN
=========

[![Build Status](https://travis-ci.com/danielcrisap/ansible-pritunl-vpn.svg?branch=master)](https://travis-ci.com/danielcrisap/ansible-pritunl-vpn)

This role will install Pritunl VPN.

**

## What is Pritunl

Pritunl is an open source VPN server and management panel. It gives the user the power of the OpenVPN protocol while using an intuitive web interface


Requirements
------------
Adding new requirements

This aplication need it to run in an Linux server, can be  under Cent Os, Amazon Linux, Debian and Ubunto.

Pritunl using MongoDB as database so you should have some MongoDB server.


## **About Subscriptions**

Subscriptions can purchased on the homepage or from the web console of a running Pritunl server. Credit card information is securely sent from the web browser directly to Stripe and is never stored or transferred on any other servers. A Pritunl server can be upgraded at any time and does not need to be reconfigured when upgrading to a subscription.

## 

License Key

[](https://docs.pritunl.com/docs/subscription#license-key)

After creating a subscription a license key will be emailed to the email address used during checkout. The license key does not need to be used on the same server that was used to create the subscription. Premium subscriptions can be used for only one server and Enterprise licenses can be used for only one cluster. A cluster is a group of Pritunl servers connected to the same MongoDB database. To allow for testing the license keys can be used multiple times but continued use of the license keys on multiple servers will result in the subscription being canceled.

## 

Invoice and Long-Term Subscriptions

[](https://docs.pritunl.com/docs/subscription#invoice-and-long-term-subscriptions)

Some companies require full form invoices and annual subscriptions. This is only available with Enterprise subscriptions and there is no discount for annual subscriptions. To request an annual invoice for an Enterprise subscription email the bill-to information to contact@pritunl.com include an email address to receive the invoice and an email address to receive the license key.

## 

Education Discount

[](https://docs.pritunl.com/docs/subscription#education-discount)

There is a 50% discount available to public schools. This can be applied to an existing monthly subscription or to an annual subscription. For a discount on monthly subscriptions first start a trial then send the email address used to create the subscription to contact@pritunl.com, for an annual subscription follow the instructions above.


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
