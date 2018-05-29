# Docker-Compose
Docker Compose
- Compose là công cụ giúp định nghĩa và khởi chạy multi-container Docker applications.
- Chỉ với một câu lệnh, ta có thể dễ dàng create và start toàn bộ các services phục vụ cho việc chạy ứng dụng.

- Việc sử dụng Docker Compose được tóm lược trong 3 bước cơ bản sau:

- Khai báo app’s environment với Dockerfile.
- Khai báo các services cần thiết để chạy app trong docker-compose.yml.
- Run docker-compose up và Compose sẽ start và run app.
# 1. Cài đặt

- Install using pip

```$ pip install docker-compose```

Hoặc bạn có thể sử dụng cách khác:

- Install as a container

```$ curl -L https://github.com/docker/compose/releases/download/1.11.2/run.sh > /usr/local/bin/docker-compose```<br>
```$ chmod +x /usr/local/bin/docker-compose```
# 2. Ví dụ chạy wordpress.
- Chúng ta sẽ tạo ra 2 containers, 1 containers chứa mã nguồn wordpress và 1 containers chưa cơ sở dữ liệu mysql. Bằng cách định nghĩa trong file compose. Chỉ với 1 dòng lệnh khởi tạo, docker sẽ lập tức tạo ra 2 containers và sẵn sàng cho chúng ta dựng lên wordpress, một cách nhanh chóng.
- Đoạn mã compose: Viết theo cú pháp YAML.

```
version: '2'
services:
   db:
     image: mysql:5.7
     volumes:
       - ./data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: wordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_PASSWORD: wordpress
       
