# Редиректы

### Редирект с html на без html ###
```
RewriteRule (.+)\.html?$ http://site.ru/$1/ [R=301,L]
```

### Редирект без www на www ###
```
RewriteCond %{HTTP_HOST} ^site.ru
RewriteRule (.*) http://www.site.ru/$1 [R=301,L]
```

### Редирект с www на без www ###
```
RewriteCond %{HTTP_HOST} ^www.site.ru
RewriteRule (.*) http://site.ru/$1 [R=301,L]
```

### Подмена robots.txt ###
```
RewriteCond %{HTTP_HOST} ^site.ru$
RewriteRule ^robots.txt$ /robots-main.txt [L]
RewriteCond %{HTTP_HOST} ^subdomain.site.ru$
RewriteRule ^robots.txt$ /robots-subdomains.txt [L]
```

### Редирект с http на https ###
```
RewriteCond %{HTTPS} =off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [QSA,L]
```
```
RewriteCond %{SERVER_PORT} !^443$
RewriteRule .* https://%{SERVER_NAME}%{REQUEST_URI} [R,L]
```
```
RewriteCond %{ENV:HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```
```
RewriteCond %{HTTP:X-HTTPS} !1
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
```
```
RewriteCond %{HTTP:CF-Visitor} '"scheme":"http"'
RewriteRule ^(.*)$ https://www.domain.com/$1 [L] #не забудьте заменить на ваш домен
```
```
RewriteCond %{HTTP:X-Forwarded-Protocol} !=https
RewriteRule .* https://%{SERVER_NAME}%{REQUEST_URI} [R=301,L]
```
```
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE]
```

### Редирект с hhtps на http ###
```
RewriteCond %{SERVER_PORT} ^443$ [OR]
RewriteCond %{HTTPS} =on
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```
```
RewriteCond %{SERVER_PORT} ^443$
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```
```
RewriteCond %{HTTPS} =on
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```

### Настройка переадресации на папки со слешем в конце / ##
```
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_URI} !\..{1,10}$
RewriteCond %{REQUEST_URI} !(.*)/$
RewriteRule ^(.*)$ http://www.site.ru/$1/ [L,R=301]
```