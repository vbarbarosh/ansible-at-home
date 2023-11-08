The goal of bootstraping a new server is to be able to use Ansible afterwards.

1. Create a new user (uid=1000)
2. Enable passwordless sudo
3. Add new server to local ~/.ssh/config to allow `ssh servername` to it.

```bash
adduser agent
usermod --append --groups sudo agent
echo '%sudo ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/nopasswd
chmod 400 /etc/sudoers.d/nopasswd

su agent
mkdir -p .ssh
cat > .ssh/authorized_keys << EOF
___PASTE YOUR SSH PUBLIC KEY HERE___
EOF
chmod 700 .ssh
chmod 600 .ssh/authorized_keys 
```

```ssh
Host 11.11.11.11
Hostname home.agent1
User agent
IdentityFile ~/.ssh/home/id_rsa
```

Now, ansible tool could be used through this user.
