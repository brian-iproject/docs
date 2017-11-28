# Редиректы

### Редирект с html на без html ###
```
#!htaccess

RewriteRule (.+)\.html?$ http://site.ru/$1/ [R=301,L]
```

### Редирект без www на www ###
```
#!htaccess

RewriteCond %{HTTP_HOST} ^site.ru
RewriteRule (.*) http://www.site.ru/$1 [R=301,L]
```

### Подмена robots.txt ###
```
#!htaccess

RewriteCond %{HTTP_HOST} ^site.ru$
RewriteRule ^robots.txt$ /robots-main.txt [L]
RewriteCond %{HTTP_HOST} ^subdomain.site.ru$
RewriteRule ^robots.txt$ /robots-subdomains.txt [L]
```

### Редирект с http на https ###
```
#!htaccess

RewriteCond %{ENV:HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```
```
#!htaccess

RewriteCond %{HTTP:X-HTTPS} !1
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
```