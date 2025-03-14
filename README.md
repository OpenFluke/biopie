# Setup ssh

```
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

```
ssh-copy-id open@192.168.0.240
ssh-copy-id open@192.168.0.241
ssh-copy-id open@192.168.0.243
```

# Config the inventory.ini example

```
[raspberry_pis]
pi_240 ansible_host=192.168.0.240 ansible_user=open
pi_241 ansible_host=192.168.0.241 ansible_user=open
pi_243 ansible_host=192.168.0.243 ansible_user=open
```

# Test

```
ssh open@192.168.0.241
```

# Updates the system & installs podman n unzip

Fresh System (Minimal updates) → ~5-10 minutes
Light Updates (Few pending packages) → ~10-15 minutes
Heavy Updates (Many packages, kernel updates, major upgrades) → ~20-40 minutes

```
ansible-playbook -i inventory.ini update_and_install_podman.yml
```

or asking for pwd for sudo

```
ansible-playbook -i inventory.ini update_and_install_podman.yml -K
```

# Copy files to servers

```
ansible-playbook -i inventory.ini copy_biofoundry_files.yml
```

# Check if podman works on a server if you want

SSH to a server

```
ssh open@192.168.0.241
```

cd /BioFoundry

```
cd BioFoundry/
```

Run test of pod

```
podman-compose up
```

```
podman-compose down
```

# Start n stop all pods up

```
ansible-playbook -i inventory.ini start_podman.yml
```

```
ansible-playbook -i inventory.ini stop_podman.yml
```
