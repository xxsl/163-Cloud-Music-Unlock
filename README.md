# 163-Cloud-Music-Unlock
Unlock 163 cloud music by server &amp; proxy mode，解锁版权以及地域限制

## For OpenWRT or 其他借助DNS实现的Unblocker用户
```
配置添加 address=/music.163.com/[serverip]
```
## For Android & IOS 越狱用户
```
hosts添加 [serverip] music.163.com
```
## For Android 未越狱越狱用户
```
走 shadowsocks-android
服务器hosts添加 [serverip] music.163.com
```
## For IOS 未越狱越狱用户
```
*需要Surge
规则中增加Local DNS Map [serverip] music.163.com
```

## 以server方式部署
安装Python环境并运行
```
sudo apt-get install python-dev python-pip
sudo pip install tornado
python music163.py -m server -p 16163 -a 127.0.0.1
```
Nginx代理服务器参考配置
```
server {
    listen 0.0.0.0:80;
    server_name music.163.com;
    access_log /var/log/nginx/music.163.log;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header HOST $http_host;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://127.0.0.1:16163;
        proxy_redirect off;
    }
}

```

## 以proxy方式部署
在Winodows客户端中可以设置代理服务器，指向脚本基本，脚本可在本地运行