# Laravel + Nginx + PHP + MariaDB – Ansible Role
**Developer:** Mina Amin

## Overview
This Ansible role automates the deployment of a complete Laravel application environment using:
- Nginx
- PHP-FPM
- MariaDB
- Composer

It prepares everything needed for production or staging environments and can be integrated into CI/CD pipelines.

## Features
- Install PHP and required Laravel extensions
- Install and configure Nginx
- Install MariaDB and create DB & user
- Install Composer
- Clone Laravel project from Git
- Run migrations and seeders
- Run Laravel optimization commands
- Set correct permissions
- Manage services (Nginx, PHP-FPM, MariaDB)

## Role Structure
```
laravel_nginx_mariadb/
├── defaults/
│   └── main.yml
├── files/
│   ├── db_script.sh
│   └── install_php.sh
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   ├── system.yml
│   ├── artisan.yml
│   ├── db.yml
│   ├── nginx.yml
│   ├── php.yml
│   └── main.yml
├── templates/
│   └── nginx.conf.j2
└── tests
    ├── inventory
	└── test.yml
```

## Requirements
- Ubuntu 20.04 or higher
- Ansible 2.10+
- Laravel project hosted on GitHub/GitLab

## Role Variables
### defaults/main.yml
```yaml
project_name: # your laravel project name
app_dir: /var/www/html/{{ project_name }}
repo_ssh: # Change to your repo SSH URL if private, else use HTTPS URL
repo_branch: # branch name
ssh_key_path: ~/.ssh/id_ed25519
server_name: # name or IP of your server
php_version: # Make Sure of the PHP version in your project, else you are lost.

db_name: #database name
db_user: #database user
db_password: #database user password
db_root_password: #database root password
```

## Example Playbook
```yaml
- hosts: server
  become: yes

  roles:
    - role: laravel_nginx_mariadb
```

## Handlers Included
- Restart/Reload Nginx

## License
MIT License

## Author
**Mina Amin**
DevOps Engineer – Automation & Cloud Enthusiast
