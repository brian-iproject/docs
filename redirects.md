# Редиректы

### Редирект с html на без html ###
```
#!htaccess

RewriteRule (.+)\.html?$ http://site.ru/$1/ [R=301,L]
```


### Подмена robots.txt ###
```
#!htaccess

RewriteCond %{HTTP_HOST} ^site.ru$
RewriteRule ^robots.txt$ /robots-main.txt [L]
RewriteCond %{HTTP_HOST} ^subdomain.site.ru$
RewriteRule ^robots.txt$ /robots-subdomains.txt [L]
```