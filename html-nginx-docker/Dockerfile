# Use an official Nginx base image
FROM nginx:latest
# Copy index.html and nginx.conf into the appropriate location in the container
# COPY index.html /var/www/html/
COPY ./index.html /usr/share/nginx/html/
COPY ./nginx.conf /etc/nginx/nginx.conf
# Ensure that the Nginx server is started when the container is run
CMD ["nginx", "-g", "daemon off;"]