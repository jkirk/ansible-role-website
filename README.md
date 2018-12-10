website
=======

A simple to role to deploy websites.

Requirements
------------

None.

Role Variables
--------------

*  website: Set ServerName in the virtual host configuration and deploy (and enable) it as $website.conf in /etc/apache2/site-available
*  serveradmin: Set ServerAdmin
*  (optional) documentroot: DocumentRoot will be $documentroot/$website. If documentroot is not given it defaults to /var/www/html/$website
*  (optional) webalias: Set ServerAlias (list of aliases allowed)
*  (optional) rootredirection: RedirectMatch ^/$ to a given destination
*  (optional) letsencrypt: Enable SSL via letsencrypt (role 'letsencrypt' needs to be called before calling this role)

Dependencies
------------

None, but it might be a good idea to use the role letsencrpt to deploy Let's Encrypt for the websites.

Example Playbook
----------------

```
  roles:
    - { role: website, website: 'demo.example.at', webalias: 'www.demo.example.at', rootredirection: 'https://demo2.example.com', serveradmin: 'webmaster@example.at', letsencrypt: true }
```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
