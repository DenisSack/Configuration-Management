# Static Website Deployment with Ansible
Project URL: https://roadmap.sh/projects/configuration-management


This project provides an Ansible playbook to automatically provision a web server with:

- **Base system setup** – updates, essential utilities, fail2ban, and UFW firewall.
- **Nginx** – installation and configuration as a web server.
- **Static website deployment** – uploads and extracts a tarball containing your HTML/CSS/JS files.
- **SSH key management** – adds a public key for secure remote access.

The playbook is designed to be idempotent, secure, and easy to extend.

---

## Prerequisites

- Ansible 2.9+ installed on your control machine (`pip install ansible`).
- SSH access to the target server (user with `sudo` privileges).
- The target server must be a Debian/Ubuntu system (package manager `apt`).

## Configuration

### 1. Inventory

Edit `inventory.ini` with your server details:

```ini
[webserver]
192.168.1.100 ansible_user=ubuntu ansible_become=yes

Create the files/ directory and place your artifacts there:

mkdir files


3. Customize Variables (Optional)
Each role contains a defaults/main.yml file. Override any variable by setting it in setup.yml or in group_vars/all.yml.

Common overrides:

app_web_root – Change from /var/www/mywebsite to another path.

nginx_site_name – Name of the Nginx site configuration.

ssh_user – Which user’s authorized_keys file to modify (default: root).

ansible-playbook -i inventory.ini setup.yml


# Only the app role (upload website)
ansible-playbook -i inventory.ini setup.yml --tags "app"

# Only base + nginx
ansible-playbook -i inventory.ini setup.yml --tags "base,nginx"

# Skip the app role, run everything else
ansible-playbook -i inventory.ini setup.yml --skip-tags "app"


