To install Jenkins using Docker, follow these steps:

**Prerequisites:**
Docker: Ensure you have Docker installed on your system. If not, download and install Docker from Docker’s official site.

## Step 1: Pull Jenkins Docker Image

- Open your terminal or command prompt.
- Run the following command to pull the Jenkins image from Docker Hub

```bash
docker pull jenkins/jenkins
```

## Step 2: Create a Docker Volume for Jenkins Data

To persist Jenkins data, you should create a Docker volume, which ensures that data (such as plugins, configurations, etc.) is not lost when you restart or delete the Jenkins container.

Run the following command:
```bash
docker volume create jenkins_home
```


## 3. Step 3: Run Jenkins Container

Now, start a Jenkins container and map the necessary ports and volumes.

Run the following command to start the container:

```bash
docker run -d --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins
```

Here’s what the command does:

- ``-d:`` Run the container in detached mode (in the background).
- ``--name jenkins:`` Name the container as ``jenkins``.
- ``-p 8080:8080:`` Maps port 8080 of your host to port 8080 of the container (Jenkins' web interface).
- ``-p 50000:50000:`` Maps port 50000 of your host to port 50000 of the container (for Jenkins agents).
- ``-v jenkins_home:/var/jenkins_home:`` Mounts the volume created earlier (``jenkins_home``) to the container’s /var/jenkins_home directory, which is where Jenkins stores its data.

## Step 4: Access Jenkins in a Web Browser
Once Jenkins is up and running, open your browser and go to ``http://localhost:8080``.



********************************************************

## Step 5: Unlock Jenkins
- Jenkins will prompt you for an **Administrator** password.
- To get the password, run the following command to view the initial password in the Jenkins container logs:


```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

```
- Copy the password from the output and paste it into the Jenkins web interface to unlock it.


## Step 6: Install Plugins and Set Up Admin User

- **Install Suggested Plugins:** After unlocking Jenkins, you’ll be prompted to either install suggested plugins or select specific plugins. For a quick setup, choose **Install suggested plugins.**

- **Create Admin User:** After the plugins are installed, you'll need to create your admin user. Fill in the required details to set up your user account.

- **Configure Jenkins URL:** Jenkins will ask you to confirm its URL. The default URL should be ``http://localhost:8080``, which you can modify if necessary.


## Step 7: Jenkins is Ready

You now have Jenkins running in a Docker container. You can begin using Jenkins to create jobs, configure pipelines, or set up CI/CD.


**********************************************

# Optional: Running Jenkins with Docker Compose

You can also use Docker Compose to simplify the process of running Jenkins with more customization (like binding different ports, adding environment variables, etc.).

- Create a ``docker-compose.yml`` file:


```yaml
version: '3'
services:
  jenkins:
    image: jenkins/jenkins
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
volumes:
  jenkins_home:

```
- **Run Docker Compose:** In the same directory as your ``docker-compose.yml`` file, run:


```bash
docker-compose up -d
```

This command will set up Jenkins using Docker Compose.

#### Managing Jenkins

**Stop the Jenkins container:**
```bash
docker stop jenkins
```
**Start the Jenkins container:**
```bash
docker start jenkins
```

You can now manage Jenkins running in Docker as needed.


*********************************************
*******************************************

- **RUN** 

``Ifconfig`` 

- Check the Ip address

``Copy the Ip address of machine``

- Go to root user

``sudo -i`` 

- Copy and paste "172.28.85.79  jenkins.local" into /etc/hosts

``echo  "172.28.85.79  jenkins.local" >> /etc/hosts``

- Ping the machine with alias "jenkins.local"

``ping jenkins.local``


- Browser the jenkins.local

``http:jenkins.local:8080``  

- check the Admin password of jenkins

``sudo cat /var/lib/jenkins/secrets/initialAdminPassword``

- Add Plugin 

``Simple theme``

``Role Base Contol``


- Trigger builds remotely (e.g., from scripts)

``http://localhost:8080/job/demo%20forth/build?token=mysecretstoken``

- Add plugin

``Build Authorization Token root``  

 Now you need to change the url base on plugin

``http://localhost:8080/buildByToken/build?job=demo%20forth&token=mysecretstoken``

For Curl url for terminal use \ intead of &

``curl http://localhost:8080/buildByToken/build?job=demo%20forth\token=mysecretstoken``
`
- SCM (Source Code Management)

  If new code is available in repository every 2 minute then job will not execute

  ``https://github.com/Hasansattar/Deploy_Container_App_on_AzureCloud_And_CICD_Github_Actions``

**Scheduled**  ``H/2 * * * *``

- Add Plugin

``Build Pipeline``

``Deploy to Container``

``Copy Artifcat``
