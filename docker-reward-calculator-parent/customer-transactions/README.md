# Customer transactions micro service

## Introduction

This service will handle the to customer transactions. We can save the customer transactions and use them to calculate the total reward points based on the total purchase amount. This spring boot micro service also includes the below features

- Junit parameterized test cases
- Code coverage 
- Functional test cases (Possitive & Negative)
- Logging using logback
- Actuator metrics
- Exception handling
- Java documentation
- Lombok for automatic code generation

This micro service will support below services

URL: http://localhost:8686/customer/transaction/

- Create transaction (POST)
- Get all transactions by customer id (GET -/custid/{customerId})
- Delete transactions by id (DELETE - /{id})

## Technologies Used

- Java 17 (This will work with java 11 also. We need to modify the version in the pom.xml to point to 11 (_<java.version>11</java.version>_)).
- SpringBoot 3.0.x
- H2 database to store the configuration data

If you are using java.version 11, then make sure java_home also should point to java 11 to build the project in the command prompt.

## Tools used

- Maven for build
- Jacoco for coverage
- STS 4.x for development


## H2 configuration details:
This service will use H2 database with below configuration details

```
Database connection url: jdbc:h2:file:/data/rewards-cust-transaction
username: admin
password: admin
```
We can access the h2 console using the URL: ```http://localhost:8686/customer/transaction/h2-console```

![alt text](https://github.com/sureshdharisi/rewards_calculator/blob/develop/rewards-calculator-parent/customer-transactions/h2console_login.PNG?raw=true)

![alt text](https://github.com/sureshdharisi/rewards_calculator/blob/develop/rewards-calculator-parent/customer-transactions/h2console_home.PNG?raw=true)

Run the below steps to create initial database setup for the configuration service.

### Drop predefined data structure
```sql
DROP SEQUENCE cust_transaction_seq;
DROP TABLE CUST_TRANSACTIONS;
```
### Create sequence using below query
```sql
CREATE SEQUENCE cust_transaction_seq START WITH 1 INCREMENT BY 1;
```
### Create table
```sql

CREATE TABLE CUST_TRANSACTIONS
(ID INTEGER NOT NULL,
CUSTMER_ID VARCHAR(50) NOT NULL,
TRANSACTION_AMT INTEGER ,
TRANSACTION_DT DATE ,
CREAE_DT DATE,
PRIMARY KEY (ID));
```

## Testing scenarios

### Base URL: localhost:8686/customer/transaction/

|Scenario|URL | Request Method | Payload | Response |
|---------|-----|-----------------|----------|-----------|
| Create customer transaction | / | POST | ``` {"customerId":"ABC","transactionAmt":100,"transactionDate":"2022-12-09"} ``` | ``` {"transactionId":8} ```|
| Get transactions by customer Id | /custid/{customerId} | GET | ABC | ``` [{"id":7,"customerId":"ABC","transactionAmt":100,"transactionDate":"2022-11-09"},{"id":8,"customerId":"ABC","transactionAmt":100,"transactionDate":"2022-12-09"}] ```|
| Delete transaction by id | /{id} | DELETE | 1 or 2 or 3 | ``` {"message": "The configuration 1 is deleted successfully"} ```|


## Junit test cases details
![alt text](https://github.com/sureshdharisi/rewards_calculator/blob/develop/rewards-calculator-parent/customer-transactions/code_coverage.PNG?raw=true)


### How to run?
1. Download the code from github using below url

    ```
    git clone https://github.com/sureshdharisi/rewards_calculator.git
    ```
2. Goto the project where pom.xml is located 

    ```
    cd rewards_calculator/rewards-calculator-parent/customer-transactions
    ```
3. Run the maven command. The below command will run the junit test cases automatically

    ```
    mvn clean install
    ```
4. Run the application using spring boot plugin.

    ```
    mvn spring-boot:run
    ```
### Management URL

```
http://localhost:8686/customer/transaction/manage
```
