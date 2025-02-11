# Set Up Kubernetes Deployment

**Author:** Gilbert Emodi  
**Email:** zemodi99@gmail.com

---

![Image](https://github.com/GilbertEmodi/Set-Up-Kubernetes-Deployment-part2-/blob/main/eks2-architecture-complete.png)

---

## Introducing Today's Project!

In this project, I will prepare a backend app for Kubernetes deployment. This is because Kubernetes deployment requires apps to be containerized and for there to be a container image. This project will get us to create that container image.

### Tools and concepts

'I used Amazon EKS, Git, Docker, and Amazon ECR to prepare a backend app for deployment with Kubernetes. This involved setting up an EKS cluster, cloning code from GitHub, building and pushing a docker image to Amazon ECR.

### Project reflection

This project took me approximately 1hours. The most challenging part was running into the AWS CLI errors in the begining. I had make sure the Linux environment was perfectly set up to interact with Docker and AWS services like EKS and ECR.

Something new that I learnt from this experience was how to properly set up the AWS CLI to run linux commands that help streamline my Kubernetes cluster deployment.

---

## What I'm deploying

To set up this project, I launched a Kubernetes cluster. Steps I took to do this included launching an EC2 instance, installing "eksctl" by running the command, and modifying the IAM Role for my instance so that it has "AdministratorAccess". 

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means the logic/brain that defines how the app "works". I retrieved backend code by cloning it from a GitHub repository.

![Image](https://github.com/GilbertEmodi/Set-Up-Kubernetes-Deployment-part2-/blob/main/1-Backend%20Cloned.JPG)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because Kubernetes needs a container image for a successful app deployment. At the moment I haven't prepared a container image yet, (just raw code).

When I tried to build a Docker image of the backend, I ran into a permissions error because I am logged into the EC2 instance as "ec2-user" (created automatically from the EC2's AMI). "ec2-user" can not run root-user level commands without "sudo"

To solve the permissions error, I added the ec2-user to the Docker group. The Docker group is a group in Linux systems that grant a user the permission to run docker commands, (like docker build).

![Image](https://github.com/GilbertEmodi/Set-Up-Kubernetes-Deployment-part2-/blob/main/2-Docker%20Image%20Building.JPG)

---

## Container Registry

I'm using Amazon ECR in this project to store our container image. ECR is a good choice for the job because it is an AWS service and integrates well with other AWS services like EKS. This makes deploying the app even faster for engineers & devs.

Container registries like Amazon ECR are great for Kubernetes deployment because I get to store tagged images from a single source of truth. Users and other services can pull my latest container image without any manual downloading required.

![Image](https://github.com/GilbertEmodi/Set-Up-Kubernetes-Deployment-part2-/blob/main/3-ECR%20Repository.JPG)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learned that the app functions by extracting data from another API, but we also have our own API in "app.py" that's responsible for others wanting access to our service.

### Unpacking three key backend files

The requirements.txt file lists all the dependencies and libraries that every container needs to install when the container is created.

The Dockerfile sets up the instructions that tell Docker how it should build a container image of your backend app. It includes commands on where it can find a list of all dependencies to install (requirements.txt) and commands that automatically run

The app.py file contains three main parts: installing dependencies, formatting the data into JSON data, passing the formatted data back to the user/requester.

---

---
