website
=======

[![Build Status](https://travis-ci.com/jkirk/ansible-role-website.svg?branch=master)](https://travis-ci.com/jkirk/ansible-role-website)

A simple to role to deploy websites.

Requirements
------------

None.

Role Variables
--------------

These variables are set in defaults/main.yml:
```yaml
---
# defaults file for ansible-role-website

# Set ServerName in the virtual host configuration and deploy (and enable) it as $website.conf in /etc/apache2/site-available
website: 'demo.example.com'

# Name of the custom configuration file which should be used instead of the the website template.
# It will then be placed in /etc/apache2/sites-available/$website.conf
#
# customconf: 'demo.example.conf'

# Set ServerAdmin (can be omitted, if customconf is set)
serveradmin: 'webmaster@example.com'

# DocumentRoot will be $documentroot/$website. If documentroot is not given, DocumentRoot defaults to /var/www/html/$website
# TODO: should be renamed to documentroot_base
# documentroot: '/srv/www'

# Set ServerAlias
# TODO: (list of aliases allowed)
# webalias: 'demo2.example.com'

# RedirectMatch ^/$ to a given destination
# rootredirection: 'https://othersite.example.com'

# Set 000-default.conf symlink for this website
default_website: false

# Set ScriptAlias $scriptaliasurl to "$documentroot/$scriptaliasurl"
# scriptaliasurl: 'cgi-bin/'

# Set ScriptAlias $scriptaliasurl to "$documentroot/$scriptaliaspath" instead of "$documentroot/$scriptaliasurl"
# scriptaliaspath: 'myapp'

# Enable SSL via letsencrypt (role 'letsencrypt' needs to be called before setting this to True)
letsencrypt: false

# Put custom Apache configuration fragment in vhost section
# custom_fragment: |
#     <Directory /srv/www/${DOMAIN}>
#       Options -Indexes +FollowSymLinks
#       AllowOverride All
#     </Directory>
```

Dependencies
------------

None, but it might be a good idea to use the role [letsencrypt](https://github.com/jkirk/ansible-role-letsencrypt) to deploy Let's Encrypt for the websites.

Examples
--------

```
  roles:
    - { role: jkirk.website, website: 'demo.example.at', webalias: 'www.demo.example.at', rootredirection: 'https://demo2.example.com', serveradmin: 'webmaster@example.at', letsencrypt: true }
```

or:
```
  roles:
    - role: jkirk.website
      website: 'demo.example.com'
      webalias: 'www.example.com'

      letsencrypt: true
      httpsonly: true

      documentroot: '/srv/www'
      serveradmin: 'tech@example.com'
      custom_fragment: |
       # custom_fragment from config
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

Darshaka Pathirana - https://synpro.solutions
