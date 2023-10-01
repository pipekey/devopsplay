# Nodes configuration procedure

- Create VPS

---

- SSH in as root from srv2

```bash
ssh root@node
```

---

- Change root password

```bash
passwd
```

---

- Create ansible user

Create user with password

```bash
adduser ansible
```

Add user to sudo group

```bash
sudo usermod -aG sudo ansible
```

Copy ssh key from srv2

```bash
ssh-copy-id -i .ssh/ansible.pub ansible@node
```

Disconnect

---
