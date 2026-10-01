# EEC 174AY Lab 1 Report

## 1. SSH

(a) What is the purpose of port forwarding between your laptop, the course server, and the Docker container?

### answer:  The purpose of port forwarding is allowing me to use a program running on the course server from my own laptop. In this lab, Jupyter runs inside the Docker container on the server, but I access it through a browser on my laptop. The SSH tunnel connects the port on my laptop to the assigned port on the server, so I can use Jupyter through localhost.

## 2. Git and GitHub

(a) What is a Git repository? Explain specifically why you would track your code in a repository.
### answer: A Git repository is a folder where Git tracks changes made to files over time. It is useful for tracking code because I can see the history of my work, recover older versions if I make a mistake, and keep a backup of my project on GitHub.

(b) Explain what a branch is in Git. Why are branches useful when a team works on one project?
### answer: A branch is a separate version of a project where changes can be made without affecting the main version. Branches are useful in team projects because different people can work on different parts of the project at the same time. Later, their changes can be merged together.

(c) What is the default branch (commonly named main)? What is its role in a software project?
### answer: The main branch is usually the primary version of the project. It normally contains the stable or most current version of the code. Other branches can be used for development, and finished changes can later be merged into main.

(d) Explain what a pull request is and why it is important. Briefly explain a typical collaborative software-development cycle using Git and GitHub.
### answer: A pull request is a request to merge changes from one branch into another, usually into main. It is useful because other team members can review the code, discuss the changes, and check for problems before merging. A common workflow is to create a branch, make changes, commit them, push the branch to GitHub, create a pull request, review the changes, and then merge them into main.

## 3. Docker

(a) In your own words, explain why Docker is useful for programmers. Discuss the ways Docker can save development time.
### answer: Docker is useful because it gives programmers a consistent environment with the software, libraries, and dependencies needed for a project. This can save time because programmers do not need to install/configure everything on their own on every computer. It also helps avoid problems where code works on one machine but not on another.

(b) Explain the difference between a Docker image and a Docker container.
### answer: A Docker image is like a template that contains the software and environment needed for a project. A Docker container is a running instance of that image. One image can be used to create multiple containers.

(c) Explain how Docker can resolve a dependency conflict between a computer-vision program and a control program being developed on the same machine.
### answer: If a computer-vision program and a control program need different versions of the same library, Docker can place them in separate containers. Each container can have its own dependencies.

(d) Can Docker be used to support Linux software on a Windows computer? Explain the role of the Linux environment used by Docker Desktop.
### answer: Yes, Docker can support Linux software on a Windows computer. Docker Desktop provides a Linux environment that allows Linux-based containers to run even though the main operating system is Windows.

(e) Can Docker support development of the same project on different machines? Explain.
### answer: Yes, Docker can support development of the same project on different machines. Since the Docker image contains the required software and dependencies, different computers can use the same environment and reduce compatibility problems.

(f) In one to three sentences, explain how to build a new Docker image from scratch.
### answer: To build a new Docker image, I would create a Dockerfile that describes the base image, packages, dependencies, and setup commands. Then I would use the docker build command to create the image.


## 4. Python

(a) Compare interpreted and compiled languages. In what situations might Python be more advantageous than C++?
### answer: A compiled language such as C++ is usually converted into machine code before the program runs, while Python is usually executed through an interpreter. C++ is often faster, but Python is usually easier and faster to write and test. Python can be more useful for quick development, data analysis, machine learning, and situations where development speed is more important than maximum execution speed.

(b) Explain what lists, dictionaries, and tuples are in Python. Give one example scenario where you would use each.
### answer: A list is an ordered collection of items that can be changed. For example, I could use a list to store sensor measurements.A dictionary stores data using key-value pairs. For example, I could use a dictionary to store a student's name, ID, and grade. A tuple is an ordered collection like a list, but it cannot be changed after it is created. For example, I could use a tuple to store fixed coordinates such as (x, y).