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