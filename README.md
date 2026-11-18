
services:
  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: wordpress
      MYSQL_USER: user
      MYSQL_PASSWORD: pass123
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - mynetwork

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: user
      WORDPRESS_DB_PASSWORD: pass123
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db
    networks:
      - mynetwork

volumes:
  db_data:

networks:
  mynetwork:

=============================================================================

docker pull mysql:8.0
docker pull wordpress:latest


docker compose up -d

docker ps

docker network ls

docker volume ls

http://localhost:8080

7.Demonstrate recovery
docker stop wordpress-app
docker compose up -d

8.To demonstrate database persistence:
docker compose down
docker compose up -d

======================================================================================jenkins=====================
cd /d "C:\Users\harik\Downloads\apache-tomcat-9.0.120-windows-x64\apache-tomcat-9.0.120\bin"
catalina.bat run
====================================kubernetes===================================
Start Minikube	minikube start
Check nodes	kubectl get nodes
Create deployment	kubectl create deployment app --image=nginx
Check Pods	kubectl get pods
Check deployments	kubectl get deployments
Scale deployment	kubectl scale deployment app --replicas=5
Expose application	kubectl expose deployment app --type=NodePort --port=80
Delete Pod	kubectl delete pod pod_name
Rolling update	kubectl set image deployment/app nginx=nginx:1.27
Rollback	kubectl rollout undo deployment/app
Check rollout	kubectl rollout status deployment/app


======================================nagios==================
docker pull jasonrivers/nagios:latest

docker run --name nagiosdemo -d -p 8888:80 jasonrivers/nagios:latest

docker ps

http://localhost:8888 or http://localhost:8082

docker start nagiosdemo

to inspect host nd service monitoring :docker exec -it nagiosdemo bash

Inside the container:
ls /opt/nagios/etc/objects
ls /opt/nagios/etc/conf.d



 Username: nagiosadmin
 Password: nagios
==============================================aws================
1. Open Services → EC2 → Launch Instance.
2. Configure:
Setting	Value
Name	Ubuntu-Web-Server
AMI	Ubuntu Server 22.04 LTS
Architecture	64-bit
Instance type	t2.micro or an available eligible small instance
Number of instances	1
Storage	8 GB



1. Select Create new key pair.
2. Name: ubuntu-key
3. Key pair type: RSA.
4. Private key format: .pem.
5. Download and save it safely. You will need this file to connect through SSH.
Security group:

Add these inbound rules:
Type	Port	Source	Purpose       descript..
Custom TCP	8080	Anywhere IPv4	Tomcat 



Connect through SSH
1. Open EC2 → Instances.
2. Select your instance.
3. Click Connect → SSH client.
4. Copy the SSH command shown by AWS




cd "C:\Users\YourName\Downloads\AWS"

ssh -i "ubuntu-key.pem" ubuntu@<Public-IP>


sudo apt update
sudo apt-get install docker.io
sudo apt install git
Sudo apt install nano


git clone https://github.com/harikaa2703/mavenWeb.git

cd mavenWeb

nano Dockerfile 

FROM maven:3.9.9-eclipse-temurin-11 AS build

WORKDIR /app


COPY . .


RUN mvn clean package -DskipTests


FROM tomcat:9-jdk11


COPY --from=build /app/target/webappSample.war /usr/local/tomcat/webapps/ROOT.war


EXPOSE 8080


CMD ["catalina.sh", "run"]


----------------------------------
sudo docker build -t mavenweb1 .
sudo docker run -d --name app-demo3 -p 6061:8080 mavenweb1

http://YOUR-PUBLIC-IP:6061
[
Open AWS Console → EC2 → Instances.
Select your running Ubuntu instance.
Under the Details tab, find Public IPv4 address.
Copy that IP address.
]
