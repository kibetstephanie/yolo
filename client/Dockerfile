#Defining the base image that we want to build from
FROM node:20-alpine3.16

#Creating an application directory
WORKDIR /app

#Install all dependancies needed to the current directory of our docker image
COPY package.json ./

#Install all the node packages
RUN npm install

#Copy local project directory to the current directory of the docker image
COPY . .

#Build the application and run it
RUN npm build

#Bind to a port for docker daemon to have it mapped
EXPOSE $PORT

# Set host to localhost / the docker image
ENV NUXT_HOST=0.0.0.0

# Set app port
ENV NUXT_PORT=$PORT

# Set the base url
ENV PROXY_API=$PROXY_API

# Set the browser base url
#ENV PROXY_LOGIN=$PROXY_LOGIN

#Start the app
CMD [ "npm", "start" ]
