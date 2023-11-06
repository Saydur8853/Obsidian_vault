Different Ways to Create Spring Boot Project
1. Using spring initializ(start.spring.io)
2. Using Spring Starter Project in STS (Eclipse)
3. Spring Boot CLI
The Spring Boot CLI is a command line tool that you can use if you
want to quickly develop a Spring application.

Project - Maven
Dependency - **Spring Web**, Spring data JPA, MySQL Driver, Lombok




```

```
`sudo apt install nano`
// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', getenv_docker('WORDPRESS_DB_NAME', 'ecomilli_hwc') );

/** Database username */
define( 'DB_USER', getenv_docker('WORDPRESS_DB_USER', 'root') );

/** Database password */
define( 'DB_PASSWORD', getenv_docker('WORDPRESS_DB_PASSWORD', '123@#$Ecomilli') );
/**
 * Docker image fallback values above are sourced from the official WordPress installation wizard:
 * https://github.com/WordPress/WordPress/blob/f9cc35ebad82753e9c86de322ea5c76a9001c7e2/wp-admin/setup-config.php#L216-L230
 * (However, using "example username" and "example password" in your database is strongly discouraged.  Please use strong, random credentials!)
 */

/** Database hostname */
define( 'DB_HOST', getenv_docker('WORDPRESS_DB_HOST', 'mysql') );
docker exec -it 9e813d47161b bash

e63eb46a0a64

mysql -u root -p
mysqldump -u root -p ecomilli_hwc > ecomilli_hwc_bak.sql
docker cp 9e813d47161b:/backup/ecomilli_hwc_bak.sql .


zip -r ecomilli-front-end_6_nov_23.zip ecomilli-front-end/
