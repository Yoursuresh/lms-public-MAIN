#by the FROM instruction we are extracting node 16 -version from dockerhub as base image and taged with 'AS builder'
FROM node:16 AS builder

#then inside container i am creating frontend directory for copy the files host directory to here with RUN instruction
RUN mkdir /frontend

# COPYING files from host directory to container selective(frontend) directory with COPY instruction
COPY . /frontend

# now i am navigating out working directory in side container with WORKDIR instruction
WORKDIR /frontend

#now i am running build related commands with RUN instruction
RUN npm install
RUN npm run build

#now i need to take nginx web-application as webhost to host our application with FROM instruction
FROM nginx

#now i need to copy the all dependency files from 'dist' directory to nginx 'host directory' (/usr/share/nginx/html)
COPY --from=builder /frontend/dist /usr/share/nginx/html

# This is required to make nginx serve index.html proxy pass for all routes
COPY nginx.conf /etc/nginx/conf.d/default.conf

# now i am exposing port for container with EXPOSE instruction
EXPOSE 80

# If you add a custom CMD in the Dockerfile, be sure to include -g daemon off;
# in the CMD in order for nginx to stay in the foreground, so that Docker can
# track the process properly (otherwise your container will stop immediately after starting)!
CMD ["nginx", "-g", "daemon off;"]
