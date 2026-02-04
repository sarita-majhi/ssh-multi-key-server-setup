# SSH Server Setup with Multiple SSH Keys

## Project Overview

This project demonstrates how to provision and secure a remote Linux server using **key-based SSH authentication**, configure **multiple SSH keys**, GitHub Actions**.

It reflects real-world responsibilities of a **DevOps / Cloud Engineer**, focusing on **security, automation, and documentation**.

## objectives

- Provision a secure remote Linux server  
- Configure SSH access using **multiple SSH key pairs**
- Disable root login and enforce key-only SSH
- SSH access verified using both keys
- Configure SSH client aliases
- Protect the server from brute-force attacks
- Configure a firewall using **UFW**

## Architecture Overview

Developer Machine
├── SSH Key Pair 1
├── SSH Key Pair 2
└── ~/.ssh/config (Aliases)
│
▼
Remote Linux Server
├── OpenSSH Server
├── authorized_keys (multiple keys)
├── Root login disabled
├── Password authentication disabled
└── Fail2Ban
└── UFW Firewall enabled
▲
│
GitHub Actions


 
# Create SSH Keys
```Bash
ssh-keygen 
type keyname
default file location
ls ~/ssh/
#-----------------------------------

# Connect SSH Keys
```Bash
ssh -i ~/.ssh/key_1 user@<server-ip>
ssh -i ~/.ssh/key_2 user@<server-ip>
#____________________________________

#SSH Client Configuration(Aliases)
nano ~/.ssh/config

Host myserver
    HostName <server-ip>
    User ubuntu
    IdentityFile ~/.ssh/key_1

Host myserver2
    HostName <server-ip>
    User ubuntu
    IdentityFile ~/.ssh/key_2
#_____________________________________


# Connect using:
```Bash
ssh myserver
ssh myserver2
#______________________________________


# Disable Root Login & Enforce Key-Only SSH
sudo nano /etc/ssh/sshd_config

PasswordAuthentication no
PubkeyAuthentication yes

```Bash
sudo systemctl restart sshd
#_________________________________________


#Firewall Configuration with UFW
```Bash
sudo apt update
sudo apt install ufw -y
sudo ufw allow OpenSSH  **allow ssh**
sudo ufw enable
sudo ufw status verbose
#___________________________________________


#Security Hardening-Fail2Ban
```Bash
sudo apt update
sudo apt install fail2ban -y
sudo systemctl enabke fail2ban
sudo systemctl start fail2ban

sudo systemctl status fail2ban
#_____________________________________________


#Check SSH Port and Firewall
sudo ss -tulpn | grep :22 
sudo ufw status
sudo ufw allow ssh
sudo ufw reload
#______________________________________________












