#Archlinux MySQL PHP phpmyadmin Apache PHP-Apache Install

## By wangxian

1. ### Install the MySQL:
	[参考官方](https://wiki.archlinux.org/index.php/MySQL)
	1. ` sudo pacman -S mysql`
	2. ` sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql `
	3. ` sudo systemctl start mysqld.service `
	4. ` sudo systemctl enable mysqld.service `
	5. ` sudo mysql_secure_installation `
	6. ` mysql -u root -p ` enter the empty pasword and set the new root password 
	7. enter fourth y and complete

2. ### Install Apache PHP PHP-Apache
	[参考官方](https://wiki.archlinux.org/index.php/Apache_HTTP_Server)
	1. ` sudo pacman -S apache `
	2. ` sudo systemctl start httpd `
	3. ` sudo systemctl enable httpd `
	4. ` curl 127.0.0.1 ` can get some data, that mean it works.
	5. In /etc/httpd/conf/httpd.conf, 
	comment the line:
		` #LoadModule mpm_event_module modules/mod_mpm_event.so `
    and uncomment the line:
    	` LoadModule mpm_prefork_module modules/mod_mpm_prefork.so `
    Place this in the LoadModule list anywhere after
    `LoadModule dir_module modules/mod_dir.so:`
    `LoadModule php7_module modules/libphp7.so`
    
    Place this at the end of the Include list:
    `Include conf/extra/php7_module.conf`
    
    restart the http.service
    `sudo systemctl restart httpd`
    OK, It's work to accss the http://localhost

3. ### Install phpmyadmin
	[参考官方](https://wiki.archlinux.org/index.php/PhpMyAdmin)
    1. ` sudo pacman -S phpmyadmin php-mcrypt`
    2. editing /etc/php/php.ini, and uncomment the following line:
    	```
        extension=mysqli.so
        extension=mcrypt.so
        ```
    3. Create the Apache configuration file:
        `/etc/httpd/conf/extra/phpmyadmin.conf`
    	```
        Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
        <Directory "/usr/share/webapps/phpMyAdmin">
            DirectoryIndex index.php
            AllowOverride All
            Options FollowSymlinks
            Require all granted
        </Directory>
    	```
    4. And include it in /etc/httpd/conf/httpd.conf:
    	phpMyAdmin configuration
		`Include conf/extra/phpmyadmin.conf`
    5. restart the http.service
    	` sudo systemctl restart httpd `
    	OK, It's done to accss the http://localhost/phpmyadmin
