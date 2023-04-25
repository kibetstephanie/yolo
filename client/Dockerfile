#Defining the base image that we want to build from
FROM node:20-alpine3.16

#Creating an application directory
WORKDIR /app

#Install all dependancies needed to the current directory of our docker image
COPY package.json package.json

#Install all the node packages
RUN npm install

#Copy local project directory to the current directory of the docker image
COPY . .

#Bind to port 3000 for docker daemon to have it mapped
EXPOSE 3000

#Start the app
CMD [ "npm", "start" ]
