
# Zerbitzari
## Instalatu
Server instalatu makina batean
```
sudo apt install mysql-server-y
sudo mysql_secure_installation
```
## Konektatu makina beretikan
```
sudo mysql
```

## Pasahitza aldatu
```
ALTER USER 'root'@'localhost' INDENTIFIED WITH mysql_native_password by 'batbihiru'
```

## Aldaketak kontuan artu
```
FLUSH PRIVILEGES;
```

## Saioa asi erabiltzaile batekin
```
mysql -u root -p
```

## Sortu erabiltzaile bat
```
CREATE USER 'maranzadieg_local'@'localhost' IDENTIFIED BY 'batbihiru';
CREATE USER 'maranzadieg_local'@'%' IDENTIFIED BY 'batbihiru';
```

## Sareko konexio fitxategia
```
nano /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0 ←fitxategian gehitu edo aldatu
sudo systemctl restart mysql
```

# Rolak

## Sortu
```
CREATE ROLE 'rol_mugatua';
```
## Ezarri baimenak
```
GRANT CREATE, SELECT, INSERT ON *.* TO 'rol_mugatua';
```

## Kendu baimenak
```
REVOKE DELETE ON *.* FROM 'maranzadi_sa'@'%':
```
## Ezarri rol bat erabiltzaile bateri
```
SET DEFAULT ROL 'rol_mugatia' TO 'maranzadi'@'%'
```
## Ikusi baimenak
```
SHOW GRANTS FOR 'maraznaid_local'@'localhost';
SHOW GRANTS FOR 'maraznaid_local'@'localhost' USING 'rol_osoa';
```

# EXTRA
- **Globalak**: mysql.user  
- **Datu-base mailakoak**: mysql.db  
- **Taula mailakoak**: mysql.tables_priv  
- **Kolumna mailakoak**: mysql.columns_priv  
- **Prozedura eta funtzioak**: mysql.procs_priv  
- **Rolak**: mysql.roles_mapping  
