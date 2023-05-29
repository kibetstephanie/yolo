# Learning DevOps Practices

Learn simple DevOps practices with different DevOps tools.


## 1. Containerization

 Create containers for each of the services in the app using Docker
 ## Steps
 1. Create Dockerfile

    This will define how to build the specific Image.

    Build the image
    ```
     sudo docker build -t <name_of_image> .
     ```
    Run the image
    ```
     sudo docker run -d -p <port> <name_of_image>
     ```
        


 2. Create the docker-compose file
     
     We will use it to document and configure all of the application's service dependencies. We have 5 services
    1. database - define database dependancies
    2. backend - define backend dependancies
    3. client - define client side dependancies
    4. volumes - to store persistent data
    5. networks - connect the backend and client images together
    
    Run the docker compose file
    ```
     docker compose up
     ```
	 
 3. Push to docker hub

    Login to Docker Hub from the terminal
      ```
      sudo docker login
      ```
    Version the new image by giving it a new name and tag
   
      ```
      sudo docker tag {old name of image}:{old tag of image} {docker username}/{new name of image}:{new tag of image}
      ```
    Push the new Image  to Docker Hub
   
      ```
      sudo docker push {docker username}/{new name of image}:{new tag of image}
      ```
 