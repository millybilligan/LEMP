## LEMP (Linux, Nginx, MySQL, PHP) installation on Arch Linux.

### Installing MySQL.

$ `sudo pacman -Sy mariadb`  
$ `sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`  
$ `sudo systemctl start mariadb`  
$ `sudo mysql_secure_installation`  
$ `sudo mysql -u root -p`  

### Installing PHP.

$ `sudo pacman -Sy php php-fpm`  
$ `sudo systemctl start php-fpm`  

### Installing Nginx.

$ `sudo pacman -Sy nginx`  
$ `sudo systemctl start nginx`  
$ `curl localhost # Functional check`  

### Configure Nginx.

$ `sudo vim /etc/nginx/nginx.conf`  

**Add these lines in 'server {}':**  

`location ~ \.php$ {`  
      `fastcgi_pass   unix:/var/run/php-fpm/php-fpm.sock;`  
      `fastcgi_index  index.php;`  
      `root   /srv/http;`  
      `include        fastcgi.conf;`  
`}`
 
### Check PHP.

$ `touch /srv/http/info.php`  
$ `echo "<?php phpinfo(); ?>" > /srv/http/info.php`  
$ `curl localhost/info.php`  

### At the end.

$ `sudo systemctl enable nginx php-fpm mariadb`  
