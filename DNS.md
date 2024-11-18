## Cache
/etc/bind/named.conf
```
recursion yes;
allow-query {any;};
```

## FQDN
/etc/bind/named.conf
```
$TTL    86400
@       IN      SOA     ns.manex.zubiri. admin.manex.zubiri. (
                        2156878         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                          86400 )       ; Negative Cache TTL
;
@       IN      NS      ns.manex.zubiri.
ns      IN      A       127.0.0.1
pc1     IN      A       172.31.35.200
pc2     IN      A       172.31.35.222
www     IN      A       172.31.35.223
@       IN      MX      10 mail.manex.zubiri.
mail    IN      A       172.31.35.224
```
### Inversa
```
$TTL    604800
@       IN      SOA     ns.manex.zubiri. admin.manex.zubiri. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      localhost.
1.0.0   IN      PTR     localhost.
127.0.0.1       IN      PTR     ns.manex.zubiri.
200     IN      PTR     pc1.manex.zubiri.
222     IN      PTR     pc2.manex.zubiri
223     IN      PTR     www.manex.zubiri.
224     IN      PTR     mail.manex.zubiri.
```

### Conf
/etc/bind/named.conf.local
```
zone "manex.zubiri" IN {
        type master;
        file "/etc/bind/db.manex.zubiri";
        allow-transfer {172.31.35.254;};
        also-notify {172.31.35.254;};
};

zone "42.31.172.in-addr.arpa" IN {
        type master;
        file "/etc/bind/db.172";
};

zone "maranzadi.eus" IN {
        type master;
        file "/etc/bind/db.maranzadi.eus";
        allow-transfer {172.31.35.254;};
        also-notify {172.31.35.254;};
};
```

## SLAVE
### Conf
/etc/bind/named.conf.local
```
zone "manex.zubiri" IN{
	type slave;
	masters {172.31.42.42;};
	file "/var/cache/bind/db.manex.zubiri";
}