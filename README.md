prerequesites Docker-Desktop to be installed.
1.Create a folder 'html-nginx-docker' and add
2.Creat index.html
add the following lines
<html>
    <head>

    </head>
    <body>
        <h1>Hello Docker!</h1>
    </body>
</html>

3. create a nginx.conf file and add the following lines

user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;
        # multi_accept on;
}

http {

        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ##
        # SSL Settings
        ##

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

        gzip on;

        # gzip_vary on;
        # gzip_proxied any;
        # gzip_comp_level 6;
        # gzip_buffers 16 8k;
        # gzip_http_version 1.1;
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}


#mail {
#       # See sample authentication script at:
#       # http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#       # auth_http localhost/auth.php;
#       # pop3_capabilities "TOP" "USER";
#       # imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#       server {
#               listen     localhost:110;
#               protocol   pop3;
#               proxy      on;
#       }
#
#       server {
#               listen     localhost:143;
#               protocol   imap;
#               proxy      on;
#       }
#}
4. Create a Dockerfile and add the following lines
# Use an official Nginx base image
FROM nginx:latest
# Copy index.html and nginx.conf into the appropriate location in the container
# COPY index.html /var/www/html/
COPY ./index.html /usr/share/nginx/html/
COPY ./nginx.conf /etc/nginx/nginx.conf
# Ensure that the Nginx server is started when the container is run
CMD ["nginx", "-g", "daemon off;"]

5. Start the docker-desktop
6. create docker image 
docker build -t <image_name>:<tag>
image_name: any name 
tag:version

the docker image is created
7. create a public ECR repository in aws
8.go to c drive /users/go to your user name/.docker folder/ take backup of config file and edit that original config file
After editing remove the second line from the file and save it
After that go to program files/docker/docker/resources/bin/
There will be one file with wincred wording in it.(this is a bug)

9.Then just try to run the command
 docker images
docker tag <image id from previous command> public.ecr.aws/<registry_alias from aws-ecr-site>/<name_of repo>
docker push public.ecr.aws/<registry_alias from aws-ecr-site>/<name_of_repo>

to find the image on ecr
 
 
