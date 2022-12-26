# Редиректы

### Редирект с html на без html ###
``` apacheconf
RewriteRule (.+)\.html?$ http://site.ru/$1/ [R=301,L]
```

### Редирект без www на www ###
``` apacheconf
RewriteCond %{HTTP_HOST} ^site.ru
RewriteRule (.*) http://www.site.ru/$1 [R=301,L]
```

### Редирект с www на без www ###
``` apacheconf
RewriteCond %{HTTP_HOST} ^www.site.ru
RewriteRule (.*) http://site.ru/$1 [R=301,L]
```

### Убираем лишние слеши ###
``` apacheconf
RewriteCond %{REQUEST_URI} ^(.*)/{2,}(.*)$
RewriteRule . %1/%2 [R=301,L]
```
``` apacheconf
RewriteCond %{THE_REQUEST} //
# Проверяем, повторяется ли слеш (//) более двух раз.
RewriteRule .* /$0 [R=301,L]
# Исключаем все лишние слеши.
```

### Подмена robots.txt ###
``` apacheconf
RewriteCond %{HTTP_HOST} ^site.ru$
RewriteRule ^robots.txt$ /robots-main.txt [L]
RewriteCond %{HTTP_HOST} ^subdomain.site.ru$
RewriteRule ^robots.txt$ /robots-subdomains.txt [L]
```

### Редирект с http на https ###
``` apacheconf
RewriteCond %{HTTPS} =off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [QSA,L]
```
``` apacheconf
RewriteCond %{SERVER_PORT} !^443$
RewriteRule .* https://%{SERVER_NAME}%{REQUEST_URI} [R,L]
```
``` apacheconf
RewriteCond %{ENV:HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```
``` apacheconf
RewriteCond %{HTTP:X-HTTPS} !1
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
```
``` apacheconf
RewriteCond %{HTTP:CF-Visitor} '"scheme":"http"'
RewriteRule ^(.*)$ https://www.domain.com/$1 [L] #не забудьте заменить на ваш домен
```
``` apacheconf
RewriteCond %{HTTP:X-Forwarded-Protocol} !=https
RewriteRule .* https://%{SERVER_NAME}%{REQUEST_URI} [R=301,L]
```
``` apacheconf
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE]
```

### Редирект с https на http ###
``` apacheconf
RewriteCond %{SERVER_PORT} ^443$ [OR]
RewriteCond %{HTTPS} =on
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```
``` apacheconf
RewriteCond %{SERVER_PORT} ^443$
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```
``` apacheconf
RewriteCond %{HTTPS} =on
RewriteRule ^(.*)$ http://site.ru/$1 [R=301,L]
```

### Настройка переадресации на папки со слешем в конце / ###
#### Apache ####
``` apacheconf
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_URI} !\..{1,10}$
RewriteCond %{REQUEST_URI} !(.*)/$
RewriteRule ^(.*)$ http://www.site.ru/$1/ [L,R=301]
```

#### Nginx ####
```  apacheconf
if (!-f $request_filename){
  rewrite ^([^.\?]*[^/])$ $1/ permanent;
}
```

### Настройка переадресации с index.php на без index.php ###
#### Apache ####
``` apacheconf
RewriteCond %{THE_REQUEST} /(.*)index.php.*$
RewriteCond %{THE_REQUEST} !bitrix/admin/
RewriteRule .* https://mir-lest.ru/%1 [R=301,L]
```

#### Nginx ####
``` apacheconf
if ($request_uri ~ "^(.*)index\.(?:php|html)") {
    return 301 $1;
}
```