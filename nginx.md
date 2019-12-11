**nginx配置图片裁剪**

```shell
# 1.安装必要的包
yum -y install gcc automake autoconf libtool make gcc gcc-c++

# 2.安装PCRE库
cd ~
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.43.tar.gz 
tar -zxvf pcre-8.43.tar.gz
cd pcre-8.43
./configure
make && make install

# 3.安装zlib库
cd ~
wget http://zlib.net/zlib-1.2.11.tar.gz
tar -zxvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make && make install

# 4.安装GD
yum install gd-devel -y
yum -y install openssl openssl-devel

# 5.安装nginx
cd ~
wget http://nginx.org/download/nginx-1.16.0.tar.gz
tar -zxvf nginx-x.x.x.tar.gz
cd nginx-x.x.x
./configure --sbin-path=/usr/local/nginx/nginx --conf-path=/usr/local/nginx/nginx.conf --pid-path=/usr/local/nginx/nginx.pid --with-http_ssl_module --with-pcre=../pcre-8.43 --with-zlib=../zlib-1.2.11 --with-http_image_filter_module
make && make install

```

设置nginx开启启动

```shell
cd /lib/systemd/system/
vim nginx.service
#复制下面内容
[Unit]
Description=nginx service
After=network.target 
   
[Service] 
Type=forking 
ExecStart=/usr/local/nginx/nginx
ExecReload=/usr/local/nginx/nginx -s reload
ExecStop=/usr/local/nginx/nginx -s quit
PrivateTmp=true 
   
[Install] 
WantedBy=multi-user.target

# 加入开机自启动
systemctl enable nginx
# 删除开机自启动
systemctl disable nginx
```

niginx配置

```nginx

server {
    listen       80;
    server_name  自己的图片网站域名;
 
    # http://xxx.com/1.jpg
    location / {
        root   图片所在位置;
    }
 
    # http://xxx.com/1.jpg!100x100
    location ~* /(.+)\.(jpg|jpeg|gif|png)!(\d+)x(\d+)$ {
        set $w $3;
        set $h $4;
        
        #这里一定要写
        root 图片所在位置;
        image_filter crop $w $h;
        image_filter_buffer  10M;
        
        try_files /$1.$2  /notfound.jpg;
    } 
} 
```

