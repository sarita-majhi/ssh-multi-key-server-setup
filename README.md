# SSH Server Setup with Multiple SSH Keys

## Requirements Achieved
- Remote Linux server created
- Two SSH key pairs configured
- SSH access verified using both keys
- SSH aliases configured
- Fail2Ban installed (stretch goal)

## Create SSH Keys
```bash
ssh-keygen 
type keyname
default file location
ls ~/ssh/

# Connect SSH Keys
```bash
ssh -i ~/.ssh/key_1 user@<server-ip>
ssh -i ~/.ssh/key_2 user@<server-ip>

#SSH Client Configuration(Aliases)
nano /~/ssh/config

Host myserver
    HostName <server-ip>
    User ubuntu
    IdentityFile ~/.ssh/key_1

Host myserver2
    HostName <server-ip>
    User ubuntu
    IdentityFile ~/.ssh/key_2

```Bash
ssh myserver
ssh myserver2


#Security Hardening-Fail2Ban
```Bash
sudo apt update
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban

sudo systemctl status fail2ban


#Check SSH Port and Firewall
sudo ss -tulpn | grep :22 
sudo ufw status
sudo ufw allow ssh
sudo ufw reload













