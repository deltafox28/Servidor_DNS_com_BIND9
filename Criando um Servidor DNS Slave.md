# Criando um Servidor DNS Slave

##
```sh
vim /etc/netplan

gateway4: 192.168.88.2, 192.168.88.3
```

##
```sh
apt-get install bind9 -y
```

##
```sh
scp /etc/bind/named.conf.local root@dns2.empresa.com.br:/etc/bind/named.conf.local
```

##
```sh
vim /etc/bind/named.conf.local

zone "empresa.com.br" {
     type slave;
     file "direta.db";
	 masters { 192.168.88.2; };
};

zone "88.168.192.in-addr.arpa" {
     type slave;
     file "inversa.db";
     masters {192.168.88.2; };
};
```


##
```sh
ls -l /var/cache/bind
```
##
```sh
vim /etc/bind/named.conf.local

zone "empresa.com.br" {
      type master;
      file "/etc/bind/direta.db";
	  allow-transfer { 192.168.88.3; };
      notify yes;
      also-notify {192.168.88.3; };
};

zone "88.168.192.in-addr.arpa" {
      type master;
      file "/etc/bind/inversa.db";
	  allow-transfer { 192.168.88.3; };
      also-notify {192.168.88.3; };
};
```

##
```sh
rndc reload
```

##
```sh
tailf /var/log/syslog
```

##
```
ls -l /var/cache/bind/
```

##
```sh 
systemctl restart bind9

tail -n 30 /var/log/syslog

dig -x 192.168.88.4 @192.168.88.3
```


