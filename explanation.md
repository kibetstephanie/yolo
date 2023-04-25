# Creating my Microservice: Explanation

* First install the required technologies and run the app locally to have a feel of the applications front and back end. The instructions are found in the README.md file
* Ok now let's get started with creating the microservice 

## Client Side

* Started with creating Dockerfile to define how to build an image from our application.
* The steps used to create the Dockerfile are as follows:

	1. Create a base image using [node](https://hub.docker.com/_/node) from Docker Hub with the 20-alpine3.16 tag version.
	2. Create an app directory for the docker image. I experienced an error while using `WORKDIR /app`. I realized that the path to the app was wrong and used this one instead -> `WORKDIR /usr/client/src/app` .
	3. Copy all the dependancies needed from our local directory to the current directory of our Docker Image.
	4. nstall the node packages by running npm install.
	5. Copy the local project directory to the current directory of the docker image
	6. Bind the application to the port 3000 for the docker daemon to map it.
	7. Finally, use the `CMD [ "npm", "start" ]` to start the app on the client side.

* After creating the Dockerfile, I built the Image using the `sudo docker build . -t <name of image>` command. In this case the name of my image is `yolo_img`. 
* The `-t` or `--tag` flag is used to set a name  to the image.