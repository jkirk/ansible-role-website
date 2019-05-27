website
=======

A simple to role to deploy websites.

Requirements
------------

None.

Role Variables
--------------

*  website: Set ServerName in the virtual host configuration and deploy (and enable) it as $website.conf in /etc/apache2/site-available
*  customconf: Path of the custom configuration. Usually sits in files/apache2-sites
*  serveradmin: Set ServerAdmin (can be omitted, if customconf is set)
*  (optional) documentroot: DocumentRoot will be $documentroot/$website. If documentroot is not given it defaults to /var/www/html/$website
*  (optional) webalias: Set ServerAlias (list of aliases allowed)
*  (optional) rootredirection: RedirectMatch ^/$ to a given destination
*  (optional) default_website: Set 000-default.conf symlink for this website
*  (optional) scriptaliasurl: Set URL of ScriptAlias to "/$scriptalias" and Path to "$documentroot/$scriptalias"
*  (optional) scriptaliaspath: Set Path of ScriptAlias to "$documentroot/$scriptaliaspath" (if $scriptaliasurl is defined)
*  (optional) letsencrypt: Enable SSL via letsencrypt (role 'letsencrypt' needs to be called before calling this role)
*  (optional) custom_fragment: Custom Apache configuration

Dependencies
------------

None, but it might be a good idea to use the role letsencrpt to deploy Let's Encrypt for the websites.

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
