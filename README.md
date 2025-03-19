# linux-ngnix-config


```
sudo vi /etc/nginx/conf.d/tomcat.conf

upstream tomcat {
        ip_hash;
        server localhost:1234;
}

server{
        listen 80;
        server_name domainname;

        location / {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Ror $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;

                proxy_pass http://tomcat;
                proxy_redirect off;
                charset utf-8;
                client_max_body_size 100M;
        }
}




sudo vi /etc/nginx/sites-available/reverse-proxy.conf

server {
        listen 80;
        listen [::]:80;
        server_name domainname;

        access_log /var/log/nginx/domain1.access.log;
        error_log /var/log/nginx/domain1.error.log;

        location / {
                 proxy_pass http://localhost:1234;
        }
}
server {
        listen 80;
        listen [::]:80;
        server_name domainname;

        root /path/dist;

        access_log /var/log/nginx/domain2.access.log;
        error_log /var/log/nginx/domain2.error.log;
        location / {
               try_files $uri $uri/ /index.html;
        }
}


```
