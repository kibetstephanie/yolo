# Creating a Microservice: Explanation

* First install the required technologies and run the app locally to have a feel of the applications front and back end. The instructions are found in the README.md file
* Ok now let's get started with creating the microservice 


## 1. Dockerfile Creation
### Client Directory Image Creation

* Started with creating Dockerfile to define how to build an image for the client side of our application.
* The steps used to create the Dockerfile are as follows:

	1. Create a base image using [node](https://hub.docker.com/_/node) from Docker Hub with the `20-alpine3.16` tag version.
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

* After creating the Dockerfile, I built the Image using the `sudo docker build . -t <name of image>` command. In this case the name of my image is `yolo_client`. 
* The `-t` or `--tag` flag is used to set a name  to the image.
* The run the image using the `sudo docker run -p 3000:3000 yolo_client`
* Notice that the image will run on port 3000.
* You can find the client dockerfile [here](https://github.com/kibetstephanie/yolo/blob/master/client/Dockerfile)


### Backend Directory Image Creation

* Started with creating a Dockerfile to define how to build an image for the backend side of our application.
* The steps used are as follows:

    1. Create a base image using [node](https://hub.docker.com/_/node) from Docker Hub with the `20-alpine3.16` tag version.
    2. Create an app directory for the docker image. 
	3. Copy all the dependancies needed from our local directory to the current directory of our Docker Image.
    4. Install the node packages by running npm install.
	5. Copy the local project directory to the current directory of the docker image
    7. Bind the application to a port for the docker daemon to map it.
    8. Finally, use the `CMD [ "npm", "start" ]` to start the app on the client side.

* After creating the Dockerfile, I built the Image using the `sudo docker build . -t <name of image>` command. In this case the name of my image is `yolo_backend`. 
* The `-t` or `--tag` flag is used to set a name  to the image.
* Then connect your database to the application. I had to create a cluster in [MongoDB](https://www.mongodb.com/) then connect it to the code in VS Code using the link provided.
* The run the image using the `sudo docker run -p 3000:3000 yolo_backend`
* Notice that the image will run on port 5000.
* You can find the backend dockerfile [here](https://github.com/kibetstephanie/yolo/blob/master/backend/Dockerfile)

* I ran both images at the same time then in the application, I added a product. It worked successfully.



## 2. Docker-compose File Creation

### Volume

* I created a volume called `yolo_yolo_vol` in the docker-compose that will persist the data created. 
* It will be used in the `database` service in my docker-compose file and data will be stored in the default path of my container.
* It is also going to use the local driver to store data.

### Containers

#### Client Side
* In the docker compose file, I created a container called `yolo_client_cont` that will build the client dockerfile hence create an image called `yolo_client`

#### Backend Side
* In the docker compose file, I created a container called `yolo_back_cont` that will build the backend dockerfile hence create an image called `yolo_backend`

#### Database Side
* In the docker compose file, I created a container called `mongo:5.0.16` that will  create an image called `yolo_db`

### Ports
* The client side is bounded to port 3000
* The backend side is bounded to port 5000
* The client side is bounded to port 27017


