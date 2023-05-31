# Learning DevOps Practices

Learn simple DevOps practices with different DevOps tools.


## 1. Containerization

 Create containers for each of the services in the app using Docker
 ## Steps
 1. Create Dockerfile

	This will define how to build the specific Image

    Build the image
    ```
     sudo docker build -t <name_of_image> .
     ```
    Run the image
    ```
     sudo docker run -d -p <port> <name_of_image>
     ```
        


 2. Create the docker-compose file
     
     It has 5 services: 
    * database - define database dependancies
    * backend - define backend dependancies
    * client - define client side dependancies
    * volumes - to store persistent data
    * networks - connect the backend and client images together
    
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

## 2. Configuration Management

## Ansible Playbook
  ## Steps
  1. Create required files
      * ansible.cfg -this states our inventory location
      * Vagrantfile 
      * hosts -this is our inventory that has the defined servers
      * playbook.yml - this has our main play
      * vars.yml - we define our variables in this file and import them into playbook.yml
  2. Initialize roles for abstraction purposes
      ```
      ansible-galaxy init <roleName>
      ```
      We will use 3 roles in this case and add them to a role folder
      1. git - Installs git
      1. docker -Installs dependencies, docker and docker-compose
      1. docker-compose -Starts our docker compose
      
  3. Run the playbook through vagrant provision
      ```
      vagrant up
      ```
      This autmatically provisions as stated in the Vagrantfile.

      ```
      vagrant provision
      ```
  4. After the play runs to completion, you can access the app through the browser
      [http://localhost:3000](http://localhost:3000)
      This is made possible by the forwarded ports added in Vagrantfile
      ```
      config.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "tcp"
      config.vm.network "forwarded_port", guest: 5000, host: 5000, protocol: "tcp"

      ```
  5. Add products to the app and confirm data persistence
  

## 3. Orchestration

## Google Kubernetes Engine

  Using the cloudshell:
  1. Clone the App
    ```
    git clone <repoName>
    ```
  2. Create a cluster
    ```
      gcloud container clusters create-auto yolo-cluster --region us-central1
    ```
  3. Deploy to GKE
    > Two objects . Deployment and Service
    
    * Deploy the resource to the cluster
        ```
        kubectl apply -f deployment.yaml
        ```
    * Create service
        ```
        kubectl apply -f service.yaml
        ```
          
  ## View Deployed app 
  In the GCP Console, under services click the link on the client service.
  ```
    http://EXTERNAL_IP
  ```
  ---