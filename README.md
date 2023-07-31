

## compile

yum install -y pcre pcre-devel

yum install -y zlib zlib-devel

yum install -y openssl openssl-devel

vim auto/cc/conf 

modify line ngx_compile_opt="-c -g"

mkdir install

#开启-g选项 并且去掉Gcc优化
./auto/configure --with-debug --with-cc-opt='-g -O0' --prefix=/root/nginx/install

make

## install

make install

## start

vim conf/nginx.conf

modify line  user  root;

cd install

./sbin/nginx -c ../conf/nginx.conf

## keepalive test

```
from flask import Flask, Response
from werkzeug.serving import WSGIRequestHandler

app = Flask(__name__)

@app.route("/")
def index():
    return Response("Hello, World!", 200, {'Connection': 'keep-alive'})

if __name__ == '__main__':
    WSGIRequestHandler.protocol_version = "HTTP/1.1"
    app.run(host='0.0.0.0', port=8888)
```
### modify flask source code to support keepalive function

`vim /usr/local/lib/python3.9/site-packages/werkzeug/serving.py`

modify line : self.send_header("Connection", "Keep-Alive")
