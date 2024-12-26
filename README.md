# Ansible Playbook for Setting up a Laravel Server

This repository contains an Ansible playbook to set up a Laravel server. You can test it locally using a Docker container.

## Description
The playbook automates the process of configuring a server for Laravel development and testing it within a Docker container.

## Steps

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Install Ansible
Ensure Ansible is installed on your local Linux OS:
```bash
sudo apt update 
sudo apt install ansible -y
```

### 3. Configure Inventory
Create a new `inventory.ini` file from the provided example and update the private key file path:
```bash
cp inventory.ini.example inventory.ini
```
Edit `inventory.ini` and set the path for `ansible_ssh_private_key_file`:
```
ansible_ssh_private_key_file=/path/to/private/key
```

### 4. Build a Virtual Ubuntu Server Using Docker
1. Navigate to the Docker folder:
   ```bash
   cd docker
   ```

2. Build the Ubuntu image if it doesn't already exist:
   ```bash
   docker build -t ssh-enabled-ubuntu-image .
   ```

3. Run the container and map port 22:
   ```bash
   docker run -d -p 2222:22 --name ubuntu-server ssh-enabled-ubuntu-image
   ```

4. Access the Ubuntu Docker container and set your SSH public key:
   ```bash
   ssh testuser@localhost -p 2222
   ```
   Add your `id_rsa.pub` to the server's authorized keys.

### 5. Run the Playbook
Execute the Ansible playbook:
```bash
ansible-playbook -i inventory.ini laravel_playbook.yml
```

## Final Check
After running the playbook, verify that all necessary tools are installed by accessing the container.
```bash
ssh testuser@localhost -p 2222
```

You're all set to use the configured Laravel server!
