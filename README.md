![Screenshot 2025-05-03 084201](https://github.com/user-attachments/assets/edf821c3-87a3-46a8-a317-8c796509f135)# Ansible Playbook for Configuring Apache and Redis

## Overview

This Ansible playbook sets up a server with the following features:

* **Apache Web Server** configured to host two virtual hosts:

  * `tenant1.local`
  * `tenant2.local`
* Each virtual host has its own directory and homepage (`index.php`).
* Redis is used as a caching service, accessible from both sites.

## Prerequisites

1. **Ansible Installed**: Ensure Ansible is installed on your control node.
2. **Target Host**: The target server must run a Debian-based OS (e.g., Ubuntu).
3. **Root Privileges**: The playbook requires `become: true` for certain tasks.
4. **DNS Configuration**: Add entries to `/etc/hosts` on the client machine to resolve `tenant1.local` and `tenant2.local`.

## Playbook Features

### Installed Packages

* Apache
* PHP
* Redis
* Required PHP extension: `php-redis`

### Virtual Hosts Configuration

Each virtual host is set up with its own directory and homepage:

* `tenant1.local`:

  * Document root: `/var/www/tenant1`
  * Homepage: `index.php` containing Redis connectivity test.
* `tenant2.local`:

  * Document root: `/var/www/tenant2`
  * Homepage: `index.php` containing Redis connectivity test.

### Redis Configuration

* Redis service is installed and started.
* Both websites include a PHP script to verify Redis connectivity.

### Apache Configuration

* Enables the virtual hosts: `tenant1.local` and `tenant2.local`.
* Disables the default Apache site (`000-default.conf`).

## Execution Steps

### 1. Clone or Create the Playbook

Save the playbook file with the name `setup.yml`.

### 2. Run the Playbook

Execute the playbook with the following command:

```bash
ansible-playbook setup.yml
```

### 3. Test the Setup

#### Update `/etc/hosts`

Add the following lines to the `/etc/hosts` file on your local machine:

```
127.0.0.1 tenant1.local
127.0.0.1 tenant2.local
```

#### Access the Sites

Open a browser and navigate to:

* [http://tenant1.local](http://tenant1.local)
* [http://tenant2.local](http://tenant2.local)

Both should display their respective homepages and Redis connectivity status.

### 4. Verify Redis

* Test Redis using:

  ```bash
  redis-cli ping
  ```

  Output should be `PONG`.
![Uploading Screenshot 2025-[Uploading playbook.yml…]()05-03 084201.png…]()

## Conclusion

This playbook automates the setup of a basic web server with virtual hosts and caching support. Modify it further to suit your project needs.
