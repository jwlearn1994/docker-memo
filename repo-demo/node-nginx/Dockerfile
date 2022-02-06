FROM node:16.13.2

RUN apt-get update && \
    apt-get install -y nginx && \
    nginx -c /etc/nginx/nginx.conf

### Add nginx.conf
ADD nginx.conf /etc/nginx/conf.d/default.conf

WORKDIR /home/node/app

### Build files
COPY package.json ./

RUN yarn

COPY . .

EXPOSE 80
