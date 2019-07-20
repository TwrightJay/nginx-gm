# nginx-gm
集成GmSSL的nginx，支持TLS和GMTLS同时提供服务

## 使用说明
1. 配置SSL协议
2. 配置三套证书（国密签名证书、国密加密证书、其他普通证书）
3. 配置套件

## 演示配置

证书字段请自行替换

```
# HTTPS server
server {
    listen       1443 ssl;
    server_name  localhost;

    # ssl_protocols GMTLS;
    ssl_certificate      /root/Git/GmSSL/gm_test/003/sig.pem;
    ssl_certificate_key  /root/Git/GmSSL/gm_test/003/sig.key;
    ssl_certificate      /root/Git/GmSSL/gm_test/003/enc.pem;
    ssl_certificate_key  /root/Git/GmSSL/gm_test/003/enc.key;
    ssl_protocols TLSv1.2 TLSv1.3 GMTLS;
    ssl_certificate      /etc/nginx/server01.pem;
    ssl_certificate_key  /etc/nginx/server01.pem;


    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;

    ssl_ciphers "ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256:ECDHE-SM2-WITH-SMS4-GCM-SM3:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES256-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA256:ECDHE-SM2-WITH-SMS4-SHA256:ECDHE-SM2-WITH-SMS4-SM3:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES128-SHA:RSA-PSK-AES256-GCM-SHA384:DHE-PSK-AES256-GCM-SHA384:RSA-PSK-CHACHA20-POLY1305:DHE-PSK-CHACHA20-POLY1305:ECDHE-PSK-CHACHA20-POLY1305:AES256-GCM-SHA384:PSK-AES256-GCM-SHA384:PSK-CHACHA20-POLY1305:RSA-PSK-AES128-GCM-SHA256:DHE-PSK-AES128-GCM-SHA256:AES128-GCM-SHA256:PSK-AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:ECDHE-PSK-AES256-CBC-SHA384:ECDHE-PSK-AES256-CBC-SHA:SRP-RSA-AES-256-CBC-SHA:SRP-AES-256-CBC-SHA:RSA-PSK-AES256-CBC-SHA384:DHE-PSK-AES256-CBC-SHA384:RSA-PSK-AES256-CBC-SHA:DHE-PSK-AES256-CBC-SHA:AES256-SHA:PSK-AES256-CBC-SHA384:PSK-AES256-CBC-SHA:ECDHE-PSK-AES128-CBC-SHA256:ECDHE-PSK-AES128-CBC-SHA:SRP-RSA-AES-128-CBC-SHA:SRP-AES-128-CBC-SHA:RSA-PSK-AES128-CBC-SHA256:DHE-PSK-AES128-CBC-SHA256:RSA-PSK-AES128-CBC-SHA:DHE-PSK-AES128-CBC-SHA:SM9-WITH-SMS4-SM3:SM9DHE-WITH-SMS4-SM3:SM2-WITH-SMS4-SM3:SM2DHE-WITH-SMS4-SM3:AES128-SHA:RSA-WITH-SMS4-SHA1:RSA-WITH-SMS4-SM3:PSK-AES128-CBC-SHA256:PSK-AES128-CBC-SHA";
    # ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers  on;

    location / {
        root   html;
        index  index.html index.htm;
    }
}
```