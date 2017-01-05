nginx安装、启动

1. 安装pcre、zlib、openssl

（1）下载

openssl-1.0.2j.tar.gz(注，不要用1.1.0c版本）
pcre-8.39.tar.gz
zlib-1.2.10.tar.gz到/usr/local,解压

（2）进入解压目录下运行./configure或./config

（3）make & make install

2. 安装nginx

(1) 下载

lua-5.1.5.tar.gz
LuaJIT-2.1.0-beta2.tar.gz
lua-nginx-module-0.10.7.tar.gz
ngx_devel_kit-0.3.0.tar.gz
echo-nginx-module-0.60.tar.gz
到/usr/local下，分别解压
其中luajit需要编译，其它只要解压即可

cd LuaJIT-2.1.0-beta2

make PREFIX=/usr/local/luajit

make install PREFIX=/usr/local/luajit


(2) 下载nginx-1.10.2.tar.gz,并解压

(3) 编译

export LUAJIT_LIB=/usr/local/luajit/lib

export LUAJIT_INC=/usr/local/luajit/include/luajit-2.1


./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_v2_module \
--conf-path=/usr/local/nginx/conf/nginx.conf \
--pid-path=/usr/local/nginx/nginx.pid \
--with-ipv6 --with-http_gzip_static_module --with-http_realip_module --with-http_flv_module \
--with-http_ssl_module \
--with-pcre=/usr/local/pcre-8.39 \
--with-pcre-jit --with-ld-opt='-ljemalloc' \
--with-ld-opt="-Wl,-rpath,/usr/local/lib" \
--with-openssl=/usr/local/openssl-1.0.2j \
--with-zlib=/usr/local/zlib-1.2.10 \
--add-module=/usr/local/ngx_devel_kit-0.3.0 \
--add-module=/usr/local/lua-nginx-module-0.10.7 \
--add-module=/usr/local/echo-nginx-module-0.60

make & make install
