EC2 Ansible Manager

This project demonstrates how to automate AWS EC2 instance lifecycle tasks using Ansible, including:

🚀 Provisioning multiple EC2 instances with different operating systems

🔑 Setting up passwordless SSH authentication from the control node

📴 Selectively shutting down only Ubuntu-based EC2 instances using facts

It’s designed as a learning project for DevOps, Ansible, and AWS automation.

📌 Project Overview
✅ What It Does

Create EC2 Instances (ec2_create.yaml)

Launches multiple EC2s in ap-south-1 region

Mix of Ubuntu and Amazon Linux instances

Tags applied for identification

Passwordless SSH Setup

Copies your public SSH key to provisioned EC2s

Enables future Ansible runs without .pem file

Stop Only Ubuntu Instances (ec2_stop.yaml)

Uses ansible_facts to filter OS family

Stops only Debian-based (Ubuntu) machines

📁 Folder Structure
ec2-ansible-manager/
├── ec2_create.yaml      # Playbook to launch EC2 instances
├── ec2_stop.yaml        # Playbook to stop only Ubuntu EC2s
├── inventory.ini        # Static inventory (user@host format)
├── group_vars/          # Encrypted variables via Ansible Vault
├── vault.pass           # Vault password file (ignored in Git)
├── README.md            # Documentation (this file)
└── .gitignore           # Ignore sensitive/temp files

🔐 Recommended .gitignore
*.pem
*.retry
*.log
vault.pass
group_vars/
__pycache__/
*.pyc
*.swp

🛠️ How to Use
1. Create EC2s
ansible-playbook -i inventory.ini ec2_create.yaml --vault-password-file vault.pass

2. Setup Passwordless SSH (if needed)
ssh-copy-id -i ~/.ssh/id_ansible.pub -o IdentityFile=~/downloads/aws-keypair.pem ubuntu@<your-ip>

3. Stop Only Ubuntu Instances
ansible-playbook -i inventory.ini ec2_stop.yaml --vault-password-file vault.pass

💡 Notes

Configure AWS credentials using Ansible Vault or environment variables.

Requires the amazon.aws collection → install it using:

ansible-galaxy collection install amazon.aws


Ensure port 22 is open for Ansible to connect.

👤 Author

Akshay — Final-year AIML student exploring DevOps & AWS automation with Ansible.
