# FROM node:latest

# # make the 'app' folder the current working directory

# RUN npm install -g http-server
# WORKDIR /var/www
# COPY Frontend/TD/package.json /var/www/package.json

# # install project dependencies
# RUN npm install

# # copy project files and folders to the current working directory (i.e. 'app' folder)
# COPY Frontend/TD /var/www

# # build app for production with minification
# EXPOSE 3000
# CMD [ "http-server", "dist" ]
FROM node:18-alpine 
COPY ./Frontend/TD .
WORKDIR /var/www/frontend 

RUN apk update && apk upgrade && apk add bash

RUN yarn cache clean
RUN yarn install 

EXPOSE 5000 

CMD [ "bash","-c","yarn run dev" ]
