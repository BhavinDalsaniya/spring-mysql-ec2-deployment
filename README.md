# spring-mysql-ec2-deployment

# Steps to Set Up and Deploy the Spring Boot Application with MySQL

## 1. Create a VPC and Subnet
- Create a VPC in any one region with the CIDR block `10.0.0.0/16`.
- Create a subnet within the VPC with the CIDR block `10.0.1.0/24`.

## 2. Create and Attach an Internet Gateway
- Create an Internet Gateway (IGW) for accessing the internet.
- Attach the IGW to the created VPC.

## 3. Update the Route Table
- Add the Internet Gateway to the route table associated with the VPC.
- Ensure the route table has the following entries:
  - `10.0.0.0/16` for local traffic.
  - `0.0.0.0/0` with the Internet Gateway for external traffic.

## 4. Connect to Your EC2 Instance
- Use the following command to connect to your EC2 instance via SSH:
  ```bash
  cd Downloads
  ssh -i first-ec2.pem ubuntu@54.88.58.168

## 5. Clone the repository:
- Setup and Installation Guide
- ```bash
  mkdir repos
  cd repos/
  git clone https://github.com/rafsan-jany/spring-boot-rest-api-h2-database.git
  cd spring-boot-rest-api-h2-database  

## 6. Install Required Software :
- ```bash
  sudo apt update  
  sudo apt install openjdk-8-jdk -y  
  sudo apt install maven -y  

  java --version  
  mvn --version  

## 7. Add MySQL Dependency  
- Add the following MySQL dependency to pom.xml:  
  <dependency>  
      <groupId>mysql</groupId>  
      <artifactId>mysql-connector-java</artifactId>  
      <version>5.1.49</version>  <!-- Update the version if needed -->  
  </dependency>  

## 8. Modify Mockito Dependency  
- Remove the <scope>test</scope> tag from the Mockito dependency in pom.xml:  
  <dependency>  
      <groupId>org.mockito</groupId>  
      <artifactId>mockito-core</artifactId>  
      <!-- Remove this line: <scope>test</scope> -->  
  </dependency>  

## 9. Configure application.properties  
- Add the following entries to src/main/resources/application.properties:  
  spring.jpa.database-platform=org.hibernate.dialect.MySQL5Dialect  
  spring.jpa.hibernate.ddl-auto=create  
  spring.datasource.username=root  
  spring.datasource.password=root  

## 10. Install and Configure MySQL  
- ```bash
  sudo apt install mysql-server  
  sudo service mysql status  
  sudo mysql_secure_installation  

- Validate Password component? No  
- Remove anonymous users? No  
- Disallow root login remotely? No  
- Remove test database and access to it? No  
- Reload privilege tables now? Yes  

## 11. Update MySQL Root User
- ```bash
  sudo mysql  
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';  
  EXIT;  

## 12. Create Database 
- ```bash
  mysql -h localhost -u root -p  
- Enter the password: root.  
- CREATE DATABASE shipwreck;  

## 13. Build and Run the Application  
- ```bash
  mvn clean install -DskipTests  
  mvn spring-boot:run  

## 14. Access the Application  
- Open your browser and navigate to:  
  http://54.160.65.98:8181/index.html#/  
- Ensure that the security group for your EC2 instance allows inbound traffic on port 8181.  
- Replace 54.160.65.98 with your EC2 instance's public IP address if it changes.  
