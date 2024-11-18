/etc/apache2/sites-available/mugatua.conf
```
<VirtualHost *:80>


        ServerAdmin admin@manex.zubiri
        ServerName mugatua.maranzadi.eus
        ServerAlias mugatua
        DocumentRoot /home/mugatua


        <Directory /home/mugatua>
                AllowOverride All
                Options Indexes FollowSymLinks
                Require all granted
        </Directory>

        <Directory /home/mugatua>
                AuthType Basic
                AuthName "Acceso Restringido"
                AuthUserFile /etc/apache2/klabeak/.htpasswd
                Require valid-user
        </Directory>
        
```

.htaccess
```
AuthType Basic
AuthName "Acceso Restringido"
AuthUserFile /etc/apache2/klabeak/.htpasswd
Require valid-user


Options -Indexes
```
Sortu
```
sudo -cb /etc/apache/giltzak/.htpasswd admin admin
```

activatu 
```
sudo a2endom ssl
```
kendu web gunea 
```
sudo a2dissite 000-
```