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

# Setup running on fedora 41

Download the zip file

```
wget https://openfluke.com/download-file/linux-alpha-0_9_0.zip
```

Install podman and podman compose

```
sudo dnf install podman-compose
```

```
sudo dnf install podman
```

Create podman-compose.yml with this code https://github.com/OpenFluke/biopie/blob/main/podman-compose_x86.yml

Make sure the the zip folder is next to the podman-compose yaml then run

```
podman-compose up
```

If all goes well you should see:
[biofoundry] | 🌍 Planet '(2, 2, 1)' added to grid (2, 2, 1)

[biofoundry] | 🌍 Planet '(2, 2, 2)' added to grid (2, 2, 2)

[biofoundry] | 🟦 Total Cubes: 0

[biofoundry] | 🟦 Total Cubes: 0
