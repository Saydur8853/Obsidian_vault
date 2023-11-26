  
### Prepare Virtual Machine Server

##### Access Server
##### Access Server
ssh root@SERVER_IP_ADDRESS

## Prerequisites Software’s
For this project, we will require following softwares

- Java Development Kit
- Apache Maven 
- Nginx

#### Install Java Development Kit

```
sudo add-apt-repository ppa:linuxuprising/java -y
sudo apt update
sudo apt-get install oracle-java17-installer oracle-java17-set-default
```

#### Install Maven 

```
sudo apt install maven
```

#### Install Nginx Web server

```
sudo apt updatesudo apt install nginxsudo ufw allow 'Nginx Full'systemctl status nginx
```

## Setup Project on Server

After install above software’s, please get your project on server. For this project i’m using git to pull my project which is hosted on Github. Here’s the starter [project](https://github.com/studygyaan/spring-boot-starter) for demo purpose.

```
sudo apt install git
```

git clone https://github.com/studygyaan/spring-boot-starter.git

Navigate to the project folder `cd spring-boot-starter/` and run the project using maven.

```
./mvnw spring-boot:run
```

Now your project is running on port 8080, as specified in file – `src/main/resources/application.properties`

Now go to browser and type your server ip address with port number. Example – SERVER_`IP_ADDRESS:8080`
![[image-8.webp]]   


Now lets stop the project `Ctrl+C` and run the same project using Nginx Server.

### Change Nameservers and Add Domain to Digital Ocean

Before deploying project on Nginx, we need a domain. Change the Nameserver in your domain provider and add it to Digital Ocean Domain.![[image-12.webp]]  Point to DigitalOcean Nameservers in Godaddy![[image-10-1024x253.webp]] Adding Domain to Digital Ocean