Ansible example
===============

1. run workers

    cd docker
    docker-compose up
    
2. check some command
rem: you should not use relative path
export ANSIBLE_INVENTORY=./ansible_hosts
export ANSIBLE_HOST_KEY_CHECKING=false
 ansible all -i inventory.ini -a "cat /etc/hostname"  
ansible all -m ping 
ansible all -a "/bin/echo hello"
ansible all -a "cat /etc/hostname"  
ansible localhost -m ping -e 'ansible_python_interpreter="/usr/bin/env python"'

ansible-inventory webservers   --graph 

 
 
3. run playbook
ansible-playbook -i inventory.ini playbook.yml -e app_name=example -e app_version=1.0.1 -e env=test -t install

To run image:

 $  docker run --rm -i -p 1022:22 -v ~/.ssh/id_rsa.pub:/root/.ssh/authorized_keys fedora-sshd 

docker-compose.yml: 

    ssh3:
      image: pdemanget/fedora-sshd
      ports:
        - "10322:22"
      volumes:
        - "~/.ssh/id_rsa.pub:/root/.ssh/authorized_keys"
        
to login

    ssh root@127.0.0.1 -p 10322


### build info
docker build . -t fedora-sshd
docker tag 766eee1b0728 pdemanget/fedora-sshd:28
docker login --username=pdemanget 
docker push pdemanget/fedora-sshd
