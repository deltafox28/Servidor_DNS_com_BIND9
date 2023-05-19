# Criando uma zona reversa

##
```sh
vim named.conf.local

zone "88.168.192.in-addr.arpa" {
     type master;
     file "/etc/bind/inversa.db";
};
```


##
```sh 
vim /etc/bind/inversa.db
```

##
```sh
$TTL 8h ;
@	IN	SOA	dns1.empresa.com.br. root.empresa.com.br. (
			2018041703 ; serial
			3h ; refresh
			30m ; retry
			4d ; expiry
			1h ; negative cache
);
@	IN	NS	dns1.empresa.com.br.
@	IN	NS	dns2.empresa.com.br.
@	IN	MX	5 mail.empresa.com.br.
2	IN	PTR	dns1.empresa.com.br.
3	IN	PTR	dns2.empresa.com.br.
5	IN	PTR samba.empresa.com.br.
4	IN	PTR	dhcp.empresa.com.br.
7	IN	PTR	www.empresa.com.br.
1	IN	PTR	firewall.empresa.com.br.
3	IN	PTR	mail.empresa.com.br.
```


## 
```sh
named-checkzone 88.168.192.in-addr.arpa inversa.db
```

##
```sh
systemctl restart bind9
```

##
```sh
dig -x 192.168.88.2
```

##
```sh
dig -x 192.168.88.3
```
