---
---

## 웹 서버
### TOMCAT

### Jetty

### NginX - proxy Server

- /etc/nginx/nginx.conf 초기 상태에서는 localhost:80 에 다음과 같이 브라우저에서 확인되었다.


- /etc/nginx/nginx.conf 파일의 내용을 다음과 같이 수정 후 
java project 에서 tomcat 서버를 8080 포트에 연결 후 브라우저에서 확인

```
    server {
        listen       80;
        listen       [::]:80;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            root    html;
            index   index.html index.htm;
            proxy_pass http://localhost:8080; # 요청을 8080 포트로 넘깁니다.
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
        }

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }
```


### NginX - Load Balancer

- 빌드 후 
    - java -jar sample-0.0.1-SNAPSHOT.jar
    - java -Dserver.port=8081 -jar sample-0.0.1-SNAPSHOT.jar

