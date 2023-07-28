

## compile

yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum install -y openssl openssl-devel

vim auto/cc/conf 

to
ngx_compile_opt="-c -g"


mkdir install
./auto/configure --prefix=install

make

## install

make install

## start

vim conf/nginx.conf
modify line
user  root;

cd install
./sbin/nginx -c ../conf/nginx.conf
