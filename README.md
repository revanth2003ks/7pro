# 7pro

Playbook.yml File

- name: Configure Web Server
  hosts: webservers
  become: true
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: latest

    - name: Start and enable Apache
      service:
        name: httpd
        state: started
        enabled: true

    - name: Create a custom index.html
      copy: 
        dest: /var/www/html/index.html
        content: "<h1>Hello from Ansible Web Server!</h1>"

- name: Configure DB Server
  hosts: dbservers
  become: true
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: latest

    - name: Start and enable Apache
      service:
        name: httpd
        state: started
        enabled: true


----------------------------------------------
C:\VagrantProject\ansible-controller>vagrant init centos/7

C:\VagrantProject\ansible-controller>vagrant ssh

C:\VagrantProject\ansible-controller>vagrant up

C:\VagrantProject\ansible-controller>vagrant provision

C:\VagrantProject\ansible-controller>vagrant ssh

[vagrant@controller ~]$ ls
ansible-project
[vagrant@controller ~]$ cd ansible-project
[vagrant@controller ansible-project]$ ls
hosts  playbook.yml
[vagrant@controller ansible-project]$ vi playbook.yml
[vagrant@controller ansible-project]$ exit
logout

C:\VagrantProject\ansible-controller>cd ansible-hosts
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant init centos/7
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant provision
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant up
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant provision
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant status
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant ssh
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant ssh web
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant ssh db
C:\VagrantProject\ansible-controller\ansible-hosts>vagrant status
C:\VagrantProject\ansible-controller\ansible-hosts>cd ..
C:\VagrantProject\ansible-controller>vagrant ssh
Last login: Fri Jun  6 09:34:41 2025 from 10.0.2.2

[vagrant@controller ~]$ cd ansible-project

[vagrant@controller ansible-project]$ ansible all -m ping -i hosts

192.168.33.11 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.33.10 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
[vagrant@controller ansible-project]$ ansible-playbook -i hosts playbook.yml


192.168.33.10              : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.33.11   
