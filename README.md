# jenkins-docker-installation
[Jenkins](https://www.jenkins.io/) application, built by [Dockerfile](https://docs.docker.com/engine/reference/builder/), provisioned via [Docker-Compose](https://docs.docker.com/compose/install/) and hosted within a [Docker](https://www.docker.com/) container.

## Architecture

![image](https://user-images.githubusercontent.com/83971386/201360595-b5de5908-8329-45b2-9031-299b7bd9e89c.png)

## Prerequisites
* Docker installation - [steps](https://docs.docker.com/engine/install/)
* Docker-Compose setup - [steps](https://docs.docker.com/compose/)
* Virtualbox installation - [steps](https://www.virtualbox.org/wiki/Downloads) 

## Install Jenkins
### 1. Clone the Git Repository
      sudo yum install git -y 
      cd /home
      git clone https://github.com/BJWRD/jenkins-docker-installation
      cd jenkins-docker-installation
      
###   2. Run Jenkins Container
Before we begin the Jenkins Installation, we need to ensure that Docker and Docker-Compose has been installed on the VM you are using. Please follow the steps within the 'Prerequisites' section to get started.

Once Docker and Docker-Compose has been installed, execute the following Docker-Compose command to start the Jenkins container in detatched mode. This will host your Jenkins instance.

      docker-compose up -d
      
###   3. Unlocking Jenkins
After running the container you should be able to access the Jenkins application via web browser using ```http://localhost:8080``` or ```http://<host_ip>:8080```.

Initially you will notice that you are presented with a 'Unlock Jenkins' screen. To retrieve the requested 'Administrator password' you will need to enter the following docker command below to view the container logs and locate the password -
      
      docker logs <containerID>

Example:

<img width="656" alt="image" src="https://user-images.githubusercontent.com/83971386/195887709-16190167-11f1-405a-adf5-6e2537b0d7ae.png">

Once retrieved, copy and paste the password into the 'Administrator password' field -

<img width="848" alt="image" src="https://user-images.githubusercontent.com/83971386/195887952-7930b373-175c-4d99-81d6-31187fc86807.png">

###   4. Customize Jenkins
Select 'Install suggested plugins' and wait for the completed installation -

<img width="871" alt="image" src="https://user-images.githubusercontent.com/83971386/195888092-df15273c-bb37-4534-8af5-05bea6a46e3e.png">

Note: In the instance all of the plugins fail, you may need to enter the following commands to ensure a HTTP connection is established rather than HTTPS when pulling the Jenkins plugins -

      docker exec -it <containerID> bash
      sed -i 's/https/http/g' /var/jenkins_home/hudson.model.UpdateCenter.xml 
 
 Example:
 
<img width="704" alt="image" src="https://user-images.githubusercontent.com/83971386/195888177-aad8e0a2-8aa5-41ed-b440-6a039e70244f.png">

###   5. Creating Jenkins Admin User
You will then be presented with the following 'Create First Admin User' screen, enter details relevant to yourself and select 'Continue'.

<img width="781" alt="image" src="https://user-images.githubusercontent.com/83971386/195888296-ab95b2c2-dfce-4dc2-b50d-69b861c9bffe.png">

## Install Docker Pipeline Plugin 
From the Jenkins Dashboard, select the 'Manage Jenkins' option on the left-hand side, followed by 'Manage Plugins' and then the 'Available Plugins' widget.

Within the Search field, enter 'Docker Pipeline' and select the 'Install without restart'button -

<img width="731" alt="image" src="https://user-images.githubusercontent.com/83971386/195888404-2d7a605d-8bec-4e0b-9c3c-819ddcbf55b1.png">

<img width="371" alt="image" src="https://user-images.githubusercontent.com/83971386/195888471-8d6fcb01-742b-46cd-8bdb-f3549ee1b3d9.png">

## Adding Credentials
###   1. Adding Docker Hub Credentials
Before you begin looking into a Pipeline creation, it would be beneficial to add your Docker Hub and Git credentials to your Jenkins profile.

Select 'Manage Jenkins' -

<img width="199" alt="image" src="https://user-images.githubusercontent.com/83971386/195980344-fe6f3028-c6b8-4cb1-860e-ab23c5c40356.png">

Followed by 'Manage Credentials' - 

<img width="636" alt="image" src="https://user-images.githubusercontent.com/83971386/195980368-bb7bb47c-8cd3-4206-a55e-cd642a133372.png">

Select the 'Global' hyperlink -

<img width="460" alt="image" src="https://user-images.githubusercontent.com/83971386/195980385-58b72a3f-ef3a-41cc-b18d-4b3786f5d5ce.png">

And then click on 'Add Credentials', from here you can populate the following screen with your Docker Hub login credentials and save -

<img width="1213" alt="image" src="https://user-images.githubusercontent.com/83971386/195980417-df538493-b935-4331-9533-cdac898a1be7.png">

Example:
<img width="1218" alt="image" src="https://user-images.githubusercontent.com/83971386/195980445-ae882dca-9f39-4c1f-8149-87f4194be0fb.png">

## Conclusion
In this project, we have built and run a local Jenkins Docker Container and have performed the initial Jenkins installation steps which I hope will leave you in a position where you can begin to kickstart the creation of your own Jenkins CICD pipeline.

## List of tools/services used
* [Jenkins](https://www.jenkins.io/)
* [Docker](https://www.docker.com/)
* [Dockerfile](https://docs.docker.com/engine/reference/builder/)
* [Docker-Compose](https://docs.docker.com/compose/)
* [Virtualbox](https://www.virtualbox.org) 
