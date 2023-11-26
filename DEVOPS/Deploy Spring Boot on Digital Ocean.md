  REF: https://studygyaan.com/spring-boot/deploy-spring-boot-app-on-vm-using-nginx-https-domain
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

Now lets add record, which will point our domain ip address, like bellow image.![[image-11-1024x259.webp]] Create Record to Point Ip Address In Digital Ocean

### Setup Spring Boot Project using Nginx Reverse Proxy

On the server, Nginx is already installed. Create an Nginx configuration for the website with the command below. For demo purpose, we are using domain `example.com`. Please replace with your domain appropriately

```
sudo vi /etc/nginx/sites-available/example.com
```

And please add bellow code inside it.

```
server {
    server_name example.com;
    index index.html index.htm;
    access_log /var/log/nginx/example.log;
    error_log  /var/log/nginx/example-error.log error;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:8080;
        proxy_redirect off;
    }
}
```

**Note**: Please replace **`**example**`.com** with your domain.

Now enable the website

```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com
```

Let’s verify if there is no Nginx error, then reload it to take the changes into account:

```
sudo nginx -t
sudo nginx -s reload
```

Lets re-run the project – `./mvnw spring-boot:run`

Navigate to you domain to see the running project.

**Optional**: For easy spring boot [project](https://studygyaan.com/category/spring-boot) running i have written shell script, you can find in project: `startup.sh, restart.sh and shutdown.sh`

For running project – `sh startup.sh`

For stop project – `sh shutdown.sh`

### SpringBoot Enable HTTPS: Add SSL Certificate using Lets Enrypt

Install Certbot, which is the tool responsible for certificate generation

```
sudo apt install snapd
sudo snap install --classic certbot
```

Generate and install an SSL certificate for our domain. Please replace **example.com** with your domain name.

```
sudo certbot --nginx -d example.com
```

Reload Nginx configuration: `sudo nginx -s reload` and go to your website, you will see secure website.