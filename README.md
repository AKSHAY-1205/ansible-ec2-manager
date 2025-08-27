# 🚀 Ansible EC2 Manager

This project demonstrates how to automate **AWS EC2 instance lifecycle tasks** using **Ansible**, including:

* Provisioning multiple EC2 instances with different operating systems
* Setting up passwordless SSH authentication from the control node
* Selectively shutting down only Ubuntu-based EC2 instances using Ansible facts

It’s designed for anyone learning **DevOps, Ansible, or AWS automation**.

---

## 📂 Project Structure

```
ansible-ec2-manager/
├── ec2_create.yaml      # Playbook to launch EC2 instances
├── ec2_stop.yaml        # Playbook to shutdown only Ubuntu EC2s
├── inventory.ini        # Static inventory file with user@host
├── group_vars/          # Stores vaulted AWS credentials
├── vault.pass           # Vault password file (ignored in .gitignore)
├── .gitignore           # Ignore sensitive or temp files
└── README.md            # Documentation
```

---

## ⚡ Features

* ☁️ Automates **EC2 lifecycle** (create, stop)
* 🔑 Supports **passwordless SSH** setup
* 🔒 Secures credentials using **Ansible Vault**
* 📦 Uses **amazon.aws** Ansible collection

---

## 🛠️ How to Use

### 1. Create EC2s

```bash
ansible-playbook -i inventory.ini ec2_create.yaml --vault-password-file vault.pass
```

### 2. Setup Passwordless SSH (if needed)

```bash
ssh-copy-id -i ~/.ssh/id_ansible.pub -o IdentityFile=~/downloads/aws-keypair.pem ubuntu@<your-ip>
```

### 3. Stop Ubuntu Only

```bash
ansible-playbook -i inventory.ini ec2_stop.yaml --vault-password-file vault.pass
```

---

## 💡 Notes

* Configure **AWS credentials** using Ansible Vault or environment variables

* Install required collection:

  ```bash
  ansible-galaxy collection install amazon.aws
  ```

* Ensure **port 22** is open for Ansible to connect to EC2s

---

## 📌 Requirements

* Ansible 2.9+
* boto3 & botocore (Python libs)
* AWS account with IAM permissions

---

## 🔒 Security Notes

* Never commit `aws-key.pem` or sensitive credentials
* Keep `vault.pass` **out of Git**
* Example `.gitignore`:

```gitignore
*.pem
vault.pass
*.log
*.retry
__pycache__/
group_vars/
```

---
## 📜 License

This project is licensed under the MIT License — you are free to use, modify, and distribute it with attribution.

---

## 👤 Author

**Akshay** — Final-year AIML student exploring DevOps automation with Ansible & AWS.
