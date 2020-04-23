# Putting things together
Now that we have a MySQL container and Apache container, let's put something together and see if it they can communicate with each other!  
## Create MySQL entries
We will begin by creating something for Apache to extract from the database.  
Start a mysql client session:  
`mysql -uroot -pguest -h 172.18.0.2 -P 3306`{{execute}}  
Create a database:  
`CREATE database myTestDB;`{{execute}}  
Select the database:  
`USE myTestDB;`{{execute}}  
Create a new table:  
`CREATE TABLE meetings ( id INT(6)  UNSIGNED AUTO_INCREMENT PRIMARY KEY, name VARCHAR(30) NOT NULL, location VARCHAR(30) NOT NULL, time TIME);`{{execute}}  
Insert a few entries into the table:   
`INSERT INTO meetings (name, location, time) VALUES ('Breakfast meeting', 'Canteen', '08:00:00' );`{{execute}}  
  
`INSERT INTO meetings (name, location, time) VALUES ('Midday meeting', '802', '11:30:00' );`{{execute}}  
  
`INSERT INTO meetings (name, location, time) VALUES ('After work', 'The Red room', '20:00:00' );`{{execute}}  
Exit MySQL interface:  
`exit`{{execute}}  

## Change load entries
For loading these entries I have prepared a small php page. This page will connect to the MySQL server on host "mysql-server" and print all entries in the table "meetings" in the database "myTestDB". The file is heavily inspired from w3schools [example](https://www.w3schools.com/php/php_mysql_select.asp).  
  
As with the php info page, just move the file as index.php to the shared volume space:  
`mv test_mysql_query html/index.php`{{execute}}  
  
Access the host on port 8080 and you should now see the entries printed on the web page!  
