# Choice of the base image on which to build each container.
-For the frontend container, I will choose the official Node.js image from Docker Hub as the base image because it has the required dependencies (Node and NPM) for the frontend app to run.

For the backend container, I will choose the official Node.js image from Docker Hub as the base image because it has the required dependencies (Node and NPM) for the backend app to run. Additionally, I will include the MongoDB image to run the database in a separate container.

# Dockerfile directives used in the creation and running of each container.
-For the frontend container, I will copy the package.json and package-lock.json files to the container, run "npm install" to install the dependencies, and then copy the rest of the code files to the container. I will also include the "npm start" command in the Dockerfile to start the frontend app.
-For the backend container, I will copy the package.json and package-lock.json files to the container, run "npm install" to install the dependencies, and then copy the rest of the code files to the container. I will also include the "npm start" command in the Dockerfile to start the backend app. 

# Docker-compose Networking (Application port allocation and a bridge network implementation) where necessary.
-I will create a bridge network in Docker Compose to allow the containers to communicate with each other. I will also allocate ports for the frontend and backend apps to run on.

# Docker-compose volume definition and usage (where necessary).
-I will define volumes in Docker Compose to persist the data in the MongoDB container. This will ensure that the added products are not lost when the container is stopped or removed.

# Git workflow used to achieve the task.
-I will follow the standard Git workflow of creating a branch for the task, committing changes, and I will merge the branch into the main branch.

# Successful running of the applications and if not, debugging measures applied.
-In case the applications do not run successfully, I will check the logs of the containers to identify any errors. I will also check the environment variables and port allocations to ensure that they are correct.

# Good practices such as Docker image tag naming standards for ease of identification of images and containers. 
-I will use Docker image tag naming standards that include the project name, version number, and the name of the container. This will make it easier to identify the images and containers.

# Vagrantfile Description
- This file contains the configuration of your virtual machine. 

* Vagrant.configure("2") do |config|
    config.vm.box = "geerlingguy/ubuntu2004"  (Specifies the base box for the VM)
    config.vm.provider "virtualbox" do |virtualbox| (Specifies the provider of the VM)
       virtualbox.memory = "2048"  (Specifies amount of memory to allocate to the VM)
       virtualbox.cpus = 2  (Specifies the number of CPUs To be allocated)
    end
    config.vm.network "forwarded_port", guest: 80, host: 8080 (Forwards port 80 on the VM to port 8080 on the host machine)
    config.vm.provision "ansible" do |ansible| (Configures ansible as the provisioning tool of choice)
      ansible.playbook = "playbook.yml" (Specifies the playbook used for provisioning)
    end
  end

# Inventory File Description
- This specifies the hosts ansible will manage.

# Playbook Description
- This file defines the tasks that ansible will execute on the managed hosts. It performs the following:

1. Installs Docker and Docker Compose
2. Clones Repository
2. Starts a backend container named 'backend' using the tyler-hera/yolo-backend:1.0.0 image.
3. Starts a client container named 'client' using the tyler-hera/yolo-client:1.0.0 image.


# IP4 EXPLANATION
## Choice of the Kubernetes Objects used for deployment 
- For this project, I chose to use Deployments for deploying both the backend and client applications.Deployments allow for easy scaling and rolling updates of the application while maintaining availability.

## Method used to expose your pods to internet traffic.
- To expose the pods to internet traffic, I used a LoadBalancer service. This provides a stable IP address that can be accessed by users outside of the Kubernetes cluster. The LoadBalancer service automatically distributes incoming traffic to the available pods. I used the --type=LoadBalancer flag to specify the type of service.

## Use-of or there-lack-of of persistent storage.
-  I used PersistentVolumeClaims to dynamically provision storage. This would allow for easy scaling and management of the storage solution.

## Git workflow used to achieve the task.
- I used a standard Git workflow. I also used descriptive commit messages to make it easy to track changes and revert to previous versions if needed.

## Successful running of the applications from the link provided in your github Repository's README.md, if not the debugging measures applied.
- To ensure that the applications run successfully, I tested them locally before deploying them to the Kubernetes cluster. But encountered errors that prevented deployment on link: http://34.67.188.23

## Good practices such as Docker image tag naming standards for ease of identification and personalization of images and containers.
- I followed Docker image tag naming standards to ensure ease of identification and personalization of images and containers.
