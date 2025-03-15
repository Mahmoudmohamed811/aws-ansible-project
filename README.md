# AWS Infrastructure Deployment with Ansible

This project automates the deployment of AWS infrastructure, an EC2 instance, a database, and an application using **Ansible**. The project follows a modular approach, leveraging separate Ansible roles to manage different aspects of the deployment.

## Project Overview
The project consists of **four Ansible roles**, each responsible for a specific task:
- **infra**: Deploys AWS infrastructure using CloudFormation.
- **setup**: Provisions and configures an EC2 instance.
- **db**: Creates and configures an RDS database instance.
- **app**: Deploys an application using Docker on the EC2 instance.

## Repository Structure
```
project-root/
│-- inventory          # Dynamic inventory file with EC2 IPs
│-- playbook.yml       # Main Ansible playbook
│-- requirements.yml   # List of external roles
│-- roles/             # Directory for roles
│   ├── infra/         # Infrastructure setup
│   ├── setup/         # EC2 instance provisioning
│   ├── db/            # Database configuration
│   ├── app/           # Application deployment
```

## Prerequisites
- **Ansible installed** (`pip install ansible`)
- **AWS credentials configured** (`aws configure`)
- **Ansible Galaxy installed roles**
  ```sh
  ansible-galaxy install -r requirements.yml
  ```

## Deployment Steps
1. **Clone the repository**
   ```sh
   git clone https://github.com/your-username/aws-ansible-project.git
   cd aws-ansible-project
   ```

2. **Install required roles**
   ```sh
   ansible-galaxy install -r requirements.yml
   ```

3. **Run the playbook**
   ```sh
   ansible-playbook playbook.yml -i inventory
   ```

## Playbook Execution
The `playbook.yml` runs the following tasks:

```yaml
- name: Deploy AWS Infrastructure with CloudFormation
  hosts: localhost
  gather_facts: no
  roles:
    - infra

- name: Setup EC2 Instance
  hosts: localhost
  gather_facts: no
  roles:
    - setup

- name: Deploy Database
  hosts: localhost
  gather_facts: no
  roles:
    - db

- name: Deploy Application
  hosts: webserver
  gather_facts: no
  become: yes
  roles:
    - app
```

## Cleaning Up Resources
To **delete** the deployed infrastructure, run:
```sh
ansible-playbook playbook.yml -i inventory --extra-vars "state=absent"
```

## Contributing
Feel free to fork this repository and contribute improvements or bug fixes.

