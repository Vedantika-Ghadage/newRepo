+++
title = "Verify Data in the New Pod"
description = ""
weight=90
+++
{{%excerpt%}}

When a node is disabled on the original pod, Kubernetes reschedules the pod on another, available host in the cluster and assigns the pod a new name. 

To verify the data in the rescheduled and renamed pod, select *Environments* from the sidebar menu and open the environment and application. Then select the pod name.

![image](/images/rook-37.png)

Next, login to the mysql database. Select *Environments* from the sidebar menu and open the environment, application, and pod. Select mysql from the *Running Containers* list. Click gear icon in the top right corner and select *Launch Terminal*.

![image](/images/rook-38.png)

The displayed command is *sh*. Do not change the command. Select *Connect Terminal*.

![image](/images/rook-39.png)

In the terminal window, enter the Connect to mysql Database as a Root User command. 

**mysql Command to Connect to Database as Root User:**  

```
mysql -u root -pchangeme
```


![image](/images/rook-40.png)

Verify the ‘testrook’ database by entering the Show Databases command.

**Show Databases Command:**  

```
mysql> show databases;
```

The following will display:

```
+---------------------+
| Database            |
+---------------------+
| information_schema  |
| #mysql50#lost+found |
| mysql               |
| performance_schema  |
| testrook            |
+---------------------+
5 rows in set (0.01 sec)
```
Connect to the testrook database by using the Connect to testrook Database command.

**Connect to testrook Database Command:**

```
mysql> use testrook;
```

When connected, the following message will display:

```
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```
Verify the records in the table by using the View Table command.

**View Table Command:**  

```
mysql> select * from employee;
```

The following table will display:

```
+-----+--------+------------+--------+
| id  | name   | dept       | salary |
+-----+--------+------------+--------+
| 100 | Thomas | Sales      |   5000 |
| 200 | Jason  | Technology |   5500 |
| 300 | Mayla  | Technology |   7000 |
| 400 | Nisha  | Marketing  |   9500 |
| 500 | Randy  | Technology |   6000 |
+-----+--------+------------+--------+
5 rows in set (0.00 sec)
```

Exit from mysql and terminal using the Exit command.

**Exit Command:**

```
mysql> exit
```
   
{{%/excerpt%}}