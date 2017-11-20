# Редиректы

### Редирект с html на без html ###
```
#!htaccess

RewriteRule (.+)\.html?$ http://site.ru/$1/ [R=301,L]
```