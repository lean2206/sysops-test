# SysOps Test - Marfeel

This project sets up an automated infrastructure using Ansible and Vagrant on a Windows environment. Below is a description of the folder structure and the steps to run the scripts.

## Folder Structure

- **.vagrant/**: This folder is used by Vagrant to store files and configurations related to virtual machines.
  
- **roles/**: Directory containing different Ansible roles, organized into subdirectories based on their functionality:
  - **create-network/tasks/**: Contains the tasks for setting up the shared network in the infrastructure.
    - `main.yml`: Main file containing tasks for network configuration.
  - **echoserver/tasks/**: Includes tasks for setting up several echo server containers.
    - `main.yml`: Main file containing tasks for echo server setup.
  - **folders/tasks/**: Manages the creation and configuration of necessary folders.
    - `main.yml`: Main file containing tasks for folder setup.
  - **haproxy/tasks/**: Contains tasks for setting up an HAProxy container.
    - `main.yml`: Main file containing tasks for HAProxy configuration.
  - **nginx/tasks/**: Includes tasks for setting up several Nginx containers.
    - `main.yml`: Main file containing tasks for Nginx setup.
    - `nginx.conf.j2`: Nginx configuration template.

- **ansible.cfg**: Ansible configuration file that defines global settings like the inventory path, user settings, etc.

- **infrastructure.yml**: Ansible playbook that defines and runs the necessary roles to configure the entire infrastructure.

- **setup.yml**: Ansible playbook for initial setup (docker, docker-compose, permissions, etc).

- **Vagrantfile**: Vagrant configuration file that defines the virtual machine requested to host the infrastructure

## Prerequisites

Before running this project, make sure you have the following software installed on your Windows system:

- [Vagrant](https://www.vagrantup.com/downloads) v2.4.1
- [VirtualBox](https://www.virtualbox.org/) v.7.0.20


## Execution

Follow these steps to run the project on a Windows machine:

1. **Configure the variables in the infrastructure.yml**:
    You can specify the number of echoservers and nginx containers you want to be deployed changing the following variables:
    echo_server_count 
    nginx_server_count 

2. **Start the virtual machines with Vagrant**:
    ```
    vagrant up
    ```
    This will create and start the virtual machines defined in the `Vagrantfile`.

4. **Login to the virtual machine**:
    ```
    vagrant ssh
    ```
4. **Verify the setup**:
    Once the virtual machine is up and running and both setup and infrastructure are done, you can test the infrastructure as it follows:
    ```
    curl http://localhost/api #to test the echoservers
    curl http://localhost/statics/<any_path_you_want> #to test the nginx servers 
    ```



