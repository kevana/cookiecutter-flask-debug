############################################################
# Dockerfile to build Python WSGI Application Containers
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Kevan Ahlquist

# Add the application resources URL
RUN echo "deb http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) main universe" >> /etc/apt/sources.list

# Update the sources list
RUN apt-get update

# Install basic applications
#RUN apt-get install -y tar git curl nano wget dialog net-tools build-essential

# Install Python and Basic Python Tools
RUN apt-get install -y python python-dev python-distribute python-pip

# Copy the application folder inside the container
ADD . /{{cookiecutter.app_name}}

# Get pip to download and install requirements:
RUN ls /{{cookiecutter.app_name}}
RUN pip install -r /{{cookiecutter.app_name}}/requirements/prod.txt
RUN pip install gunicorn

# Expose ports
EXPOSE 8000

# Set the default directory where CMD will execute
WORKDIR /{{cookiecutter.app_name}}

# Set the default command to execute    
# when creating a new container
CMD gunicorn -b 0.0.0.0:8000 -w 2 {{cookiecutter.app_name}}.app:create_app\(\) 2>&1
