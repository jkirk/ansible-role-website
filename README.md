website
=======

[![GitHub Super-Linter](https://github.com/jkirk/ansible-role-base/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)

A simple to role to deploy websites.

Requirements
------------

None.

Role Variables
--------------

Role variables are set and documented in [`defaults/main.yml`](defaults/main.yml):

Dependencies
------------

None, but it might be a good idea to use the role [website_letsencrypt](https://github.com/jkirk/ansible-role-website_letsencrypt) to deploy Let's Encrypt for the websites.

Examples
--------

```yaml
  roles:
    - { role: jkirk.website, website_domain: 'demo.example.at', website_webalias: 'www.demo.example.at', website_rootredirection: 'https://demo2.example.com', website_serveradmin: 'webmaster@example.at', website_letsencrypt: true }
```

or:
```yaml
  roles:
    - role: jkirk.website
      website_domain: 'demo.example.com'
      website_webalias: 'www.example.com'

      website_letsencrypt: true
      website_httpsonly: true

      website_documentroot_base: '/srv/www'
      website_serveradmin: 'tech@example.com'
      website_custom_fragment: |
       # website_custom_fragment from config
               <Directory /srv/www/${DOMAIN}>
                 Options -Indexes +FollowSymLinks
                 AllowOverride All
               </Directory>
```

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - <https://synpro.solutions>
