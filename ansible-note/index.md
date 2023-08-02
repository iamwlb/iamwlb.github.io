# Ansible Note

## 1. Introduction

Ansible is a Python-based automation tool that manages nodes over SSH and uses YAML to describe configurations. It has features like being agentless, efficient, and simple. Ansible is commonly used for automation deployment, configuration management, etc.

## 2. Installation & Configuration

### 2.1. Install Ansible

```bash
# MacOS
> brew install ansible

# CentOS  
> yum install epel-release
> yum repolist
> yum install ansible -y

# Ubuntu
> sudo apt-add-repository ppa:ansible/ansible
> sudo apt-get update
> sudo apt-get install ansible

# Pip
> pip install ansible
```

### 2.2. Configure Ansible

Edit the `/etc/ansible/ansible.cfg` file for configuration. E.g. define the inventory file, enable logging, etc.

## 3. Common Modules

Some common Ansible modules:

- **command** - Execute commands
- **copy** - Copy files
- **shell** - Execute scripts
- **yum** - Package management
- **service** - Manage services

Use `ansible-doc -l` to see all modules.

## 4. Snippets

### 4.1. Remote copy

```yaml
- name: copy file to the target host
  copy:
    src: filename
    dest: /usr/local/src/
```

### 4.2. yum

```yaml
- name: install dependencies
  yum:
    name:
      - gcc-c++
      - pcre
      - pcre-devel
      - zlib 
      - zlib-devel
      - openssl
      - openssl-devel
    state: present
```

### 4.3. Execute shell

```yaml
- name: shell
  shell: make && make install
  args:
    chdir: /usr/local/src/

- name: set script permissions
  shell: chmod +x /etc/profile.d/start-tomcat.sh
  args:
    chdir: /usr/local/src/mysql_secure_installation.sh

- name: execute mysql_secure_installation.sh
  shell: sh mysql_secure_installation.sh
  args:
    chdir: /usr/local/src/
```

### 4.4. file

```yaml
- name: create directory if it does not exist
  file:
    path: /var/www/html/yumrepository
    state: directory
    mode: '0755'

- name: create a symlink for keystone virtual host config 
  file:
    src: /usr/share/keystone/wsgi-keystone.conf
    dest: /etc/httpd/conf.d/wsgi-keystone.conf
    state: link  
```

### 4.5. service

```yaml
- name: start nginx
  shell: 'nohup /usr/local/nginx/sbin/nginx &'

- name: reload service
  systemd:
    daemon-reload: yes

- name: start and enable elasticsearch on boot
  service:
    name: elasticsearch
    state: started
    enabled: yes

- name: wait for elasticsearch to start
  wait_for:
    port: 9200
    delay: 10

- name: start service httpd if not started
  service:
    name: httpd
    state: started

- name: stop service httpd if started  
  service:
    name: httpd
    state: stopped

- name: restart service httpd in all cases
  service:
    name: httpd
    state: restarted

- name: reload service httpd in all cases
  service:
    name: httpd
    state: reloaded

- name: enable httpd service , don't touch state
  service:
    name: httpd
    enabled: yes

- name: start service foo based on running process
  service:
    name: foo
    pattern: /usr/bin/foo
    state: started

- name: restart network service for interface eth0
  service:
    name: network 
    state: restarted
    args: eth0
```

### 4.6. Variables

```yaml
# register shell result as variable
- name: verify installation
  shell: docker version
  register: dockerVersion

- name: print docker version
  debug:
    var: dockerVersion

# check if file exists
- name: register file info
  stat:
    path: "/tmp/test_file"
  register: file_path

- name: create file if it doesn't exist
  file:
    path: "/tmp/test_file"
    state: touch
  when: file_path.stat.exists == False  
```

### 4.7. environment

```yaml
- name: check 
  shell: openstack token issue
  register: openstack_token_issue
  environment:
    OS_PROJECT_DOMAIN_NAME: Default
    OS_USER_DOMAIN_NAME: Default
    OS_PROJECT_NAME: admin
    OS_USERNAME: admin
    OS_PASSWORD: admin
    OS_AUTH_URL: http://192.168.0.101:5000/v3
    OS_IDENTITY_API_VERSION: 3
    OS_IMAGE_API_VERSION: 2
  tags:
    - debug
```

### 4.8. template

```yaml
{{ yum_server_ip }}

- name: generate /etc/etcd/etcd.conf
  template:
    src: etcd.conf.j2
    dest: /etc/etcd/etcd.conf
```

```bash
[all:vars]
# yum server ip 
yum_server_ip=172.16.18.23
```

### 4.9. tags

```yaml
- name: copy file to the target host
  template:
    src: CentOS-PrivateLocal.repo.j2
    dest: /etc/yum.repos.d/CentOS-PrivateLocal.repo
  tags:
    - debug
```

```bash  
> ansible-playbook -i hosts site.yml --tags=debug
```

## 5. Common Errors

### 5.1. notify does not execute

If the source and target files are the same when copying config files, the copy command does not execute.
If the copy command does not execute, the notify will not call the handler.
The solution is to delete the existing config file first before copying.

### 5.2. Environment variables do not take effect

- For non-login shells like Ansible remote execution, environment variables in /etc/profile and ~/.bash_profile are not loaded, only ~/.bashrc and /etc/bashrc are loaded.
- If commands requiring specific environment variables need to be executed in Ansible, source ~/.bash_profile beforehand or put the environment variables in ~/.bashrc.

### 5.3. Ansible shell script does not work as expected

Problem:

```yaml
- name: start skywalking
  shell: './startup.sh'
  args:
    executable: /bin/bash
    chdir: '/usr/local/skywalking/bin/' 
```

Ansible can execute normally and returns results, but actually does not start.
It can start normally via SSH.

Solution:

```yaml
- name: start skywalking
  shell: 'nohup ./startup.sh &'
  args:
    executable: /bin/bash
    chdir: '/usr/local/skywalking/bin/'  
```

### 5.4. /usr/bin/python: not found

Problem:

```bash
> fatal: [node1]: FAILED! => {"changed": false, "module_stderr": "Shared connection to 192.168.100.111 closed.\r\n", "module_stdout": "/bin/sh: 1: /usr/bin/python: not found\r\n", "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error", "rc": 127}
```

Solution 1:

Install python on the remote host

Solution 2:

```bash
ansible_python_interpreter=/usr/bin/python3 
```

### 5.5. Ansible hangs for no reason

Problem: Ansible may hang randomly at some step during execution, even though that step has actually finished.

Solution:

```bash
> rm -rf ~/.ansible
```

