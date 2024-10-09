## Introduction

This project fully automates the deployment and maintenance of my homelab using Infrastructure as Code principles.  
It provisions virtual machines, services, and containers on Proxmox, configured to my personal preferences.

While the project is made according my personal preferences, you can easily run this in your environment and almost everything will work out of the box. 
You will need to modify most of the variables though since they are hardcoded.

## What it Does

1. **Proxmox Configuration:**
    - Configures the Proxmox package repositories.
    - Removes the default welcome nag message.

2. **Proxmox VM Deployment:**
    - Deploys a Debian VM for hosting Docker.
    - Creates a Debian LXC container for an SMB share.
    - Deploys a Home Assistant OS VM.

3. **Samba Configuration:**
    - Configures an SMB share for network storage.

4. **Docker Configuration:**
    - Creates Docker volumes and network.
    - Deploys Portainer for managing containers.
    - Automatically deploys Docker stacks (compose files).
    - Populates Docker volumes with necessary configuration files from predefined folders.

## Get Started

To deploy this setup, follow the steps below:

1. **Install Dependencies:**
    ```bash
    ansible-galaxy install -r requirements.yml
    ```

2. **Customize Inventory and Variables:**
   - Edit the `inventory.yml` file to include the IP addresses of your Proxmox, SMB, and Home Assistant OS (HAOS) instances.

3. **Run the Playbook:**
    ```bash
    ansible-playbook deployment.yml -i inventory.yml --vault-password-file ~/vault-pass
    ```

## Requirements

- A working **Proxmox** server.
- **Ansible** installed on your control machine.
- Customization of variables in the `inventory.yml` file:
   - Proxmox IP address.
   - SMB share IP address.
   - Home Assistant OS IP address.

## Features
* **Idempotency:** The playbook is idempotent, meaning you can run it multiple times without causing any harm or redeploying existing resources.
* **Portainer Role:** Portainer checks for missing containers and dynamically deploys them. Note that changes to the Docker Compose files will not trigger redeployment, but volume contents will be updated if necessary.
