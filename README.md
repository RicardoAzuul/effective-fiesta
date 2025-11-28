# effective-fiesta
Repo for Debian config using Ansible

## Overview

This Ansible playbook configures a Debian server with:
- System updates and upgrades
- SSH server installation and configuration (with password authentication enabled)
- Docker installation
- Pihole container for DNS filtering
- Jellyfin container for media streaming

## Prerequisites

- Ansible installed on the control machine
- SSH access to the target Debian server
- Sudo privileges on the target server

## Usage

1. Copy the inventory example and add your hosts:
```bash
cp inventory.example inventory
```

2. Edit the inventory file with your Debian server details:
```ini
[debian]
192.168.1.100 ansible_user=your_user
```

3. Run the playbook:
```bash
ansible-playbook site.yml -e "docker_pihole_password=your_secure_password"
```

Or with additional custom variables:
```bash
ansible-playbook site.yml -e "docker_pihole_password=your_secure_password" -e "docker_timezone=America/New_York"
```

## Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `docker_timezone` | `UTC` | Timezone for containers |
| `docker_pihole_password` | (required) | Pihole web interface password |
| `docker_jellyfin_media_path` | `/media` | Path to media files for Jellyfin |

## Ports

The following ports are exposed:
- **22** - SSH
- **53** (TCP/UDP) - Pihole DNS
- **80** - Pihole web interface
- **8096** - Jellyfin web interface

## Security Note

The `docker_pihole_password` variable must be set when running the playbook. Always use a secure password in production environments.
