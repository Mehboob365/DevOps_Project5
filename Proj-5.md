**Understanding Client-Server Architecture**


As we proceed on our journey into the world of IT, we begin to realise that certain concepts apply to many other areas. One such concepts is – Client-Server architecture.

Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server".

![image](https://user-images.githubusercontent.com/67065306/132592379-5afd4dee-2985-4266-b34c-ccaae10720fd.png)

**IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).**

TASK1 – Implement a Client Server Architecture using MySQL Database Management System (DBMS).

To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS) actioned as below;

Created and configured two Linux-based virtual servers (EC2 instances in AWS).

Server A name - `mysql server`
Server B name - `mysql client`

![image](https://user-images.githubusercontent.com/67065306/132704393-938d9572-d297-4873-987c-4c33e0051083.png)

Task2. On mysql server Linux Server install MySQL Server software.
 1. sudo apt update - y
 2. sudo apt install mysql-server -y
 3. sudo systemctl enable mysql
 
 ![image](https://user-images.githubusercontent.com/67065306/132705735-0281b2e5-6c93-440f-87fc-c626c54b04d6.png)

Task3. On mysql client Linux Server install MySQL Client software.
  1. sudo apt update - y
  2. sudo apt install mysql-client -y
  
![image](https://user-images.githubusercontent.com/67065306/132706597-9e615247-2c3b-4a0c-a8e4-834caad34111.png)

Task3. By default, both of our EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. 
We will use mysql server's local IP address to connect **from** mysql client. 
MySQL server uses TCP port 3306 by default, so will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. 
For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

![image](https://user-images.githubusercontent.com/67065306/132707959-64a02956-126a-4e0b-a777-88c0823e4dc4.png)

We still need a database on the server and a user on the client.

sudo mysql_secure_installation

![image](https://user-images.githubusercontent.com/67065306/132709452-3678cf6b-7b3b-4c38-8c21-a8eea6d95edd.png)

On the server run
sudo mysql
![image](https://user-images.githubusercontent.com/67065306/132710035-c90f3050-b393-4648-8061-b1f2481996e7.png)

on the Server, we will create a user 

1. CREATE USER 'remote_user'@'%' IDENTIFIED WITH MYSQL_NATIVE_PASSWORD BY '<password>'
2. CREATE DATABASE test_db;
3. GRANT ALL on test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;
4. FLUSH PRVILEGES
5. EXIT
 ![image](https://user-images.githubusercontent.com/67065306/132711969-01c25feb-288f-4156-9938-e21949a3a7f6.png)

 Task5. We need to configure MySQL server to allow connections from remote hosts.
 
 sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf    Replace bind-address with 0.0.0.0
 
 ![image](https://user-images.githubusercontent.com/67065306/132714756-cbfb6eb2-2b8c-4098-a878-4e7ce911eeb7.png)

 on Server run
 
 sudo systemctl restart mysql
 
 Task6. On mysql client Linux Server connect remotely to mysql server Database Engine without using SSH. 
         We will use the mysql utility to perform this action.
 
 On mysql client run
 
 sudo mysql - u remote_user -h 'server public ip address' -p
 
 ![image](https://user-images.githubusercontent.com/67065306/132715900-198a984d-5810-4cd1-934b-4a496d5a7290.png)

 mysql) show databases
 

 ![image](https://user-images.githubusercontent.com/67065306/132716644-76b08fa2-70e3-48cb-9a68-d3ae114315bb.png)

 
 
 
 

