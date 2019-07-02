
##---------------------- 部署到 docker -----------------------------
------- 1. build --------------
$ npm run build
------- 2. 配置 Dockerfile ------------

FROM nginx:alpine
RUN mkdir /app
COPY  ./dist /app
COPY nginx.conf /etc/nginx/nginx.conf

-------- 3. 配置 nginx.conf --------------------

user  nginx;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
events {
  worker_connections  1024;
}
http {
  include       /etc/nginx/mime.types;
  default_type  application/octet-stream;
  log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';
  access_log  /var/log/nginx/access.log  main;
  sendfile        on;
  keepalive_timeout  65;
  server {
    listen       8080;
    server_name  localhost;
    location / {
      root   /app;
      index  index.html;
      try_files $uri $uri/ /index.html;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
      root   /usr/share/nginx/html;
    }
  }
}

------------- 4. 生成镜像 ---------------------------
$ docker build . -t my-app
$ docker push my-app     // 推送到远程镜像服务器
-------------- 5. 运行 -----------------------------
docker run -d -p 8080:8080 my-app


##---------------------- 部署到 express -----------------------------
# dist文件部署到express
----------- 安装express-generator生成器 --------
1. $ npm install express-generator -g
--------- - 创建一个express项目 ---------------
2. $ express expressDemo

 $ cd expressDemo                                                                               

 $ npm install     
3. 把dist目录下的所有文件复制到express项目的public文件夹下

4. 然后运行 $ npm start 启动expressDemo

打开浏览器，输入 http://localhost:3000 , 就可以看到效果了