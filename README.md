
# Setting Up Ansible

In this guide, we'll set up Ansible on Ubuntu and configure our server, which will be CentOS 8.

## Installation

### 1. User and Hostname Configuration
- Set the hostname for convenience:
  ```shell
  sudo hostnamectl set-hostname ansible
  ```

### 2. Update and Upgrade (for Ubuntu)
- Update the package list:
  ```shell
  sudo apt update
  ```
- Upgrade packages:
  ```shell
  sudo apt upgrade -y
  ```

### 3. Hosts Configuration
- Edit the `/etc/hosts` file to add the server's private IP and name:
  ```shell
  sudo vi /etc/hosts
  ```
  - Add the following line:
    ```
    172.31.109.173  master
    ```
- Verify hostname resolution:
  ```shell
  ping master
  ```

### 4. Install Ansible
- Add the Ansible PPA repository:
  ```shell
  sudo apt-add-repository ppa:ansible/ansible
  ```
- Install Ansible:
  ```shell
  sudo apt install ansible -y
  ```

### 5. Create Ansible User
- Create the `ansible` user:
  ```shell
  sudo adduser ansible
  ```

### 6. Ansible Inventory
- Edit the Ansible inventory file `/etc/ansible/hosts`:
  ```shell
  sudo vi /etc/ansible/hosts
  ```
  - Add the following content:
    ```
    [master]
    192.12.3.2
    ```

### 7. Passwordless Login for Ansible User
- To enable passwordless login for the `ansible` user, create a sudoers file:
  ```shell
  sudo visudo -f /etc/sudoers.d/ansible-nopasswd
  ```
  - Inside the file, add the line:
    ```
    <your_user> ALL=(<target_user>) NOPASSWD:ALL
    ```
  - Set the file's permissions:
    ```shell
    sudo chmod 440 /etc/sudoers.d/ansible-nopasswd
    ```

### 8. Switch to the Ansible User
- Switch to the `ansible` user without a password:
  ```shell
  sudo -u ansible -i
  ```

### 9. Generate SSH Key
- Generate an SSH key for passwordless login:
  ```shell
  ssh-keygen
  ```

(Continue to CentOS server setup...)

## CentOS Server (continued)

(Include the steps specific to configuring a CentOS server here.)

(Once you've returned to the main server...)
### 10. Set the Server's Hostname

- Set the hostname to "ansible" or your preferred name:
  ```shell
  sudo hostnamectl set-hostname ansible
  ```
  
### 11. Create the `ansible` User
- Create the `ansible` user:
  ```shell
  sudo adduser ansible
  ```

### 12. Set a Password for the `ansible` User (if needed)
- Set a password for the `ansible` user:
  ```shell
  sudo passwd ansible
  ```

### 13. Add the `ansible` User to the `wheel` Group
- Grant the `ansible` user sudo access by adding it to the `wheel` group:
  ```shell
  sudo usermod -aG wheel ansible
  ```

### 14. Edit the Sudoers File
- Edit the sudoers file:
  ```shell
  sudo visudo
  ```
  - Add the following line to grant the `ansible` user passwordless sudo access:
    ```
    ansible		ALL=(ALL)	NOPASSWD: ALL
    ```
## Return to ansible server (main server) 
### 15. SSH Key Copy
- Inside the `ansible@ansible` user, copy your SSH key to the remote server:
  ```shell
  ssh-copy-id ansible@172.31.102.110
  ssh master
  ```

### 16. Create Ansible Inventory File
- Create an Ansible inventory file named `inventory.yaml`:
  ```shell
  vi inventory.yaml
  ```
  - Add server information:
    ```yaml
    vm:
      hosts:
        master:
          ansible_host: 172.31.109.173
    ```

### 17. Verify Inventory
- Verify that the server is in the inventory:
  ```shell
  ansible-inventory -i inventory.yaml --list
  ```

### 18. Create a Playbook for Configuration
- Create a playbook to configure the firewall, SELinux, and other settings:
  ```shell
  vi playbook.yaml
  ```
  - Add the playbook contents:
    ```yaml
    ---
    - name: Firewall
      hosts: vm
      become: yes
    
      tasks:
        - name: Allow ports
        shell: sudo firewall-cmd --permanent --add-port=5432/tcp

        - name: Reload Firewall
        shell: sudo firewall-cmd --reload

        - name: Selinux
        shell: sudo sed -i "s/SELINUX=.*/SELINUX=disabled/" /etc/selinux/config

        - name: Reload Selinux
        shell: sudo setenforce 0
    ```

### 19. Install PostgreSQL (Example)
- Create a playbook to install PostgreSQL on CentOS:
  ```shell
  vi postgres.yaml
  ```
  - Add the playbook contents:
    ```yaml
    ---
    - name: Install PostgreSQL on CentOS
      hosts: vm
      become: yes
      tasks:
        - name: Install PostgreSQL and EPEL Repository
        yum:
          name: "{{ item }}"
          state: present
        loop:
          - epel-release
          - postgresql-server
          - postgresql-contrib
        when: ansible_distribution == 'CentOS'

      - name: Initialize the PostgreSQL Database
        command: postgresql-setup initdb
        when: ansible_distribution == 'CentOS'

      - name: Start and Enable PostgreSQL Service
        systemd:
          name: postgresql
          enabled: yes
          state: started
        when: ansible_distribution == 'CentOS'
    ```

### 20. Run Ansible Playbook
- Run the PostgreSQL playbook (or other playbooks):
  ```shell
  ansible-playbook -i inventory.yaml postgres.yaml
  ```

That's it! You've successfully set up Ansible and performed various configurations on your servers.
