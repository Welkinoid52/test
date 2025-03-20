# test
A sample node.js project having mongo and redis.
After cloning this project on local machine; running it successfully; dockerfile is created to containerize the application.
Later Docker-composefile is created.
jenkins container is created as master, ports exposed to local machine 0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp
Jenkins-slave ec2 instance is created with port exposed shown in image and below is startup script(also add jenkins agent)

   #!/bin/bash
  sudo dnf update
  sudo dnf install java-17-amazon-corretto -y
  sudo dnf install docker -y
  sudo systemctl enable docker
  sudo systemctl start docker
  sudo yum install git -y
  sudo mkdir /home/ec2-user/jenkins
  cd /home/ec2-user/jenkins
  
  sudo wget https://github.com/docker/compose/releases/latest/download/docker-compose -o /usr/local/lib/docker/cli-plugins/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  sudo usermod -aG docker ec2-user
  newgrp docker

On Jenkins master the node created must be up, create  new item -> pipeline, mention github, paste jenkinfile, save, run.
