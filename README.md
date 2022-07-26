## 这是个啥玩意儿？
稳定和最新的 nginx，支持 HTTP/2, brotli压缩。包含了 Cloudflare 优化的 zlib 和 支持 TLS 1.3 、BoringSSL 等价加密套件、 CHACHA20-Poly1305 草案的 OpenSSL 库。除此之外，我还添加了一些 nginx 模块。
## What is this？
Stable and up-to-date nginx with HTTP/2 support, with brotli compression, include zlib by Cloudflare and OpenSSL library with TLS 1.3 Support, BoringSSL's Equal Preferencen Support and ChaCha20-Poly1305 Draft Version Support.In addition to this, I have added some modules.

## 里面有些啥？

## What's inside?
```
nginx version: nginx/1.23.1
built by gcc 10.3.1 20210424 (Alpine 10.3.1_git20210424) 
built with OpenSSL 1.1.1q  5 Jul 2022
TLS SNI support enabled
configure arguments: 
        --prefix=/etc/nginx
        --sbin-path=/usr/sbin/nginx
        --modules-path=/usr/lib/nginx/modules
        --conf-path=/etc/nginx/nginx.conf
        --error-log-path=/var/log/nginx/error.log
        --http-log-path=/var/log/nginx/access.log
        --pid-path=/var/run/nginx.pid
        --lock-path=/var/run/nginx.lock
        --http-client-body-temp-path=/var/cache/nginx/client_temp
        --http-proxy-temp-path=/var/cache/nginx/proxy_temp
        --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp
        --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp
        --http-scgi-temp-path=/var/cache/nginx/scgi_temp
        --user=nginx
        --group=nginx
        --with-http_ssl_module
        --with-http_realip_module
        --with-http_addition_module
        --with-http_sub_module
        --with-http_dav_module
        --with-http_flv_module
        --with-http_mp4_module
        --with-http_gunzip_module
        --with-http_gzip_static_module
        --with-http_random_index_module
        --with-http_secure_link_module 
        --with-http_stub_status_module
        --with-http_auth_request_module 
        --with-http_xslt_module=dynamic 
        --with-http_image_filter_module=dynamic 
        --with-http_geoip_module=dynamic 
        --with-threads 
        --with-stream 
        --with-stream_ssl_module 
        --with-stream_ssl_preread_module 
        --with-stream_realip_module
        --with-stream_geoip_module=dynamic 
        --with-http_slice_module 
        --with-mail 
        --with-mail_ssl_module 
        --with-compat 
        --with-file-aio 
        --with-http_v2_module 
        --with-http_v2_hpack_enc 
        --with-zlib=/usr/src/zlib 
        --with-pcre=/usr/src/pcre-8.45 
        --with-pcre-jit 
        --with-libatomic=/usr/src/libatomic_ops-7.6.12 
        --add-module=/usr/src/headers-more-nginx-module-0.34 
        --add-module=/usr/src/ngx-fancyindex-0.5.2 
        --add-module=/usr/src/ngx_brotli 
        --add-module=/usr/src/ngx_http_geoip2_module 
        --add-module=/usr/src/nginx-http-flv-module 
        --add-module=/usr/src/ngx_http_substitutions_filter_module 
        --with-openssl-opt='zlib enable-weak-ssl-ciphers enable-ec_nistp_64_gcc_128 -ljemalloc -Wl,-flto'
```
## 咋用？
## How to use？

```
docker pull justf/nginx-http2-brotli:latest
```


### Nginx 配置
* 挂载在 /etc/nginx/main.d 中的 .conf 文件将被包含在 nginx.conf 的上下文中。（你可以在这里调用 env 指令）

* 挂载在 /etc/nginx/conf.d 中的 .conf 文件将被包含在 nginx.conf 中的 http 块中。
```
include /etc/nginx/main.d/*.conf;
...
http{
        ...;
        include /etc/nginx/conf.d/*.conf;

}
```
### Nginx Config
* `.conf` files mounted in `/etc/nginx/main.d` will be included in the `main` nginx context(e.g. you can call [`env` directive](http://nginx.org/en/docs/ngx_core_module.html#env) here)
* `.conf` files mounted in `/etc/nginx/conf.d` will be includednin the `http` nginx context.

#### SSL 配置
这个镜像里包含了了来自 [ Mozilla 的 DHparameter 文件](https://ssl-config.mozilla.org/ffdhe2048.txt)并且保存在 ```/etc/ssl/dhparam.pem``` 中。
所以你应该在你的 nginx 配置中添加如下一行：
```
ssl_dhparam /etc/ssl/dhparam.pem;
```
#### SSL Config
This image has [ DH parameters for DHE ciphers fetched from Mozilla](https://ssl-config.mozilla.org/ffdhe2048.txt) and store in `/etc/ssl/dhparam.pem`.

So you should add this line in your nginx config:
```
ssl_dhparam /etc/ssl/dhparam.pem;
```
## Thank

[@kn007/patch](https://github.com/kn007/patch)

[@akafeng/docker-nginx](https://github.com/akafeng/docker-nginx)

[@macbre/docker-nginx-http3](https://www.github.com/macbre/docker-nginx-http3)