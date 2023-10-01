# SRV2 configuration procedure

- Create VPS

---

- SSH in as root from host

```bash
ssh root@srv2
```

---

- Change root password

```bash
passwd
```

---

- Attach Ubuntu Pro subscription (optional)  
[Get Ubuntu Pro for personal use](https://ubuntu.com/pro)

```bash
sudo apt update
sudo apt install ubuntu-advantage-tools
sudo pro attach [YOUR_TOKEN]
sudo apt upgrade
```

---

- Install basic packages

```bash
sudo apt install ufw bash-completion unattended-upgrades git curl snapd
```

---

- Configure & enable firewall (ufw)

Create rule to allow SSH

```bash
sudo ufw allow OpenSSH
```

Or allow connection only from specific address (optional, or use portknock, fail2ban, etc.)

```bash
sudo ufw allow from [YOUR_IP_ADDRESS] to any port 22 proto tcp
```

Enable firewall and show rules

```bash
sudo ufw enable
sudo ufw status
```

---

- Create sudo user

Create user

```bash
adduser [YOUR_USER]
```

Add user to sudo group

```bash
sudo usermod -aG sudo [YOUR_USER]
```

Copy ssh key (already generated) from host

```bash
ssh-copy-id -i .ssh/[YOUR_KEY].pub [YOUR_USER]@srv2
```

Disconnect as root and login as user.

---

- Configure SSH server

Use preferred editor, create and modify config file

```bash
sudo vim /etc/ssh/sshd_config.d/00-user.conf
```

and add next lines

```text
PClientAliveCountMax 2
LogLevel VERBOSE
MaxAuthTries 3
MaxSessions 2
TCPKeepAlive no
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
X11Forwarding no
AllowTcpForwarding no
AllowAgentForwarding no
AllowUsers ansible [YOUR_USER]
```

Restart sshd

```bash
sudo systemctl restart sshd
```

---

- SSH hardening  
[Ubuntu 22.04 LTS SSH hardening](https://www.sshaudit.com/hardening_guides.html#ubuntu_22_04_lts)

---

- Create SSH keys for ansible and user

Create key for ansible user without password (hit enter when asks for password)

```bash
ssh-keygen -t ed25519 -C "ansible@srv2"
```

Create key for user (user for case you need to login to nodes)

```bash
ssh-keygen -t ed25519 -C "[YOUR_USER]@srv2"
```

---

- Install ansible

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

---

- Install ansible linter (recommended)

Install pip - Python package installer  

```bash
sudo apt install python3-pip
python3 -m pip install --upgrade pip
```

Install ansible-lint

```bash
python3 -m pip install --user ansible-lint
```

---
