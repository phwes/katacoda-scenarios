# Putting things together
It's not very fun to just print "success".
Let's create a table and a few entries to print on our web page!

## Create MySQL entries 
`mysql -uroot -pguest -h 172.18.0.2 -P 3306`{{execute}}
`USE DATABASE myTestDB`{{execute}}  
`CREATE TABLE meetings ( id INT(6)  UNSIGNED AUTO_INCREMENT PRIMARY KEY, name VARCHAR(30) NOT NULL, location VARCHAR(30) NOT NULL, time TIME);`{{execute}}  
`INSERT INTO meetings (name, location, time) VALUES ('Breakfast meeting', 'Canteen', '08:00:00' );`{{execute}}  
