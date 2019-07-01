website
=======

[![Build Status](https://travis-ci.com/jkirk/ansible-role-website.svg?branch=master)](https://travis-ci.com/jkirk/ansible-role-website)

A simple to role to deploy websites.

Requirements
------------

None.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ansible-role-website

# Set ServerName in the virtual host configuration and deploy (and enable) it as /etc/apache2/site-available/$website_domain.conf
website_domain: 'demo.example.com'

# Name of the custom configuration file which should be used instead of the the website template.
# It will then be placed in /etc/apache2/sites-available/$website_domain.conf
#
# website_customconf: 'demo.example.conf'

# Set ServerAdmin (can be omitted, if website_customconf is set)
website_serveradmin: 'webmaster@example.com'

# DocumentRoot will be $website_documentroot_base/$website_domain. If website_documentroot_base is not given, DocumentRoot defaults to /var/www/html/$website
# website_documentroot_base: '/srv/www'

# Set ServerAlias
# TODO: (list of aliases allowed)
# website_webalias: 'demo2.example.com'

# RedirectMatch ^/$ to a given destination
# website_rootredirection: 'https://othersite.example.com'

# Set 000-default.conf symlink for this website
website_default: false

# Set "ProxyPass / $website_proxy" and "ProxyPassReverse / $website_proxy" (if website_proxyreverse is not defined)
# website_proxy: 'http://localhost:8080/'
#
# Set "ProxyPassReverse / $website_proxyreverse"
# website_proxyreverse: 'http://localhost:8080/'
#
# Set "AllowEncodedSlashes" to 'On' (not recommended), 'Off' (default) or 'NoDecode'
website_encoded_slashes: 'Off'

# Set ScriptAlias $website_scriptalias_url to "$website_documentroot_base/$website_scriptalias_url"
# website_scriptalias_url: 'cgi-bin/'

# Set ScriptAlias $website_scriptalias_url to "$website_documentroot_base/$website_scriptalias_path" instead of "$website_documentroot_base/$website_scriptalias_url"
# website_scriptalias_path: 'myapp'

# Enable SSL via website_letsencrypt (role 'website_letsencrypt' needs to be called before setting this to True)
website_letsencrypt: false

# Always redirect http to https:
website_httpsonly: false

# Put custom Apache configuration fragment in vhost section
# website_custom_fragment: |
#     <Directory /srv/www/${DOMAIN}>
#       Options -Indexes +FollowSymLinks
#       AllowOverride All
#     </Directory>
```

Dependencies
------------

None, but it might be a good idea to use the role [website_letsencrypt](https://github.com/jkirk/ansible-role-website_letsencrypt) to deploy Let's Encrypt for the websites.

Examples
--------

```
  roles:
    - { role: jkirk.website, website_domain: 'demo.example.at', website_webalias: 'www.demo.example.at', website_rootredirection: 'https://demo2.example.com', website_serveradmin: 'webmaster@example.at', website_letsencrypt: true }
```

or:
```
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

Darshaka Pathirana - https://synpro.solutions
