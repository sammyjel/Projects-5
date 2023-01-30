# CLIENT-SERVER ARCHITECTURE WITH MYSQL

# IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

To begin the project, two Ubuntu servers must be set up on an AWS instance.

Call the first one "server," and the second "client."

run the following command to install mysql server on the server:

`sudo apt install -y mysql-server`

Install "mysql client" on the mysql client server using the command:

`sudo apt install -y mysql-clint`

Start the MySQL server console and run a security script with the command:

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password of your choice>';`

Please keep in mind that the password you create in the preceding command is for the root user.

Then, close the mysql console.

Start an interactive script by typing:

`sudo mysql_secure_installation`

Create a strong password next. The strength of your password will then be displayed, as shown in the image below:

![mysql password](./images/mysql%20password.png)

login again to mysql server console using :

sudo mysql -p

This will prompt you for the password you created.

Note: If you have successfully logged in, you will see a message similar to the one shown below:
![login into mysql with password](./images/sudo%20mysql.png)

Create a new user in your MySQL server's user table using the command:

To confirm that a user has been created, use the following command to open the mysql server user table:

`SELECT User, Host FROM mysql.user;`

This command will display a list of all existing users, as shown below:

![creation DB](./images/creation%20of%20DB.png)

create database with command: `CREATE DATABASE <database name>;`

and flush the privileges with command:

`FLUSH PRIVILEGES;`

Exit the mysql console once you've completed all of these steps.

To allow requests from the remote mysql client, the mysql server must be enabled. To accomplish this,

run `sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

Replace the default bind-address of 127.0.0.1 with 0.0.0.0, as shown in the image below:

![mysqld.conf](./images/mysqld%20conf.png)

To restart the MySQL server, type the following command:

`sudo systemctl restart mysql`

After this has been done, there is a need to open port 3306 on the mysql server to allow connection from the mysql client.

To do this, get the ip address of the mysql client by running command

`ip addr show` or `ifconfig` on the mysql client

After generating the ip address, open the security group of your mysql server on the EC2 instance and open port 3306 following the steps below:

open your mysql server security group ad click on edit inbound rules

![inbound rules](./images/inbound%20edit.png)

click on add rules

![another inmoud image](./images/inbound%20edit2.png)

paste in the ip generated from mysql client

![inbound 3](./images/inbound%20edit3.png)

Use the following command to establish a remote connection to the MySQL Server database engine after adding port 3306 on the MySQL Client Linux Server:

`sudo mysql -h <server public ip> -u <server username> -p<server password>`

You have successfully logged in remotely without using SSH, and I congratulate you on the successful connection, if the output from your server and client linux server is identical.

![connection between the 2 servers](./images/the2%20console%20servers.png)