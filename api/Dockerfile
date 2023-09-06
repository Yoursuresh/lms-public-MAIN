#by the FROM instruction we are extracting node 16 -version from dockerhub as base image
FROM node:16

#then inside container i am creating backend directory for copy the files host directory to here with RUN instruction
RUN mkdir /backend

# COPYING files from host directory to container selective(backend) directory with COPY instruction
COPY . /backend

# now i am navigating out working directory in side container with WORKDIR instruction
WORKDIR /backend

#now i am running build related commands with RUN instruction 
RUN npm install
RUN npx prisma generate
RUN npm run build

# now i am exposing port for container with EXPOSE instruction
EXPOSE 8080

#to continous-start container with CMD istruction
CMD ["npm", "start"]

