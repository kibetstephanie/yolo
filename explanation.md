# Creating my Microservice: Explanation

* First install the required technologies and run the app locally to have a feel of the applications front and back end. The instructions are found in the README.md file
* Ok now let's get started with creating the microservice 

## Dockerfile Creation
### Client Directory Image Creation

* Started with creating Dockerfile to define how to build an image for the client side of our application.
* The steps used to create the Dockerfile are as follows:

	1. Create a base image using [node](https://hub.docker.com/_/node) from Docker Hub with the 20-alpine3.16 tag version.
	2. Create an app directory for the docker image. 
	3. Copy all the dependancies needed from our local directory to the current directory of our Docker Image.
	4. Install the node packages by running npm install.
	5. Copy the local project directory to the current directory of the docker image
    6. Run the application using the `npm build` command
	7. Bind the application to a port for the docker daemon to map it.
	8. Set the host port to localhost.
    9. Set the port of the application to the bounded port.
    10. Set the base URL.
    11. Finally, use the `CMD [ "npm", "start" ]` to start the app on the client side.

* After creating the Dockerfile, I built the Image using the `sudo docker build . -t <name of image>` command. In this case the name of my image is `yolo_img`. 
* The `-t` or `--tag` flag is used to set a name  to the image.
* The run the image using the `sudo docker run -p 3000:3000 yolo_img`


### Backend Directory Image Creation

* Started with creating a Dockerfile to define how to build an image for the backend side of our application.
* The steps used are as follows:

    1. Create a base image using [node](https://hub.docker.com/_/node) from Docker Hub with the 20-alpine3.16 tag version.
    2. Create an app directory for the docker image. 
	3. Copy all the dependancies needed from our local directory to the current directory of our Docker Image.
    4. Install the node packages by running npm install.
	5. Copy the local project directory to the current directory of the docker image
    7. Bind the application to a port for the docker daemon to map it.
    8. Finally, use the `CMD [ "node", "server.js" ]` to start the app on the client side.

