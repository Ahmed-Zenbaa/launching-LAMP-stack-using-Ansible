# launching-LAMP-stack-using-Ansible
# 2-Tier-App-via-Terraform
***open in raw form for better readability***
######################################################################################

	  	This Launchin LAMP stack via Ansible project
     	    	   was created By: Eng/Ahmed Zenbaa

######################################################################################

Note the following:

1)make sure to change the ip addresses of the /inventories/hosts file.
2)update ip address depending on your own managed host/s with their hostnames under [webservers].
3)put ip address of your localhost(control server) under [servers].
4)update variables in defaults folder in each role your requirementa.
5)try to manage ssh via keys to your managed hosts and your own localhost.
6)you must make sure <PERMITROOTLOGIN yes> is configured in /etc/ssh/sshd_config of each host in hosts file.
7)you can manage ssh via keys using these commands on your control server:
    *ssh-keygen -t rsa
	  *ssh-copy-id root@<ip address> (you should go this step for all ip adresses in hosts file
    *ssh root@<ip address>    #this to make sure connection is established 
8)you can run this ansible playbook using:
    *ansible-playbook lamp_stack_playbook.yml -i inventories/hosts
9)make sure you are standing in same directory as (lamp_stack_playbook.yml) or you can provide relative or absolute path from wherever you are in the system.

######################################################################################

Road-Map:

[play 1 on managed hosts]
IN apache role:
  1)install Apache & PHP module for Apache.
  2)start and enable Apache.
  3)permit traffic in default zone for Apache.
  4)if task 3 change --> reload service firewalld.
  5)copy index.php file to the managed host.

IN mysql role:
  1)Install mysql server and dependencies packages like ( python3-PyMySQL , php-mysqlnd ).
  2)Start and enable Mysql Service.
  3)permit traffic in default zone for Apache.
  4)if task 3 change --> reload service firewalld.
  5)Copy .my.cnf file to managed host for the credentials.
  6)Create a database user.
  7)Create a new database.
  8)Copy sample data ( db.php , dump.sql )to managed host.
  9)Insert sample data.
  10)Restart Apache.
  11)copy Hello World PHP script with database to the managed host.
  12)get status of success of launching php page.
  13)get status of success of launching php page through my sql.

[play 2 on control server(local)]
IN result_on_control role:
  1)test access to php page through control server.
  2)test access to (php from mysql) page through control server.

######################################################################################

NOW:

- you should have apache with php module for it and mysql installed on the managed hosts.
- you can check the files <php_test> & <php_through_mysql_test> under /root/ of each managed host for the result whether everything is as planned or not.
- you can check the files <php_test> & <php_through_mysql_test> under /home/Ahmed of the local control server.
  ****you should change the path to where the files are touched on the local control server.
  ****at least change </home/Ahmed/.....> to </home/YOUR_USER/.....> on /roles/result_on_control/defaults/main.yml 
- you can curl <ip address> of managed hosts to check the index.php file.
- you can curl <ip address>/index.php of managed hosts to check the index.php file if you have index.html already on the managed hosts.
- you can curl <ip address>/db.php of managed hosts to check the db.php file.

######################################################################################

Hope you find this project helpful :))

