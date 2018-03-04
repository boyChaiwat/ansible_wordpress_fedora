Install Ansible
# dbf install python2
# dnf install ansible

Set ansible hosts
# nano /etc/ansible/hosts
hosts > [localhost]
        127.0.0.1

Install SSH
# dnf install -y openssh-server
# ssh-keygen -t rsa -b 4096
# systemctl restart sshd.service
# ssh-copy-id 'ip-address'

Chack Ip Address
# ifconfig

Update Fedora
# dnf update

Next > paste file to /etc/ansible/

Run ansible setup_server.yml
# cd /etc/ansible/
# ansible-playbook -i hosts setup_server.yml

Reset the MySQL 5.7 root password in Fedora 27
1. Stop mysql:
# systemctl stop mysqld

2. Set the mySQL environment option 
# systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"

3. Start mysql usig the options you just set
# systemctl start mysqld

4. Login as root
# mysql -u root

5. Update the root user password with these mysql commands
mysql> UPDATE mysql.user SET authentication_string = PASSWORD('password') WHERE User = 'root' AND Host = 'localhost';
mysql> FLUSH PRIVILEGES;
mysql> quit;

6. Stop mysql
# systemctl stop mysqld

7. Unset the mySQL envitroment option so it starts normally next time
# systemctl unset-environment MYSQLD_OPTS

8. Start mysql normally:
# systemctl start mysqld

9. Try to login using your new password:
# mysql -u root -p

10. Set ALTER root user password
mysql> SET GLOBAL validate_password_policy=LOW;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
mysql> quit;

Run ansible setup_wordpress.yml
# cd /etc/ansible/
# ansible-playbook -i hosts setup_wordpress.yml

Open Broswer 
http://localhost/
