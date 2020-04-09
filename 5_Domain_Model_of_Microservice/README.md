# The Microservice and its Domain Model

This lab is dedicated to the data management of the microservice we identified in the previous step. The overall goal is that the microservice consumes legacy data from the monolith but persists new data in its own database.

For more details about this lab, please take a look at the following blog post: [Identifying its Domain Model](https://www.dynatrace.com/news/blog/monolith-to-microservices-the-microservice-and-its-domain-model/).

![domain_model](../assets/domain_model.png)

## Step 1: Use Dynatrace to learn more about the Domain Model

1. Open service flow as explained in **Lab 4 - Identify a Microservice** at **Step 3**.
1. Follow the service flow through BookingService and your custom service. 
1. Click on the MySQL instance **ticketmonster** and on **View database statements**.

## Step 2: Create database for microservice

1. Create the database for the microservice.
    ```
    oc new-app --name=orders-db -e MYSQL_USER=ticket -e MYSQL_PASSWORD=monster -e MYSQL_DATABASE=orders mysql:5.5
    ```

## Step 3: Setup database
curl -o 0_ordersdb-schema.sql https://raw.githubusercontent.com/dynatrace-innovationlab/monolith-to-microservice-openshift/master/orders-service/src/main/resources/db/migration/0_ordersdb-schema.sql

curl -o 1_ordersdb-data.sql https://raw.githubusercontent.com/dynatrace-innovationlab/monolith-to-microservice-openshift/master/orders-service/src/main/resources/db/migration/1_ordersdb-data.sql

mysql -u root orders < 0_ordersdb-schema.sql

mysql -u root orders < 1_ordersdb-data.sql

mysql -u root

GRANT ALL ON orders.* TO 'ticket'@'%';

show databases;

use orders

show tables;

select * from id_generator;

