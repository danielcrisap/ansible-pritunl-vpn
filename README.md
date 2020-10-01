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

## Database Setup

[](https://docs.pritunl.com/docs/configuration-5#database-setup)

When Pritunl starts for the first time a database setup prompt will be shown on the web server running on port 443. The database setup will prompt for a setup key and MongoDB URI. To get the setup key ssh on to the server and run the command  `sudo pritunl setup-key`  this will return the setup key. By default the MongoDB URI will be filled with the URI for the localhost MongoDB server. This should be left as it is when the MongoDB server is running on the same server as the Pritunl instance. For Enterprise clusters refer to the MongoDB documentation for  [**Connection String URI Format**](https://docs.mongodb.org/manual/reference/connection-string/). Alternatively this can be set directly in the  `/etc/pritunl.conf`  file or using the cli command. More information on the cli command can be found in the  [**Commands**](https://docs.pritunl.com/docs/commands)  sections. Some MongoDB servers authenticate on the admin database and require the option  `authSource=admin`  to be included in the URI.

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

**

## AUTHENTICATION

**

[](https://docs.pritunl.com/docs/wireguard#authentication)

[**WireGuard**](https://www.wireguard.com/)  authentication in Pritunl utilizes keys already in the client profile. This allows transitioning to  [**WireGuard**](https://www.wireguard.com/)  without requiring users to re-import their profile. Many administrators do not configure a valid HTTPS certificate and HTTPS is not relied on or required to provide secure authentication. Authentication is done with three keys providing multiple layers of encryption and authorization.

-   **Client SHA512-HMAC Key (Authorization)**  
    The client will use a SHA512-HMAC secret to sign each connection request. The server will also use this secret to sign the response allowing the client to verify the connection response. This is the same authentication system used to authorize the client configuration sync which syncs profile configuration changes such as host addresses and server port changes (private keys are never synced).
    
-   **Client/Server NaCl Asymmetric Key (Authorization + Encryption)**  
    The client utilizes a  [**NaCl**](https://en.wikipedia.org/wiki/NaCl_%28software%29)  public key for the server that is included in the client profile. This provides asymmetric encryption of the connection request from the client to the server. The server will encrypt the response with the clients  [**NaCl**](https://en.wikipedia.org/wiki/NaCl_%28software%29)  public key providing encryption of the response. The client will also verify the server response using the server  [**NaCl**](https://en.wikipedia.org/wiki/NaCl_%28software%29)  public key. This is the same authentication system used to provide the additional layer of encryption and authorization available in  [**OpenVPN**](https://openvpn.net/)  connections with passwords and two-factor codes.
    
-   **Client RSA-4096 Asymmetric Key (Authorization)**  
    The clients RSA certificate and key is used to sign each connection request. The server will use this verify the client connection request. This is the same certificate used to verify  [**OpenVPN**](https://openvpn.net/)  connections.
    

Each  [**WireGuard**](https://www.wireguard.com/)  connection uses a new  [**WireGuard**](https://www.wireguard.com/)  key. This is done to provide the highest level of security but it will delay network connectivity when the user returns to a computer that has been asleep. The  [**WireGuard**](https://www.wireguard.com/)  private key is stored in the memory of the Pritunl client background service and also in the  [**WireGuard**](https://www.wireguard.com/)  configuration file.  [**WireGuard**](https://www.wireguard.com/)  uses a connection-less design and this private key could be used by an attacker to hijack the connection even if multi-factor authentication is used. In high security environments it is important to consider that  [**OpenVPN**](https://openvpn.net/)  connections with multi-factor authentication will not have these weaknesses. For this reason the server will quickly revoke  [**WireGuard**](https://www.wireguard.com/)  keys of inactive clients to limit the possibility of this occurring. The server will also validate that keys are not reused.

Once the client has connected it will send a ping request to the server every 10 seconds. This request allows the client to quickly detect a down link and failover in approximately 13 seconds. If the server does not receive a ping request in 6 minutes it will disconnect the user and revoke the public key.

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
