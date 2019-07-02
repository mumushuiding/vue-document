
##---------------------- 部署到 docker -----------------------------

------- 1. build --------------

$ npm run build

------- 2. 配置 Dockerfile ------------

FROM nginx:alpine

RUN mkdir /app

COPY  ./dist /app

COPY nginx.conf /etc/nginx/nginx.conf


-------- 3. 配置 nginx.conf --------------------
 见根目录的 nginx.conf

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