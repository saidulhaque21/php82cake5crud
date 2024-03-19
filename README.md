# php82cake5crud - Docker PHP 82 and CakePHP 5 Application   
CakePHP 5 Application in Docker : Apache, PHP 82, mysql and phpMyAdmin in docker!
A PHP Docker application integrating Apache, PHP 82, MySQL, and phpMyAdmin offers a comprehensive environment for web development and database management within Docker containers. This setup enables a convenient and portable development environment, making it easier to deploy, manage, and scale web applications.

The key components of this Docker setup include:

CakePHP 5: CakePHP is an open-source web framework. It follows the model–view–controller approach and is written in PHP, modeled after the concepts of Ruby on Rails, and distributed under the MIT License. CakePHP 5 is a web development framework running on PHP 8.2 (min. PHP 8.1). 

Apache:  The web server that serves the PHP web pages. It handles requests and serves the PHP content to users over the internet.

PHP 82: The scripting language used for server-side web development. It works in conjunction with Apache to process and generate dynamic web content.

MySQL: A robust and popular relational database management system. It stores and manages the application's data, providing a reliable backend for various web applications.

phpMyAdmin: A web-based graphical interface for managing MySQL databases. It simplifies tasks related to database administration, allowing users to interact with MySQL databases visually.

 

By encapsulating these components within Docker containers, this setup ensures portability, consistency, and ease of deployment. Developers can define and manage the entire environment via a docker-compose.yml file, simplifying setup across different machines and environments.

This Dockerized application offers an efficient workflow for web development, facilitating the creation, testing, and deployment of PHP-based web applications while also providing a user-friendly interface, via phpMyAdmin, for database management and manipulation.

# Step 1: Pull 
pull this docker from this repository 

# Step 2: go to php82cake5crud folder 
cd php82cake5crud

# Step 3: Change env configures if you want 
open docker-compose file and cheange database user, pass, port etc if you want 

# Step 4: run compose 
docker-compose up -d --build 

# Step 5: install CakePHP 5
To create a project, You need to read document: https://book.cakephp.org/5/en/installation.html 
Now, go to container application directory  

 docker exec -it php82cake5crud bash

It will show the directory: 
`/var/www/html`

Isside docker, check composer is installed properlly or not using following command: 
`composer -v `  

If show the version, composer is ok. 

After that, create a project using following command in the directory  /var/www/html:

`composer create-project --prefer-dist cakephp/app:~5.0 . `


# Step 6: Enjoy first part - Installation Cakephp and  phpMyAdmin
Browse for cake application  http://localhost:8255/ 

For phpMyAdmin http://localhost:8251/
`
HOST: mysql_php82cake5cruddb
Username: droot
Pass: Pass123
Database: myweb_db
Port: 3855 
`

# Step 7: DB connection 
 change read/write permission of src: 
`sudo chmod -R 777 src`

After that change app_local.php file follow section 
'Datasources' => [
        'default' => [
            'host' => 'mysql_php82cake5cruddb',
            /*
             * CakePHP will use the default DB port based on the driver selected
             * MySQL on MAMP uses port 8889, MAMP users will want to uncomment
             * the following line and set the port accordingly
             */
            //'port' => 'non_standard_port_number',

            'username' => 'droot',
            'password' => 'Pass123',

            'database' => 'myweb_db',
            /*
             * If not using the default 'public' schema with the PostgreSQL driver
             * set it here.
             */
            //'schema' => 'myapp',

            /*
             * You can use a DSN string to set the entire configuration
             */
            'url' => env('DATABASE_URL', null),
        ],
`

 Perfect, check refreash browser, it connected database. 

# Step 8: Cake Bake - CRUD operation 
 Create plugin with following command

` bin/cake bake plugin ContactManager `
after that, execute following command 

`bin/cake bake all --plugin ContactManager Contacts`

Great!

so browse 
`http://localhost:8255/contact-manager/contacts`

add, update, delete, view contact and enjoy. 

Note: if you face some problem related Cross-Site Request Forgeries (CSRF), just change follow line true to false in the src/Application.php file 
`
->add(new CsrfProtectionMiddleware([
                'httponly' => false,
            ]));
`

# Step 9: enjoy 

