* nginx conf
```
server {
    listen       80;
    server_name  opcachegui.vm;
    access_log  /var/log/nginx/opcachegui.vm.access.log;
    error_log   /var/log/nginx/opcachegui.vm.error.log;
    root /mnt/hgfs/xx/github/OpCacheGUI/public/;
    index index.php index.html index.htm;
    auth_basic "OpCacheGUI Login";
    auth_basic_user_file /mnt/hgfs/xx/github/OpCacheGUI/.htpasswd;


    try_files $uri $uri/ /index.php;

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9007;
        fastcgi_index  index.php;
        include fastcgi.conf;
        include fastcgi_params;
    }

}

```
* config.sample.php->config.php
白名单改为*否则可能密码对了也登不上
```
'whitelist'       => [
        '*',
],
```

* .htpasswd 里面的密码是通过openssl passwd生成的
* config.php里面的password是cli/generate_password.php生成，默认这个脚本是有个bug，bug-cli分支已经fix
