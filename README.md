I understand your request for formatting. Here's the content with code blocks marked by triple backticks and other sections using bullet points as requested:

```markdown
Ubuntu Server
--

* Set the hostname:
  ```
  sudo hostnamectl set-hostname ansible
  ```

* Update the package list:
  ```
  sudo apt update
  ```

* Upgrade packages:
  ```
  sudo apt upgrade -y
  ```

* Edit the `/etc/hosts` file to add the server's private IP and name:
  ```
  sudo vi /etc/hosts
  ```
  - Add the following line:
    ```
    172.31.109.173  master
    ```

* Check the hostname resolution:
  ```
  ping master
  ```

* Add the Ansible PPA repository:
  ```
  sudo apt-add-repository ppa:ansible/ansible
  ```

* Install Ansible:
  ```
  sudo apt install ansible -y
  ```

* Create the `ansible` user:
  ```
  sudo adduser ansible
  ```

* Edit the Ansible inventory file `/etc/ansible/hosts`:
  ```
  sudo vi /etc/ansible/hosts
  ```
  - Add the following content:
    ```
    [master]
    192.12.3.2
    ```

* Allow user `<your_user>` to run commands as `ansible` without a password:
  - Create a file:
    ```
    sudo visudo -f /etc/sudoers.d/ansible-nopasswd
    ```
  - Inside the file, add the line:
    ```
    <your_user> ALL=(ansible) NOPASSWD:ALL
    ```
  - Set the file's permissions:
    ```
    sudo chmod 440 /etc/sudoers.d/ansible-nopasswd
    ```

* Switch to the `ansible` user without a password:
  ```
  sudo -u ansible -i
  ```

* Generate an SSH key for passwordless login:
  ```
  ssh-keygen
  ```

CentOS Server
--

* Set the hostname:
  ```
  sudo hostnamectl set-hostname ansible
  ```

* Create the `ansible` user:
  ```
  sudo adduser ansible
  ```

* Set the password for the `ansible` user:
  ```
  sudo passwd ansible
  ```

* Add the `ansible` user to the `wheel` group for sudo access:
  ```
  sudo usermod -aG wheel ansible
  ```

* Edit the sudoers file:
  ```
  sudo visudo
  ```
  - Add the line: 
    ```
    ansible ALL=(ALL) NOPASSWD: ALL
    ```

* Return to the main server (ansible).

* Inside the `ansible@ansible` user, copy your SSH key to the remote server:
  ```
  ssh-copy-id ansible@172.31.102.110
  ```

* Create an Ansible inventory file named `inventory.yaml`:
  ```
  vi inventory.yaml
  ```
  - Add server information:
    ```yaml
    vm:
      hosts:
        master:
          ansible_host: 172.31.109.173
    ```

* Verify the server is in the inventory:
  ```
  ansible-inventory -i inventory.yaml --list
  ```

* Create a playbook to configure the firewall and SELinux:
  ```
  vi playbook.yaml
  ```
  - Add the playbook contents:
    ```yaml
    ---
    - name: Firewall and SELinux
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

* Install PostgreSQL on CentOS using a playbook:
  ```
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

* Run the PostgreSQL playbook:
  ```
  ansible-playbook -i inventory.yaml postgres.yaml
  ```
```

You can copy and paste this formatted content directly into your GitHub README.
