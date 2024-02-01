# FancyIndex

Сначала получите исходный код Nginx. Версия должна точно соответствовать той, что имеется в системе.

```
nginx -v
nginx version: nginx/1.18.0 (Ubuntu)
```

```
wget https://nginx.org/download/nginx-V.V.V.tar.gz // версия из предыдущего шага
tar xzvf nginx-1.18.0.tar.gz
git clone https://github.com/aperezdc/ngx-fancyindex.git
cd nginx-1.18.0

sudo apt install -y libpcre3-dev libxslt-dev libgd-dev libgeoip-dev libssl-dev
./configure [... args from nginx -V] --add-dynamic-module=../ngx-fancyindex
make modules

sudo cp objs/ngx_http_fancyindex_module.so /usr/share/nginx/modules
```

В `/etc/nginx/nginx.conf` нужно добавить

```
load_module /usr/share/nginx/modules/ngx_http_fancyindex_module.so;
```

И включить модуль в настройках сайта

```
location / {
    # autoindex on;
    fancyindex on;
    fancyindex_exact_size off;
}
```


```Shell
sudo nginx -t
sudo nginx -s reload
```