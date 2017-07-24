Dockerize Simple Flask App

Flask is a micro webdevelopment framework for Python based on Werkzeug, Jinja 2 and good intentions. It is easy to set up using the below command.

pip install Flask
In this tutorial you will learn how to create a simple Flask App and run it inside a docker container.

Required Software
docker (1.6.0 or above)
python 2.7 or above
Linux VM - (We used AWS Ubuntu)

Steps to Install Docker:

For this lab, I am working on AWS Ubuntu instance.
11)      Launch an AWS Instance  and  login to the system
22)      Install Docker using the below commands.
sudo apt-get -y update
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get -y update
apt-cache policy docker-ce
sudo apt-get install -y docker-ce
sudo systemctl start docker               #use stop to stop the docker
sudo usermod -aG docker username #add the user to the docker group if you wish not to use sudo every time you run docker commands with that user

Logout and login again into the docker when you complete the last step. This step is needed to run docker without sudo.
All of the above commands install docker. Sample docker commands are given below




Create a Folder and all our files should be saved in that one.

Create a new file requirements.txt and add the following line
Flask==0.10.1

Create app.py file




In the above python code there are functions to do operations like GET,PUT,POST,DELETE to and from the notes list.

Create Dockerfile with the below code

FROM ubuntu:latest
MAINTAINER Ashok
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
RUN pip install flask-api
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]


FROM   - specifies the base image you are pulling
MAINTAINER –  Maintainer the app
RUN – command to install mongodb or any other applications.
Copy – Copy local files to the container
WORKDIR – Working Directory
ENTRYPOINT -  An ENTRYPOINT helps you to configure a container that you can run as an executable.
CMD – It is used to open specific shell based on command like python, mongodb ( It runs app.py file)

Mention all the above specifications in a Dockerfile and build it using the command
Docker build –t “title” /path/to/dockerfile/

Once the image is built, run it and expose the container port to localhost.

docker run -d -p 5000:5000 --name Flakapp  bashokku/flask
docker run -d -p local_portnum:5000 –v volume_in_local:volume_in_container --name container_name  image_name



Once the image is run we can see the FlaskUI on port 5000.
