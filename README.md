# Installation-of-mysql-on-Ubuntu-
# Detailed run book of mysql installation on Ubuntu



Instullation of Mysql on Ubuntu Serve

These are the steps i took to install Ubuntu on my Linux Server via the terminal

 ## I loaded MySql download page and clicked through till i got to the just start my download which i right clicked on to extract the link
 # I had to ascertain what directory i was in by using
    pwd (i was in my home directory). 
#I changed my directory into the tmp directory by running 
   cd /tmp
# Downloaded MySql file, the wget command helps to download files from the web.+/
    wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb
# I listed the files in tmp directory to be sure i have the file downloaded
    ls
# It returned the files in the tmp directory including the file i just download and that was in red : mysql-apt-config_0.8.10-1_all.deb
# In order to install the file i have just downloaded, the whole mysql package suite. I have to run the below command. sudo gives elevated rights, dpkg is use to install, remove and inspect .deb software packages. The -i flag indicates we will like to install the named file, take note of the asterisk
    sudo dpkg -i mysql-apt-config*
  Note
    After doing this a configuration screen will pop up, which specifys the version of sql and some other information. I used the down arrow to select the OK option and then hit enter.
# I had to refresh the apt package cache to make the newly downloaded file available
  sudo apt update
# It's time to install the actual mysql-server, the apt will determine that the mysql it is about to install is the newest and best amongst the other mysql-server packages available. 
    sudo apt install mysql-server
# It then asked if i approve of it, i typed y and then ENTER. The software then gets installed. 
# I then had to set and confirm a root password
# I got a prompt where i choose the default authentication plugin
# Now mysql is installed and running, but to be sure i had to run the below command, the systemctl can be use to check status, stop and re-start a service by susbstituting what option you want
   sudo systemctl status mysql


output


      ● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2018-09-05 15:58:21 UTC; 30s ago   ( This shows mysql is active)
     Docs: man:mysqld(8)

   CGroup: /system.slice/mysql.service
           └─12805 /usr/sbin/mysqld

Sep 05 15:58:15 mysql1 systemd[1]: Starting MySQL Community Server...
Sep 05 15:58:21 mysql1 systemd[1]: Started MySQL Community Server.


# In other to perfom some security-related updates on my installation, i had to run the comman below
     mysql_secure_installation
# I had to enter my root password
# I also had to validate the component of my password, entered y and choose medium level
# Got a prompt to change my root password which i didnt want, i enetered enter to skip that 
# was prompted to remove anonymous user which i hit entered to skip, i want to keep anonymous user at this point
# I didnt allow root remote login
# I agreed to having the test database for practice purpose
# Reloaded privilege tables


Boom! Done!!

To Test my installation 


# I ran the below code
   mysqladmin -u root -p version

The -u root is to tell mysqladmin to log in as the mysql root user, the -p instructs mysql client tool to ask for password and the version is the actual command we want to run.


output

mysqladmin  Ver 8.0.12 for Linux on x86_64 (MySQL Community Server - GPL)
Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its


affiliates. Other names may be trademarks of their respective
owners.

Server version      8.0.12
Protocol version    10
Connection      Localhost via UNIX socket
UNIX socket     /var/run/mysqld/mysqld.sock
Uptime:         6 min 42 sec

Threads: 2  Questions: 12  Slow queries: 0  Opens: 123  Flush tables: 2  Open tables: 99  Queries per second avg: 0.029

 
